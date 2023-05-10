---
title: "[chrome-extension] 自己動手寫一個 chrome 擴充 (一次搜尋特定網站資源)"
tags:
  - chrome-extension
  - tool 
cover: /img/posts/chrome-ext.jpg
thumbnail:  /img/posts/chrome-ext.jpg
toc: true
categories:
  - - 技術工具
    - chrome-extension
date: 2023-05-05 15:11:30
---

{% raw %}
<article class="message is-info"><div class="message-body">
chrome-extension 是一個可以在 chrome 瀏覽器應用商店安裝的擴充功能，可以用網頁技術（HTML,CSS,JS）修改與增強瀏覽器，例如操控書籤、背景、開新分頁、右鍵選單等等，這一篇來動手學習怎麼寫一個擴充功能，並以一次搜尋特定網站為範例。

</div></article>{% endraw %}

<!--more-->
## 目錄 | Contents
<div class="my-toc">
<!-- toc -->
</div>


## 程式架構說明
GoogleChrome的github有提供幾種程式碼範例，[chrome-extensions-samples](https://github.com/GoogleChrome/chrome-extensions-samples/tree/main/functional-samples)，裡面最主要都會有一個 manifest.json 用來定義 插件的名稱,版本,描述, 以及延伸行為會使用到的 html ,js 與icon等等檔案，舉例hello-world如下： 

```json tutorial.hello-world/manifest.json
{
  "name": "Hello Extensions",
  "description": "Base Level Extension",
  "version": "1.0",
  "manifest_version": 3,
  "action": {
    "default_popup": "hello.html",
    "default_icon": "hello_extensions.png"
  }
}
```

### API reference
這份 json中 定義的 Manifest Keys 需要對照官方定義的[API reference](https://developer.chrome.com/docs/extensions/reference/)，需要注意 manifest_version 版本，網路上大部分都是v2版本的對照key寫法，上述範例是 V3 寫法，對照上需要注意避免元件出錯。

- 以下列出幾種 Manifest Keys 說明：
  - [action](https://developer.chrome.com/docs/extensions/reference/action/) 是用來控制 Chrome 用戶界面中擴展程序的工具欄按鈕，根據說明如下：
```
{
  "name": "Action Extension",
  ...
  "action": {
    "default_icon": {              // optional
      "16": "images/icon16.png",   // optional
      "24": "images/icon24.png",   // optional
      "32": "images/icon32.png"    // optional
    },
    "default_title": "Click Me",   // optional, shown in tooltip
    "default_popup": "popup.html"  // optional
  },
  ...
}

```
  - [contextMenus](https://developer.chrome.com/docs/extensions/reference/contextMenus/) 控制右鍵選單
  - [tab](https://developer.chrome.com/docs/extensions/reference/tabs/) 控制瀏覽器分頁
  - [storage](https://developer.chrome.com/docs/extensions/reference/storage/)使用來存儲、檢索和跟踪對用戶數據的更改。
  - [runtime](https://developer.chrome.com/docs/extensions/reference/runtime/) 消息傳遞，可以使用這些方法和事件與其他擴展通信：connect()、onConnect、onConnectExternal、sendMessage()、onMessage和onMessageExternal。



### 本地載入開發
將上述程式碼範例從github下載到本地端，依下列步驟載入程式
  - 打開自訂與管理->更多工具->擴充功能 或者 Open [chrome://extensions](chrome://extensions)
  - 把開發者模式打開。
  - 將範例資料夾丟入，如果格式正確就會成功載入出現該擴充。
  <img src="/images/step_import.png" width="100%" />
  - 網址列右方的擴充按鈕就會出現相關的圖示以及點擊後的彈出視窗html。（以 hello 範例為例，你可以自行載入不同擴充看看效果）
   <img src="/images/step_popup.png" width="100%" />




---------------------------------


## 動手更改程式碼
接下來自己寫一個擴充元件，加入自己想要控制的功能。

### 發想1: 一個簡單可實現的搜尋功能

<div class="notification is-info">
不知道你有沒有常常在閱讀某些網頁時，對某個主題感興趣需要另外去搜尋的時候，google其實有在右鍵中實現選取文字google搜尋，但最近我常常想要找尋一些書籍是否有在公共圖書館的電子書中，用google搜尋其實不太能快速找尋，於是我會一個又一個開啟所有我需要的電子書網站，然後一個個的輸入關鍵字按下點擊找尋，雖然是個簡單的動作，但還是花了不少時間，而google擴充功能也可以支援右鍵擴充的按鈕，就來實現看看．

</div>

#### 擴充功能 : 尋找台南圖書館線上資源
這是台南圖書館提供的[電子書資源網站列表](https://www.tnpl.tn.edu.tw/u4644318637373758255/s1)，這邊就挑選其中 HyRead ebook X 台南圖書館/台灣雲端書庫/udn讀書館(臺南分區資源中心)/台灣雲端書庫/國立公共資訊圖書館電子書服務平台 等網站來做一次開啟．

##### 功能1. 實現右鍵出現選單 contextMenus

  - 新增背景執行程式與權限 
```diff manifest.json
 "background": {
+    "service_worker": "background.js"
  },
  "permissions": [
+    "contextMenus"
  ],
```

  - 加入右鍵選單 與點選後要做的事情
```diff background.js
// title 裏面加上 %s 可以很神奇的出現你選擇的內容
function setupContextMenu() {
+  chrome.contextMenus.create({
+    id: 'find-ebook',
+    title: `find e-Book resources %s`,
+    contexts: ['selection']
+  });
}

// runtime.onInstalled 去執行 setupContextMenu
+ chrome.runtime.onInstalled.addListener(() => {
+   setupContextMenu();
+ });
 
+ chrome.contextMenus.onClicked.addListener((data) => {

  //當選單被按下要做的事 這邊要做的是新增分頁
+  chrome.tabs.create({
+    url: `https://tnml.ebook.hyread.com.tw/searchList.jsp?search_field=FullText&search_input=${data.selectionText}`
+  })

+ });

```
  - 其中 url 的部分要先去你要搜尋的網站，去觀察找出 keyword 要取代的部分


<article class="message is-info"><div class="message-body">
近一步加入自己想要開啟的特定網站列表，這樣就完成了，如下顯示：
</div></article>
<img src="https://github.com/minilabmemo/chrome-ext-find-ebook/raw/master/chrome-right-ebook.png" width="100%" />

------

##### 功能2. popup 顯示條件搜尋


根據前述的 action -> popup.html , popup.html 就可以加入你希望呈現的頁面內容，popup.js 決定操控的動作與前述的chrome API 互動即可．


<article class="message is-info"><div class="message-body">
完成如下顯示，功能效果與前述相同，只是多加了搜尋設定：

</div></article>
<img src="https://github.com/minilabmemo/chrome-ext-find-ebook/raw/master/chrome-search-ebook.png" width="100%" />

- 延伸：
  - 如果要記住設定可以與 storage API 互動
  - 設定要能同步傳到右鍵開啟選項則可以使用 runtime API 消息傳遞傳送，

--------------

###  發想２：護眼功能
<div class="notification is-info">
上一功能知道如何開啟新分頁的方式，其實應該也可以做提醒通知，自己其實常常寫程式一寫就是兩三個小時，常常忘了讓眼睛休息一下，雖然有用過番茄鐘，但找到的應用是背景執行，還是會忽略它的存在，想要的功能是可以在瀏覽器上直接跳出通知提醒我休息了．

</div>

但這項功能搜尋後發現已經有人做過了，完全符合我的需求，而且有些會去更改網頁底色，直接推薦這些元件出來，雖然我覺得應該可以參考再整合，之後有時間或更大的需求再來做做看了：
  - [eyeCare - Protect your vision](https://chrome.google.com/webstore/detail/eyecare-protect-your-visi/eeeningnfkaonkonalpcicgemnnijjhn) 可以設定休息時間還有音效，跳出通知也有簡單的護眼訊息
  - 深色模式，這個在[chrome 應用商店](https://chrome.google.com/webstore/category/extensions?hl=zh-TW) 搜尋可以發現很多，會幫你把網頁改成深色底色。






------------
## 網路參考文章

<div class="notification is-warning">
本篇文章內容參考如下
</div>


- Photo by <a href="https://unsplash.com/@mediamodifier?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Mediamodifier</a> on <a href="https://unsplash.com/photos/nPZzZpWhPwg?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  

------------
