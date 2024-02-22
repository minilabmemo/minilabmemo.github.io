---
title: "[react+scss] 快速在 create-react-app 中引用 scss 簡易開發"
tags:
  - scss
  - react
toc: true
categories:
  - - Frontend
    - css/html
date: 2023-11-07 10:27:52
---

<article class="message is-info"><div class="message-body">
之前在 React 專案中使用了 CSS-in-JS。CSS-in-JS 的寫法雖然能解決樣式污染問題，但它的寫法較為多變，需要一定的時間來熟練，且轉化 CSS 語法較為麻煩。後來發現在 React 專案中也常能看到 SCSS 的使用，而且只要套用 CSS 的邏輯即可。本篇紀錄在已有 React（Create React App）基礎上的啟用 SCSS 的方法。

</div></article>

<!--more-->

## 目錄 | Contents

<div class="my-toc">
<!-- toc -->
</div>

---

## React 專案

用以下指令快速建立 create-react-app 專案。

<div class="blockquote">
 <a href="https://create-react-app.dev/">create-react-app</a>  是由 Facebook 開發，透過執行一個命令來設定現代 Web 應用程式的 react 專案。
</div>

```
npx create-react-app my-app
cd my-app
npm start
```

## 建置 SCSS 環境

### 方法一：先寫 scss 轉成 css 引入

這是大部分任何專案都是用的方法，直接用 scss 寫法，然後用插件自動幫你轉 css，檔案引入就引入這個 css 檔案就好。

- 插件 裝 **Live Sass Compiler** 右下角有一個 watch css 按下去就可以監控到 scss 檔案幫你轉 css 了，如果有錯誤的話，轉換過程下方視窗會報錯。

### 方法二：直接引入 scss

這方法是 create-react-app 項目直接裝 `>npm i sass`，然後寫 scss 檔案，引入 scss 檔案即可，其實覺得很神奇，也不用 watch css 跟產生同樣的 css 檔案，查找上比較快速。\_[Styling React Using Sass](https://www.w3schools.com/react/react_sass_styling.asp)

```Import the Sass file
import './my-sass.scss';
const Header = () => {
  return (
    <>
      <h1>Hello Style!</h1>
    </>
  );
}
```

- 如果寫錯的話會有提示

```
Module build failed (from ./node_modules/sass-loader/dist/cjs.js):
SassError: Expected identifier.
   ╷
14 │   color: $123;
   │           ^
  src/layouts/header.scss 14:11  root stylesheet

webpack compiled with 1 error and 1 warning
```

## 檔案架構

網路上有很多可以參考的架構建議，你可以在 styles 裏面分檔案對應組件去放置，或者對應組件的地方自己放一份 scss 檔案，一開始我是用前者的方式，後來覺得要找跟創建一樣的資料夾太麻煩了，直接放在旁邊省事多了，原本的資料夾就放全域或基本的設置。

## SCSS 寫法

你可以參考這份教學文件：[Sass 官方指南](https://sass-lang.com/guide)，裡面有很詳細對應說明，以下簡單列出幾個用法並進行解釋。

### 變數 Variables

SCSS 中可以定義變量，使用 $name 來引用。雖然原本的 CSS 後來也引進了變數功能，可以視情況使用。

### 階層 Nesting

在 SCSS 中，你可以使用類似 HTML 結構的巢狀方式來定義樣式規則。這種方式更加清晰和易於維護，與原生 CSS 中用空格區分父子選擇器的寫法相比更加直觀。

### 分割

如果你想要將 SCSS 編譯成 CSS，但又不想產生大量的 CSS 文件，可以使用 \_xxx.scss 命名的方式。這類文件不會單獨產生 xxx.css 文件，而是被集合到統一的 SCSS 文件中。這種方式有助於組織和管理樣式文件，使得專案結構更加清晰。

## 插件工具

記錄其他有幫助開發的工具。

- [SCSS Everywhere](https://marketplace.visualstudio.com/items?itemName=gencer.html-slim-scss-css-class-completion)，當你定義好 scss 後，className 可以幫你自動補齊提示名稱，很多插件都有類似功能，而這個插件在 TSX 下也能正常使用，不用再來回複製，但要自己記憶比較好記的命名來做快捷輸入。

---

## 網路參考文章

<div class="ref">

- Photo by <a href="https://unsplash.com/@mediamodifier?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Mediamodifier</a> on <a href="https://unsplash.com/photos/nPZzZpWhPwg?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>

</div>
