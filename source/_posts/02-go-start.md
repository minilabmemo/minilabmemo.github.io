---
title: "[Go 02] GO 新手上路與概念筆記"
tags:
  - golang
categories:
  - Tech.
  - back-end
  - golang
date: 2020-05-01 21:16:32
---


<!--more-->

{% note info %}藍色區塊{% endnote %}


## 開始寫GO

 分享自己初學GO時看的教學文章，安裝完GO環境之後，就可以撰寫自己第一支GO的程式了，網路上的系列說明很多很詳細，就不重複撰文了，以下則是自己收藏很有用的網路文章。

- 教你撰寫第一隻 Go
  - [Go的中文指南](https://tour.go-zh.org/list) (Go的中文指南，只有簡體)
  - [the-little-go-book](https://kevingo.github.io/the-little-go-book/ "the-little-go-book")
  - [Golang — GOROOT、GOPATH、Go-Modules-三者的關係介紹](https://medium.com/%E4%BC%81%E9%B5%9D%E4%B9%9F%E6%87%82%E7%A8%8B%E5%BC%8F%E8%A8%AD%E8%A8%88/golang-goroot-gopath-go-modules-%E4%B8%89%E8%80%85%E7%9A%84%E9%97%9C%E4%BF%82%E4%BB%8B%E7%B4%B9-d17481d7a655)
  - [從商業利益看 Go 程式語言](https://blog.wu-boy.com/2017/01/business-benefits-of-go/)
- 進階 go 整理教學
  - [[筆記] Golang 進階](https://kennyliblog.nctu.me/2019/08/20/Golang-advanced/#%E7%AD%86%E8%A8%98-Golang-%E9%80%B2%E9%9A%8E "[筆記] Golang 進階")

## 個人筆記整理

### 筆記 Go 的基本类型
>bool,string
int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr
byte // uint8 的别名
rune // int32 的别名// 表示一个 Unicode 码点
float32 float64
complex64 complex128
https://tour.go-zh.org/basics/11

### 匿名欄位
```go
type User struct {
	Name string
}
type Person struct {
	User //匿名欄位
	ID   string
}

  ss := Person{User: User{Name: "123"}, ID: "123"}
	fmt.Print("ss", ss.Name)
```


###  筆記 Go的參數傳遞
傳值的意思是：函式傳遞的總是原來這個東西的一個副本，一副拷貝。
- pass by value
  嚴格來說，Go只有傳植方式，會複製一個新的變數，且分配新的memory位址。
pass by pointer (或稱 called by reference，但其實不是)
  指標方式則會複製一個新的指標，但指向的memeory位址是一樣的，但是是兩個不同的指標。
1. 通常預期參數被修改，應傳指標。
2. 在go裡pass by value開銷很小
3. 迷思:Map/chan等其實是指標型別，因此會被修改，是種引用型別(reference types)[不是指call by reference]，仍是pass by value

出自以下參考文章:

- [golang-pass-by-pointer-vs-pass-by-value](https://goinbigdata.com/golang-pass-by-pointer-vs-pass-by-value/)
- [there-is-no-pass-by-reference-in-go](https://dave.cheney.net/2017/04/29/there-is-no-pass-by-reference-in-go)
- [《Golang 入門系列七》Go語言引數傳遞是傳值還是傳引用](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/74367/)
Go語言中所有的傳參都是值傳遞（傳值），都是一個副本，一個拷貝。因為拷貝的內容有時候是非引用型別（int、string、struct等這些），這樣就在函式中就無法修改原內容資料；有的是引用型別（指標、map、slice、chan等這些），這樣就可以修改原內容資料。"


###  筆記 理解 Go 语言中的方法和接收者

- 值接收者，是一个副本，方法内部無法對其真正的接收者做更改；
- 指针接收者，是接收者的引用，對這個引用的修改可以影響真正的接收者。

[理解 Go 语言中的方法和接收者](https://segmentfault.com/a/1190000009643429)


### 筆記 go中的資料結構介面-interface

[go中的資料結構介面-interface](https://www.itread01.com/content/1574082186.html)

[interface gitbook](https://willh.gitbook.io/build-web-application-with-golang-zhtw/02.0/02.6)


### 筆記 搞定Go Mock 單元測試

[搞定Go單元測試（二）——mock框架(gomock)](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/695780/)

