---
title: "[React 筆記 01] 初始開發環境設定"
tags:
  - react
  - vscode
  - lint
  - npm
toc: true
categories:
  - [Frontend,react]
date: 2020-05-16T15:42:53+08:00
---



<article class="message is-info"><div class="message-body">
快速安裝 React 專案與建置開發環境，創建 React App 是創建單頁 React 應用程序的官方支持方式。它提供了無需配置的現代化構建設置。 

</div></article>

<!--more-->
## 目錄 | Contents
<div class="my-toc">
<!-- toc -->
</div>



#### 安裝 node.js (npm)
- Node.js 是能執行 JavaScript 的執行環境，讓 JS 可以在伺服器 (瀏覽器以外) 運作
- npm（全稱 Node Package Manager，即「node 包管理器」）是 Node.js 預設的、用 JavaScript 編寫的軟體套件管理系統

#### 使用 npm 安裝 create-react-app
```bash
npm install -g create-react-app
/usr/local/bin/create-react-app -> /usr/local/lib/node_modules/create-react-app/index.js
+ create-react-app@3.4.1
~ create-react-app --version
3.4.1
```
-  -g 代表全局安裝
- create-react-app 是適合學習 React 的環境及單頁（single-page）應用程式，不需再安装或配置 Webpack 或 Babel 等工具，它們是預先配置好並隐藏的
-  create-react-app --version 確認版本的指令 - 


#### 使用 create-react-app 建立專案
```bash
～create-react-app 01-create-react-app
Creating a new React app in /Users/xxx/front/01-create-react-app.
```

#### 啟動專案
```bash
npm start
```
就會看到一個網頁介面啟動囉！！！！！！

*註：當重新下載專案時需要先下 npm install 後才能 npm start
*在本地可以看到 node_modules 的資料夾

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
基本的 HTML 架構，內有
```html
"<div id="root"></div>"
```

- 而在/src/index.js 則有渲染 DOM 的程式碼
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
當編譯結束時，專案目錄底下會出現 build 資料夾，裡面的檔案就是所需要的靜態檔案 (可以點開 index.html 試試看)，其他檔案在部署時不用上傳。

* 實作直接打開 HTML 或是用 live server 都會一片空白？？但實際起 python web server 可以看到 (待釐清)

#### vscode 外掛
- ESlint 插件 -> 一個 Javascript Linter，是一種靜態代碼分析工具，用於識別在 JavaScript 代碼中發現的有問題的模式，可以定義和加載自定義規則。ESLint 涵蓋了代碼質量和編碼風格問題。
- JS JSX Snippets  插件  ->程式碼快速鍵

------------
#### 延伸閱讀 [wait]
[有看沒懂的 npx 方式](https://www.itread01.com/content/1544755994.html "有看沒懂的npx方式")

