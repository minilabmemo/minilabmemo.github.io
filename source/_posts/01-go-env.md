---
title: "[Go 01] 配置GO開發環境"
date: 2020-05-01 20:23:42
tags:
  - golang
  - vscode
categories:
  - Tech.
  - back-end
  - golang
---

{% cq %} 
# 什麼是Go
 {% endcq %}
 <blockquote class="blockquote-center">
 Go（又稱Golang）是Google開發的一種靜態強型別、編譯型、並發型，並具有垃圾回收功能且輕巧的程式語言．</blockquote>


# 透過三步驟設定完開發環境：
  1. 安裝官方 Go
  2. 配置開發 Go 所需要環境變數 
  3. 下載IDE「推薦Visual Studio Code加上插件」 開始寫Go

<!--more-->
------------

## Go的優點
以下截自:[Go適合做什麼？為何這麼多人偏愛Go語言？](https://www.mdeditor.tw/pl/2dVc/zh-tw)
並簡化列了以下幾點:
1. 學習曲線
因為Go語言容易學習，普通的大學生花一個星期就能寫出來可以上手的。
2. 高效率、簡單的併發
3. 出身名門、血統純正
出自Google公司，還能說什麼
4. 部署方便：二進位制檔案、Copy部署。
想部屬windows(exe)，或是linux可執行文件都很方便喔。
5. Go擁有強大的編譯檢查、嚴格的編碼規範和完整的軟體生命週期工具。


## 1.安裝 Go
go 網站https://golang.org/ 下載直接點擊安裝
預設會幫你安裝到/usr/local/go底下，這就是GOROOT位置
- 開啟終端機下指令確認安裝
```
➜  ~ go version
go version go1.14 darwin/amd64
➜  ~ which go  
/usr/local/go/bin/go

```
## 2.配置環境變數
### MAC安裝筆記
選擇的是用在使用者目錄下配置環境變數
- vi ~/.bash_profile
```
//輸入a編輯
export GOROOT="/usr/local/go"
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin 
export PATH=$PATH:$GOROOT/bin

//GOROOT表示GO安裝的目錄
//GOPATH是自訂想要放置程式的地方
//打完後esc輸入：wq存擋
```


- 執行 bash profile
	source ~/.bash_profile


## 3.IDE 安裝
3-1 下載 Visual Studio Code
3-2 打開 VScode 於 Extensions 安裝 Go (微軟官方維護) 外掛
 - Go 擴充功能整合了多種 Go 工具，例如 gocode(代碼自動補全), golint(代碼規範檢查)，goreturns(格式工具Format Tool) 等，可以查看https://github.com/golang/vscode-go/blob/master/docs/tools.md(有些有不同選擇，預設工具可以在設定裡改)
 - 如果沒有安裝對應的工具，就會在編譯.go文件時跳出提示，Analysis Tools Missing ，此時可以按下 Command + Shift + p 呼叫命令列視窗，輸入 Go: Install/Update tools 安裝/更新所有的工具解決此問題。
  - 如遇上安裝問題，也有文章推薦可直接進行3-3步驟

3-3 打開終端機執行下列指令來安裝依賴包以下工具:


```bash
go get -u -v github.com/ramya-rao-a/go-outline
go get -u -v github.com/acroca/go-symbols
go get -u -v github.com/mdempsky/gocode
go get -u -v github.com/rogpeppe/godef
go get -u -v golang.org/x/tools/cmd/godoc
go get -u -v github.com/zmb3/gogetdoc
go get -u -v golang.org/x/lint/golint
go get -u -v github.com/fatih/gomodifytags
go get -u -v golang.org/x/tools/cmd/gorename
go get -u -v sourcegraph.com/sqs/goreturns
go get -u -v golang.org/x/tools/cmd/goimports
go get -u -v github.com/cweill/gotests/...
go get -u -v golang.org/x/tools/cmd/guru
go get -u -v github.com/josharian/impl
go get -u -v github.com/haya14busa/goplay/cmd/goplay
go get -u -v github.com/uudashr/gopkgs/cmd/gopkgs
go get -u -v github.com/davidrjenni/reftools/cmd/fillstruct
```
> 配置好後在編輯ＧＯ語言就會發現有很多貼心的提示 ，同時也會出現在ＩＤ內的problems清單裡，可以進一步修改程式語法，真的是超級方便的．

- 補充：以下是相關工具的說明
|工具   |  說明 |
| ------------ | ------------ |
| dlv.exe	go  | 語言調適工具  |
| gocode.exe	go  |  語言检查，自动补全 |
| godef.exe 	go  |  語言定义和引用的跳转 |
| golint.exe 	go  | 語言规范检查  |
| go-outline.exe  |  用于在Go源文件中提取JSON形式声明的简单工具 |
|  gopkgs.exe |   	快速列出可用包的工具 |
| gorename.exe  |  在Go源代码中执行标识符的精确类型安全重命名 |
|  goreturns.exe | 类似fmt和import的工具，使用零值填充Go返回语句以匹配func返回类  |
| go-symbols.exe  |  	从go源码树中提取JSON形式的包符号的工具  |




{% note class_name %} # 參考文章 {% endnote %}
windows 安裝Go
- [[Go] Go 語言於 Windows 上之安裝與環境設定](https://oranwind.org/go-go-yu-yan-yu-windows-shang-zhi-an-zhuang-yu-huan-jing-she-ding/ "[Go] Go 語言於 Windows 上之安裝與環境設定") 
- [用vscode开发调试golang超简单教程](https://blog.csdn.net/v6543210/article/details/84504460)

Ｍac 安裝Go
- [Mac上Go環境和VS Code的正確安裝與配置方法](https://codertw.com/%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC/391186/) 

IDE : VScode
- [[Go] 使用 Visual Studio Code 上建置 Go 開發環境](https://oranwind.org/go-ide-visual-studio-code/ "[Go] 使用 Visual Studio Code 上建置 Go 開發環境") 
