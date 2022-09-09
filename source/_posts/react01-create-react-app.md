---
title: "[React 01] 初始開發環境設定"
tags:
  - react
  - vscode
  - lint
  - npm
categories:
  - Tech.
  - Web
  - front-end
  - react
date: 2020-05-16T15:42:53+08:00
---


{% note info %} 快速安裝 React 專案與建置開發環境，創建React App是創建單頁React應用程序的官方支持方式。 它提供了無需配置的現代化構建設置。 {% endnote %}



<!--more-->


#### 安裝node.js (npm)
- Node.js是能執行JavaScript 的執行環境，讓JS可以在伺服器(瀏覽器以外)運作
- npm（全稱 Node Package Manager，即「node包管理器」）是Node.js預設的、用JavaScript編寫的軟體套件管理系統

#### 使用 npm 安裝create-react-app
```bash
npm install -g create-react-app
/usr/local/bin/create-react-app -> /usr/local/lib/node_modules/create-react-app/index.js
+ create-react-app@3.4.1
~ create-react-app --version
3.4.1
```
-  -g 代表全局安裝
- create-react-app 是適合學習 React 的環境及單頁（single-page）應用程式，不需再安装或配置 Webpack 或 Babel 等工具， 它們是預先配置好並隐藏的
-  create-react-app --version 確認版本的指令- 


#### 使用create-react-app 建立專案
```bash
～create-react-app 01-create-react-app
Creating a new React app in /Users/xxx/front/01-create-react-app.
```

#### 啟動專案
```bash
npm start
```
就會看到一個網頁介面啟動囉！！！！！！

*註：當重新下載專案時需要先下npm install後才能npm start
*在本地可以看到node_modules的資料夾

#### create-react-app 內容
架構
```
README.md               
package.json //和設定打包工具(webpack)有關
node_modules            
public
package-lock.json       
src
```

- public/index.html
基本的HTML架構，內有
```html
"<div id="root"></div>"
```

- 而在/src/index.js 則有渲染DOM的程式碼
```
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```

#### 完成開發生成靜態與部署
```
npm run build
```
當編譯結束時，專案目錄底下會出現build資料夾，裡面的檔案就是所需要的靜態檔案(可以點開index.html試試看)，其他檔案在部署時不用上傳。

* 實作直接打開ＨＴＭＬ或是用live server都會一片空白？？ 但實際起python web server可以看到 (待釐清)

#### vscode 外掛
- ESlint 插件 -> 一個Javascript Linter，是一種靜態代碼分析工具，用於識別在JavaScript代碼中發現的有問題的模式，可以定義和加載自定義規則。ESLint涵蓋了代碼質量和編碼風格問題。
- JS JSX Snippets  插件  ->程式碼快速鍵

------------
#### 延伸閱讀 [wait]
[有看沒懂的npx方式](https://www.itread01.com/content/1544755994.html "有看沒懂的npx方式")

