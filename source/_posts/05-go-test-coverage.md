---
title: "[Go 06] 寫測試並產出一目瞭然的網頁版覆蓋率報告 再也不用怕遺漏"
tags:
  - golang
	- vscode
categories:
  - [Backend,golang]
date: 2020-05-09T00:02:42+08:00
---

# 本章介紹：

- 為上一篇 Gin 框架的 User & PostName func.寫個簡單測試
- 跑測試並瞭解 coverage 覆蓋率，產生測試報告(20210702 有新增vsocde用法補充)

<!--more-->

說明：新建一個檔案ＸＸ\_test.go，並為 func 取名 Test ＸＸＸ(t \*testing.T)

```go
//測試打GET /api/v1/user 去跑User() 會拿到“ＯＫ”
func TestUser(t *testing.T) {
	engine := gin.New()
	initRoutes(engine)//你的路由邏輯
	uri := "/api/v1/user"

	body := Get(uri, engine)
	fmt.Printf("response:%v\n", string(body))
	if !reflect.DeepEqual(string(body), "\"OK\"") {
		//利用 t.Errorf 觸發錯誤
		t.Errorf("Get user name need to be ok!")
	}
}
//同理測試 Post 去跑PostName() 會拿到回復的名字等於打的內容（body）
func TestPostName(t *testing.T) {
	engine := gin.New()
	initRoutes(engine) 
	uri := "/api/v1/user"
	user := structs.User{Name: "user", Age: 18}
	body := PostUser(uri, user, engine)
	fmt.Printf("response:%v\n", string(body))

	response := &structs.User{}
	if err := json.Unmarshal(body, response); err != nil {
		t.Errorf("Unmarshal，err:%v\n", err)
	}
	if response.Name != "user" {
		t.Errorf("response different，user:%v\n", response.Name)
	}
}

// GET HTTP Request
func Get(uri string, router *gin.Engine) []byte {
	req := httptest.NewRequest("GET", uri, nil)
	w := httptest.NewRecorder()

	router.ServeHTTP(w, req)
	result := w.Result()
	defer result.Body.Close()
	body, _ := ioutil.ReadAll(result.Body)
	return body
}
// POST HTTP Request
func PostUser(uri string, param structs.User, router *gin.Engine) []byte {
	jsonByte, _ := json.Marshal(param)
	req := httptest.NewRequest("POST", uri, bytes.NewReader(jsonByte))
	w := httptest.NewRecorder()
	router.ServeHTTP(w, req)
	result := w.Result()
	defer result.Body.Close()
	body, _ := ioutil.ReadAll(result.Body)
	return body
}


```

#### 測試單一個 function

如果用 VS code，可以在上方看到 run test | debug test 按鈕可以按，十分方便

#### 測試單一檔案內所有測試

cover 有帶的話會算出覆蓋率，並要在該目錄下去執行，這邊跑出來結果大約有 57.1% 的覆蓋

```bash
$go test -v -cover=true user_test.go user.go
PASS
coverage: 57.1% of statements
ok      command-line-arguments  0.297s  coverage: 57.1% of statements
```

#### 測試整個專案

```bash
如果是在main的目錄要往子目錄找
＄go test -v ./…
```

----
#### 產生測試覆蓋(coverage)報表-gotest


```bash
go test -coverprofile=coverage.out ./...
用gool tool
go tool cover -func=coverage.out
go tool cover -html=coverage.out
```

這個真的很酷，用網頁產生報告，而且非常視覺化，
可以看出剛剛沒有寫到的 UserName()測試為紅色
![](/images/post/test_coverage.png)

---

>note warning %} 20210702 補充 :
其實後來發現vscode在跑完package test 後，右邊側欄就會跑出覆蓋的條線了
如果只是要在測試時查看可以直接用ＩＤＥ的便利性即可．


![vscode](/images/post/test_coverage_vscode.png)


當然寫測試還有很多判斷的條件等等，是否等於，是否不等於，各種輸出可能．

寫完之後，可以為下一次更動後確認邏輯，看跑過測試真的很有療癒的感覺！！！:grin:

---

覺得有疑問嗎？可以再進一步看看參考文章：  
- [基于 golang gin 框架的单元测试](https://studygolang.com/articles/11836 "基于golang gin框架的单元测试")
- [go test 提示 no test files](https://www.sunzhongwei.com/go-test-suggests-no-test-files "go test 提示 no test files")<br>
- [Go: tests with HTML coverage report](https://medium.com/@kenanbek/go-tests-with-html-coverage-report-f977da09552d "Go: tests with HTML coverage report")<br>
- [使用 Go 进行单元测试](https://juejin.im/post/5dc37eb8e51d452a066999bf "使用 Go 进行单元测试")<br>


---



