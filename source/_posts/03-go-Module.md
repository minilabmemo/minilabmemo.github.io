---
title: "[Go 03] 包管理與模組(Module)相關"
tags:
  - golang
categories:
  - Tech.
  - back-end
  - golang
date: 2021-02-13 15:09:47
---

{% note info %} Go 包管理與模組相關 {% endnote %}



<!--more-->


### import


- "time" imported but not used-compiler
不允許引入未使用包，vscode 儲存，工具會自動幫忙移除。
```
如果要引用沒有用到的import，則要使用底線(_)
import (
    _ "github.com/go-sql-driver/mysql"
)
```
- import cycle not allowed
執行後會出現相依錯誤
	延伸閱讀: [Golang中解决"import cycle not allowed"的2种方法](https://studygolang.com/articles/14152)

### Go Module
Go 1.11 之後提供go modules 可以不需要把專案程式碼放在 $GOPATH/src 中開發，此外還能管理套件相依性。

- go mod init
建立一個 go.mod，裡面會記錄import版本
- go get xxxxxx
go get 命令可以借助代码管理工具通过远程拉取或更新代码包及其依赖包，并自动完成编译和安装。
 預設會下載最新，@version 可以指定版號。
 常見flag使用: 
	-d	让命令程序只执行下载动作，而不执行安装动作。
	-u	让命令利用网络来更新已有代码包及其依赖包。默认情况下，该命令只会从网络上下载本地不存在的代码包，而不会更新已有的代码包。
	-v 显示执行的命令

- go mod tidy
移除不需要的import
- go mod download
可以下载所需要的依赖，或是go build也會自動將 pkg 下載到 GOPATH/pkg/mod 內


延伸閱讀: [go get命令——一键获取代码、编译并安装](http://c.biancheng.net/view/123.html)

### Go 相依圖
go mod graph 可视化——gmchart
延伸閱讀: https://segmentfault.com/a/1190000038897207