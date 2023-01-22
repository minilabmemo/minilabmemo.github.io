---
title: "[docker]建立elasticSearch儲存資料與kibana呈現使用"
tags:
  - docker
  - elasticSearch
  - kibana
categories:
  - [Tech., deploy, docker]
  - [Tech., back-end,elasticSearch]
date: 2021-04-24 10:06:20
---

>本章介紹使用elasticSearch儲存資料與kibana呈現使用 


### 本文內容：
- 自行建立elasticSearch/kibana [docker]
- 建立elasticSearch index與傳送資料
- 使用kibana查詢資料


<!--more-->

### 1.啟動docker-elasticSearch/kibana
- 先備知識:docker & docker-compose
- 先將網路上找到的[docker-compose.yml](https://github.com/minilabmemo/docker-compose-record/tree/master/elastic_kibana)內容編輯好，然後在一樣的目錄下開啟指令docker-compose up -d

```bash
$docker-compose up -d
WARNING: Some services (elasticsearch, kibana) use the 'deploy' key, which will be ignored. Compose does not support 'deploy' configuration - use `docker stack deploy` to deploy to a swarm.
Starting elasticsearch-624 ... done
Starting kibana-624        ... done
```

需要一點時間，可以用Kitematic之類的工具查看有沒有成功<br>


- GET localhost:9200 確認elasticSearch是否啟動
成功會回版號等資訊 "number": "6.2.4"

- 開啟瀏覽器，確認kibana有無成功
http://127.0.0.1:5601/app/kibana#/home?_g=()


### 2.準備資料與index

- 先設計資料內容，假設今天要收集一個使用者每天的運動紀錄
這是一個有array的紀錄內容，內容可長可短。
```json
{
    "user": "user01",
    "timestamp": 1583734521000,
    "records": [
        {
            "record_name": "heart_rate",
            "data_number": 80,
            "data_txt": "avg"
        },
        {
            "record_name": "Calories",
            "data_number": 200
        },
        {
            "record_name": "time_duration",
            "data_number": 30,
            "record_unit": "min"
        }
    ]
}
```


#### 接著新增必須欄位的屬性index
- user是一般text,timestamp是date
- records先建立nested巢狀，在建立裡面的record_name等欄位。
- 建立index: PUT localhost:9200/{index}
```
PUT localhost:9200/event
{
    "mappings": {
        "_doc": {
            "properties": {
                "user": {
                    "type": "text",
                    "fields": {
                        "keyword": {
                            "type": "keyword",
                            "ignore_above": 256
                        }
                    }
                },
                "id": {
                    "type": "text",
                    "fields": {
                        "keyword": {
                            "type": "keyword",
                            "ignore_above": 256
                        }
                    }
                },
                "timestamp": {
                    "type": "date",
                    "format": "epoch_millis"
                },
                "records": {
                    "type": "nested",
                    "properties": {
                        "record_name": {
                            "type": "text",
                            "fields": {
                                "keyword": {
                                    "type": "keyword",
                                    "ignore_above": 256
                                }
                            }
                        },
                        "data_number": {
                            "type": "long",
                            "fields": {
                                "keyword": {
                                    "type": "keyword",
                                    "ignore_above": 256
                                }
                            }
                        },
                        "data_txt": {
                            "type": "text",
                            "fields": {
                                "keyword": {
                                    "type": "keyword",
                                    "ignore_above": 256
                                }
                            }
                        },
                        "record_unit": {
                            "type": "text",
                            "fields": {
                                "keyword": {
                                    "type": "keyword",
                                    "ignore_above": 256
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
```

#### 送資料進去
- 接著把上述資料先送一筆進去
-  http://localhost:9200/{index}/{type}
POST http://localhost:9200/event/_doc

### kibana建立index

- #### 建立index
Management頁面->create index->填入event->選擇可以做時間分割的欄位名稱{上述是用timestamp}->按下create index pattern<br>

- #### Discover頁面搜尋資料
再送一次資料，這次把 "timestamp": {改成現在時間戳}->線上有很多工具可以做轉換
回到Discover頁面，query最近15分鐘的資料->就可以看到時間軸了<br>

- #### Visualize 建立感興趣的圖表展示
ex: table顯示/長條圖顯示等/或是特定filter資料。然後替圖表存檔。<br>
- #### Dashboard 頁面
這邊把剛剛建立的圖表拉好顯示在這邊。

-  #### dev tools 頁面
透過條件指令搜尋特定資料，如有程式需要可以用搜尋API試著找出自己想搜尋的內容
- size/page/sort 分頁與排序依據
- bool query 條件-filter時間/range/match/wildcard等搜尋
	- 所有 must 必须匹配，所有 must_not 都必须不匹配
	- minimum_should_match 參數控制需要匹配的 should 語句的數量
	
範例:
```
GET /event/_search
{
  "size": 1000,
  "query": {
    "bool": {
      "filter": {
        "range": {
          "timestamp": {
            "from": 159132465000,
            "include_lower": true,
            "include_upper": true,
            "to": 1591324650099
          }
        }
      },
      "must": [
        {
          "exists": {
            "field": "user"
          }
        },
        {
          "match": {
            "user": {
              "operator": "AND",
              "query": "user01"
            }
          }
        },
        {
          "nested": {
            "path": "records",
            "query": {
              "bool": {
                "must": [
                  {
                    "match": {
                      "records.record_name": {
                        "operator": "AND",
                        "query": "heart_rate"
                      }
                    }
                  },
                  {
                    "wildcard": {
                      "records.data_txt": "*a*"
                    }
                  },
                  {
                    "range": {
                      "records.data_number": {
                        "from": 2,
                        "include_lower": false,
                        "include_upper": true,
                        "to": null
                      }
                    }
                  }
                ]
              }
            }
          }
        }
      ],
      "minimum_should_match": "1",
      "should": [
        {
          "match": {
            "user": {
              "operator": "AND",
              "query": "user01"
            }
          }
        },
        {
          "match": {
            "user": {
              "operator": "AND",
              "query": "user02"
            }
          }
        }
      ]
    }
  },
  "sort": [
    {
      "timestamp": {
        "order": "desc"
      }
    }
  ]
}

```


###  網路參考文章
>note warning %} <span style="font-size: 9px;">
學習路上感謝網路大神們，如果你發現了我，可以查看參考文章了解更多概念👇👇👇
</span>
- [elastic-組合查詢 中文](https://www.elastic.co/guide/cn/elasticsearch/guide/current/bool-query.html "elastic-組合查詢 中文")

