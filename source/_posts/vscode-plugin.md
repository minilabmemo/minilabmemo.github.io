---
title: '[✍持續更新中] [vscode] 使用與插件分享'
tags:
  - vscode
  - IDE
categories:
  - Tech.
  - tool
date: 2020-09-18 18:37:37
---

{% cq %}

# 什麼是 vscode

{% endcq %}

 <blockquote class="blockquote-center">
 Visual Studio Code（簡稱vscode）是一個由微軟開發，同時支援Windows 、 Linux和macOS等操作系統的免費程式碼編輯器，它支援測試，並內建了Git 版本控制功能，同時也具有開發環境功能，例如代碼補全、代碼片段和代碼重構等。 （維基百科）</blockquote>

> 本篇記錄自身常用設定與插件紀錄．[✍持續更新中]
<!--more-->

## 開啟命令面板

F1 或 Ctrl+Shift+P 開啟命令面板，再輸入想使用什麼內容，結合後續說明使用．

## Git 版本控制

其實在 vscode 中操作 Git 真的非常方便，以下動作都是自己摸索就找到對應功能了，
直接紀錄幾個常用動作．

- commit change File
  切換到 git 頁籤->會出現你有更動過的檔案，點擊可以看到差異點
  ->按下+ 可以新增至 change 列表->上方輸入 commit Message->上方有一個勾勾按下及 commit

- 上傳 change File Push
  點擊左下角分支圖右方會有上傳按鈕

- 新增 branch
  點擊左下角分支圖->Create branch ->輸入名稱

- 切換 branch
  點擊左下角分支圖->選擇分支

- 刪除分支
  Ctrl+shift+p->git delete branch->選擇分支

## gitmoji
在git提交上加入表情符號
[gitmoji](https://marketplace.visualstudio.com/items?itemName=Vtrois.gitmoji-vscode)

## Code Snippet

這個是 vscode 內建就有的程式碼內建設定，

## 開啟終端機

你不用跳到 VS Code 工具外來執行，直接按下【Ctrl+、】即可開啟終端機畫面，。
Ctrl+` Show integrated terminal

## 安裝插件

側邊欄中有一項 Extensions 可以在這邊搜尋插件與插件使用介紹．

### 代碼格式化

- prettier - code formatter
- ESLint

### Path Intellisense

自動補齊程式中的路徑和文件名。

### Task Kill
有時候程式發生意外終止或是不小心關閉，會需要使用終端機查出進程ＩＤ並終止．
這個插件很好用，安裝完後 cmd+shift+p 可以叫出對話 輸入task kill...by port 再輸入要砍的網路 port即可．

### TODO TREE
有時候開發過程中有未能完成或是要稍後完成的地方，可以加上TODO/FIXME等註解．
這一個插件安裝完之後，側邊會出現新的icon，點擊後可以快速找出這些註解的地方．

### Quokka.js (沒用過先記著)

Quokka.js 会在你输入时自动计算结果，并在 IDE 中打印结果。

### Auto rename Tag


### Css-in-js
可以透過指令將 CSS 選取後切換 css & css-in-js 寫法，不用再自己改半天啦！！

### vscode-styled-components
可以自動完成在css-in-js區塊裡面的css補全提示．


### Git Graph

可以看到分支圖

### 後端語言相關 Go 套件

#### 新增 task 設定

F1 或 Ctrl+Shift+P 開啟命令面板

```
tasks.json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "echo",
            "type": "shell",
            "command": "echo Hello",
            "problemMatcher": []
        },
        {
            "label": "rungo",
            "type": "shell",
            "command": "go",
            "options": {
                "cwd": "${workspaceRoot}\\",
                "env": {
                    "GOPATH": "D:\\go"
                }
            },
            "args": [
                "run",
                "main.go"
            ],
            "problemMatcher": []
        }
    ]
}
```

### 新增 debug 設定

```
D:\go\src\xxx\.vscode\launch.json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Launch",
            "type": "go",
            "request": "launch",
            "mode": "auto",
            "program": "${fileDirname}",
            "env": {},
            "args": []
        },
        {
            "name": "LaunchRoot",
            "type": "go",
            "request": "launch",
            "mode": "debug",
            "program": "${workspaceRoot}",
            "env": {},
            "args": []
        }
    ]
}
```

-

# 客製化設定

根據插件會有對應的設定
(快速鍵 Command+ ,) 開啟 settings.json 使用者設定檔

### files

```
 "files.autoSave": "onFocusChange", 當焦點移開自動儲存
  "files.associations": {
    "*.js": "javascriptreact" 新增檔案後綴連接的檔案類型 （React用）
  },
```

### editor

自動存檔格式化與更改預設格式化工具

```
"editor.tabCompletion": "on",
//type a snippet prefix (trigger text), and press Tab to insert a snippet.
"editor.formatOnSave": true,
"editor.defaultFormatter": "esbenp.prettier-vscode"
```

### React JSX 自動格式化設定

搭配 editor 根據檔案格式做設定

```

  "[javascriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "eslint.codeAction.showDocumentation": {
    "enable": true
  },

```

### React Hooks Snippets
React Hooks Snippets - React Hooks程式碼區段快速產生


### prettier

```
'prettier.singleQuote': true,
使用單引號，這個打開，格式化會幫你把""變成單引號
'prettier.semi': false,
結束是否加分號
```

{% note class_name %} ## 網路參考文章 {% endnote %}

| 連結 | 摘要 |
| ----------- | --------|
| [偏好的 Visual Studio Code 設定檔](https://blog.poychang.net/my-vscode-config)                                                 | 非常詳細   |
| [vscode 如何自動格式化代碼？](https://kknews.cc/zh-tw/code/2kj8z9y.html 'vscode 如何自動格式化代碼？')    | 編輯器默認的格式化工具 |
| [How do I enable automatic prettier formatting for .jsx files in VS Code?](https://stackoverflow.com/questions/62380051/how-do-i-enable-automatic-prettier-formatting-for-jsx-files-in-vs-code 'How do I enable automatic prettier formatting for .jsx files in VS Code?') | each file type has to be individually<br>Note javascriptreact as the identifier for JSX |
| [VScode Golang 编译任务 Task.json](https://studygolang.com/articles/20742)                                                                                                                                                                                                 | 在終端機的指令可以透過 task 安裝                                                        |
| [Visual Studio Code 極速上手指南](http://blog.tonycube.com/2018/11/visual-studio-code.html)                     |  |
| [vscode 插件推荐 todo-tree](https://zhuanlan.zhihu.com/p/63303926)                                                                                                                              |                                                                                         |
| [15 款好用的 VS Code 插件](https://www.infoq.cn/article/02mq2EZIhAaRuPk2Z8id)                                                                                                                                                                                              |                                                                                         |
| [Visual Studio Code 之常備快捷鍵](https://www.itread01.com/content/1548344894.html)                                                                                                                                                                                        | Visual Studio Code 之常備快捷鍵                                                         |
