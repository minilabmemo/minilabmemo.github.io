---
title: "[Go 08] 認識時間格式與golang的時區轉換寫法"
tags:
  - golang
categories:
  - [Backend,golang]
date: 2021-05-30 10:22:20
---


>
開發過程中，曾遇過部署到別的平台，時間就變成+0時區了（例如明明下午五點，部署平台顯示早上九點），這時才發現原來你的時間不是他的時間，而資料庫中也常常用時間戳數字來做紀錄，但顯示給使用者時又要轉成格式化顯示，本篇紀錄各種時間格式的理解與go程式對於時間的使用
<!--more-->



## 理解時間的各種顯示格式
時間可以以很多格式化的方式做顯示。例如最常看到的2021-04-22 17:27:44
### 標準時間格式
國際標準格式，像是 [ISO_8601](https://zh.wikipedia.org/wiki/ISO_8601)
- 合併表示時，要在時間前面加一大寫字母T
- 如果時間在零時區，並恰好與協調世界時相同，那麼（不加空格）在時間最後加一個大寫字母Z
例如以下這樣的顯示方式:
```
2021-04-28T01:51:35Z
2004-05-03T17:30:08+08:00  //+08:00代表比世界協調時間快8小時的時區
```


### UNIX時間與時間戳
UNIX時間代表從UTC1970年1月1日0時0分0秒起至現在的總秒數
* 而UTC為世界協調時間（英語：Coordinated Universal Time，法語：Temps Universel Coordonné，簡稱UTC）是最主要的世界時間標準。
- 這種你會看到可能是十位數的數字(s:1621999487)或是十三位數的數字(ms:1621999487377)，可以透過[線上時間戳轉換器](https://tool.lu/timestamp/)得出代表的時間。


### 時區的轉換
世界各國位於地球不同位置上，，不同地區的人會有不同的地方時間，可以看[時區轉換器](https://tw.piliapp.com/time-now/converter/)

----
## golang 時間轉換
接著說明使用golang實現以上幾種常見的轉換，而2006-01-02 15:04:05-0700是一串go獨特神奇的對應順序。可以看[time/format.go](https://go.dev/src/time/format.go)

大致列出四種轉換:
1. 將時間戳轉換為時間
2. 將時間做格式化輸出，golang語法的時間輸出跟java比較不一樣。2006-01-02 15:04:05-0700 對應到	yyyy-MM-dd HH:mm:ss Z，請見[golang 與java time的對照表](https://programming.guide/go/format-parse-string-time-date-example.html)， `記憶順序有點像是06代表年，後面則是1,2,3,4,5,7`
3. 時區轉換: FixedZone(name,位移的秒數)，可以自訂時區命名信息，loc := time.FixedZone("UTC-8", -8 * 60 * 60)第二個參數轉移多少秒，可以改+8時區等等

4. 時區轉換: LoadLocation(name)，可以輸入空值，"UTC"，"Local"，或是時區的資料庫 EX: "Asia/Taipei"，命名使用的資料庫為[IANA Time Zone database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)，好處是不用自己輸入到底是＋8還加多久，知道時區命名就好，但是背後的定義還是會依下列順序去找尋對應資料：
	- ZONEINFO 環境變數所指定的zip文件
	- Unix系统中已经安装的
	- $GOROOT/lib/time/zoneinfo.zip，

>note warning %} 
因此如果在windows系统上，没有安装go語言環境，time.LoadLocation會失敗，建議用time.FixedZone。
 
另外在docker環境裡也要注意使用的image是否已經有包含這些資料，否則會出現unknown time zone XXXX的錯誤，解決方法需要加入以下設定
```
FROM alpine
...
COPY --from=0 /usr/local/go/lib/time/zoneinfo.zip /opt/zoneinfo.zip
ENV ZONEINFO /opt/zoneinfo.zip
OR
RUN apk --no-cache add tzdata
...
```

---

四種轉換時間格式範例程式:
```go diff
package main

import (
	"fmt"
	"time"
)

func main() {
	var Time int64
	Time = 1619083664867 //ms->2021-04-22 17:27:44

	t := time.Unix(0, Time*int64(time.Millisecond))
	fmt.Println("case1: timestamp to time:", t)
	
	
	layout1 := "2006-01-02T15:04:05"
	fmt.Println("case2: Formatlayout1:", t.Format(layout1))
	
	zone := time.FixedZone("", +0*60*60)
	newTimezone0 := t.In(zone)
	fmt.Println("case3: Timezone at +0:", newTimezone0.Format(layout1))

	// name := "America/New_York"
	name := "Asia/Taipei"
	t, err := TimeIn(t, name)
	if err != nil {
		fmt.Println("err:", err)
	}
	fmt.Println("case4: Timezone at Taipei:", t.Format(layout1))

}
func TimeIn(t time.Time, name string) (time.Time, error) {
	loc, err := time.LoadLocation(name)
	if err == nil {
		t = t.In(loc)
	}
	return t, err
}
```

轉換結果：
```
timestamp: 1619083664867
case1: timestamp to time: 2021-04-22 09:27:44.867 +0000 UTC
case2: Formatlayout1: 2021-04-22T09:27:44
case3: Timezone at +0: 2021-04-22T09:27:44
case4: Timezone at Taipei: 2021-04-22T17:27:44
```


----


## 網路參考文章

- [数据库存时间戳的好处](https://blog.csdn.net/qq_34908844/article/details/78817420)
- [time-unix examples](https://www.geeksforgeeks.org/time-unix-function-in-golang-with-examples/)
- [1milli->1000000 nano sec](https://www.translatorscafe.com/unit-converter/zh-CN/time/2-4/millisecond-nanosecond/)
- [Golang 時區 golang-timezone](https://jasonlee.xyz/golang-timezone/)
- [到底是 GMT+8 還是 UTC+8 ?](https://pansci.asia/archives/84978)
- [golang-TimeIn example](https://yourbasic.org/golang/time-change-convert-location-timezone/)
- [Golang神奇的2006-01-02 15:04:05](https://www.jianshu.com/p/c7f7fbb16932)
- [Go语言标准包解析Location](https://syaning.github.io/go-pkgs/time/#location)
- [Golang时区设置](https://studygolang.com/articles/13018)
- [解决容器运行 Go 代码 unknown time zone 的正确姿势](https://liqiang.io/post/unknonw-time-zone-solution-with-running-go-in-docker-6d0edc5d)



