---
title: "[Go] 性能/品質檢測"
tags:
  - test
  - golang
  - cleanCode
categories:
  - Tech.
  - back-end
  - golang
date: 2020-09-18 15:03:37
---

 <blockquote class="blockquote-center">
 當開發golang程式完成後，其實有一些工具可以查看自己的程式效能，是否有些地方佔了太大的資訊進而改進，另外也可以
 透過品質檢測工具去看修改建議；最後，如果有撰寫測試案例的話，也有工具可以產生測試報告，確認測試案例涵蓋了程式多少百分比，還有沒被寫到的地方也可以透過報告顯示出來．</blockquote>


本章介紹:
- 性能分析工具-pprof 查看CPU/memory 等的瓶頸
- 檢視go的品質與建議-gosec


<!--more-->


## 性能分析工具-pprof

先在程式碼插入以下程式後執行。<br>
```go
import _ "net/http/pprof"
func main() {
	go func() {
		http.ListenAndServe("0.0.0.0:8080", nil)
	}()
}
```
開啟http://localhost:8080/debug/pprof/
可以看到一個簡單的分析數字

### go tool 看記憶體(heap)
透過以下指令可以看到佔記憶體的前幾名
```
$go tool pprof  http://127.0.0.1:8080/debug/pprof/heap<br>

-> 輸入top<br>
-> 輸入web可以看到圖形<br>

(pprof) top<br>

Showing nodes accounting for 1.50MB, 100% of 1.50MB total
      flat  flat%   sum%        cum   cum%<br>
    1.50MB   100%   100%     1.50MB   100%  golang.org/x/net/webdav.(*memFile).Write<br>
         0     0%   100%     1.50MB   100%  github.com/swaggo/files.init.8<br>
```

### go tool 看CPU(profile)
而以下幾令則是幾秒內的ＣＰＵ計算
```
go tool pprof http://localhost:6060/debug/pprof/profile?seconds=60<br>
```

### 網頁版查看 圖表
以上兩種指令其實可以透過以下指令可以開啟一個網頁更容易看到資料的圖表呈現
```
go tool pprof -http=":9099" -seconds=30 http://localhost:8080/debug/pprof/profile
go tool pprof -http=":9099"  http://localhost:8088/debug/pprof/heap
go tool pprof -http=":9099"  http://localhost:8088/debug/pprof/goroutine

```

參考文章:<br>
- [golang pprof](https://lrita.github.io/2017/05/26/golang-memory-pprof/ "golang pprof")<br>
- [使用多年的go pprof检查内存泄漏的方法居然是错的?!](https://colobu.com/2019/08/20/use-pprof-to-compare-go-memory-usage/ "使用多年的go pprof检查内存泄漏的方法居然是错的?!")<br>


-------------------------------

## 檢視go的品質與建議
1.先下載 go set<br>
go get github.com/securego/gosec/cmd/gosec@v2.2.0
<br>

2.輸出報告(可選格式)<br>
```
gosec -fmt=json -out=results.json ./...<br>
gosec -fmt=html -out=results.html ./...<br> 
注意是*三個點
```
- 然後打開ＨＴＭＬ檔案就可以看到程式品質分析報告了
<img src="/images/post/gosec.png" width="500px" />

- 像是以上這條處理檔案位置時，path應該清理處理過以避免輸入異常









{% note class_name %}  ## 延伸文章 {% endnote %}

|  來源 |  摘要 |
| ------------ | ------------ |
|[新手问题 golang内存检测工具](https://gocn.vip/topics/250 "新手问题 golang内存检测工具")   | 生产环境中使用 pprof 时会遇到一些问题  |
|  [go pprof与线上事故：一次成功的定位与失败的复现](https://www.jianshu.com/p/21b53f061a0a "go pprof与线上事故：一次成功的定位与失败的复现") |  很多小伙伴担心线上使用pprof会影响性能，担心安全问题。这个在我看来利大于弊，当服务出现问题的时候，资源占用多一点点与能够解决问题相比微不足道，当服务没有问题的时候使用pprof那更没有问题了~ |
| [Golang 語言的單元測試和性能測試(也叫 壓力測試)](https://www.itdaan.com/tw/c8c0ed4d4e43c2a0d6a2917232d6499b "Golang 語言的單元測試和性能測試(也叫 壓力測試)")  |  （高級測試技術） |
|  https://etcnotes.com/posts/pprof/ | 生成圖   |