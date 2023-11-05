---
title: '[chrome-extension] 自己動手寫一個 chrome 擴充 (一次搜尋電子書網站)'
tags:
  - chrome-extension
  - tool
cover: /img/posts/chrome-ext.jpg
thumbnail: /img/posts/chrome-ext.jpg
toc: true
categories:
  - - 技術工具
    - chrome-extension
date: 2023-05-05 15:11:30
---

<article class="message is-info"><div class="message-body">
Chrome 擴充功能是一種可以在 Chrome 瀏覽器應用商店安裝的擴充程式。透過網頁技術（HTML、CSS、JS），它能夠修改和增強瀏覽器的功能，例如書籤管理、自訂背景、開啟新分頁、右鍵選單等等。這篇文章將引導您進行一個實際範例，教您如何撰寫一個擴充功能，並以搜尋特定網站為例子

</div></article>

<!--more-->

## 目錄 | Contents

<div class="my-toc" >
<!-- toc -->
</div>

## 程式架構說明

在 Google Chrome 的 GitHub 存儲庫中，有提供多種程式碼範例，位置在[chrome-extensions-samples](https://github.com/GoogleChrome/chrome-extensions-samples/tree/main/functional-samples)。這些範例包含了一個 manifest.json 檔案，用於定義擴充功能的名稱、版本、描述，以及擴充功能所需的 HTML、JS 和圖示等檔案。以下是 hello-world 的範例：

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

這份 JSON 文件中所定義的 Manifest Keys 需要參考官方的[API 參考文件](https://developer.chrome.com/docs/extensions/reference/)來確保正確性。請留意 manifest_version 版本的選擇，因為網路上大部分資源是針對 V2 版本的 Manifest Keys 寫法。上述範例是 V3 版本的寫法，所以在對照時需要特別注意，以避免元件出錯。

- 以下列出幾種 Manifest Keys 說明：
  - [action](https://developer.chrome.com/docs/extensions/reference/action/) 內容可用來控制 Chrome 用戶界面中的工具欄按鈕：

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
- [runtime](https://developer.chrome.com/docs/extensions/reference/runtime/) 消息傳遞，可以使用這些方法和事件與其他擴展通信：connect()、onConnect、onConnectExternal、sendMessage()、onMessage 和 onMessageExternal。

### 本地載入開發

將上述程式碼範例從 github 下載到本地端，依下列步驟載入程式

- 打開自訂與管理->更多工具->擴充功能 或者 Open [chrome://extensions](chrome://extensions)
- 把開發者模式打開。
- 將範例資料夾丟入，如果格式正確就會成功載入出現該擴充。
  <img src="/images/step_import.png" width="100%" />
- 網址列右方的擴充按鈕就會出現相關的圖示以及點擊後的彈出視窗 html。（以 hello 範例為例，你可以自行載入不同擴充看看效果）
  <img src="/images/step_popup.png" width="100%" />

---

## 動手更改程式碼

接下來自己寫一個擴充元件，加入自己想要控制的功能。

### 發想 1 : 一個簡單可實現的搜尋功能

你是否經常在閱讀網頁時對某個主題感興趣，但需要另外進行搜尋呢？我最近經常想查找公共圖書館是否有特定的電子書，但使用 Google 搜尋並不迅速。因此，我會打開所有需要的電子書網站，一一輸入關鍵字進行搜尋。這雖然是簡單的動作，卻花了不少時間。

<div class="blockquote">
Google Chrome 擴充功能支援在右鍵選單中添加擴充按鈕，我們可以利用這個功能實現對特定網站的搜尋。以電子書資源為例，在右鍵選單中加入一個按鈕，可以快速開啟特定網站的電子書資源。
</div>

#### 擴充功能 : 尋找台南圖書館線上資源

這裡是台南圖書館提供的[電子書資源網站列表](https://www.tnpl.tn.edu.tw/u4644318637373758255/s1)，我將挑選其中我每次都會查詢的網址，包括 HyRead ebook X 台南圖書館、台灣雲端書庫、udn 讀書館(臺南分區資源中心)、台灣雲端書庫和國立公共資訊圖書館電子書服務平台，進行一次開啟。

##### 功能 1 實現右鍵出現選單 contextMenus

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

---

##### 功能 2. popup 顯示條件搜尋

根據前面提到的 "action"，我們可以設定 "popup.html"，在這個 HTML 檔案中可以加入你希望呈現的頁面內容。這部分需要一些 HTML、CSS 和 JavaScript 的基礎技巧。而 "popup.js" 則負責定義與控制動作，並與前面提到的 Chrome API 進行互動。這樣的設定可以讓你自由地定製擴充功能的外觀和功能。

<article class="message is-info"><div class="message-body">
完成如下顯示，功能效果與前述相同，只是多加了搜尋設定：

</div></article>
<img src="https://github.com/minilabmemo/chrome-ext-find-ebook/raw/master/chrome-search-ebook.png" width="100%" />

- 延伸：
  - 如果要記住設定可以與 storage API 互動
  - 設定要能同步傳到右鍵開啟選項則可以使用 runtime API 消息傳遞傳送，

#### 完整程式碼

這裡是我完整的[程式碼 chrome-ext-find-ebook](https://github.com/minilabmemo/chrome-ext-find-ebook)，你可以根據需要添加其他地區的電子資源網站。如果這對你有用，請給我一些星星評價。如果你遇到問題或有其他需求，請在問題回報頁面上提出，我會盡力提供幫助。

---

### 發想 ２ ： 護眼功能

另一個想法是添加護眼功能。根據前面所提到的開啟新分頁的方法，我們也可以設定提醒通知。有時候，當我們在寫程式時，往往會連續工作數小時，經常忘記讓眼睛休息一下。儘管有使用過番茄鐘等應用程式，但往往會忽略背景執行的提醒。

<div class="blockquote">
我們可以開發一個擴充功能，每隔一段時間彈出提醒視窗，提醒使用者休息眼睛。可以設定時間間隔，例如每60分鐘彈出一次提醒。這樣即使沉浸在工作中，也會有提醒來保護視力健康。

</div>

但這項功能搜尋後發現已經有人做過了，完全符合我的需求，而且有些會去更改網頁底色，直接推薦這些元件出來，雖然我覺得應該可以參考再整合，之後有時間或更大的需求再來做做看了：

- [eyeCare - Protect your vision](https://chrome.google.com/webstore/detail/eyecare-protect-your-visi/eeeningnfkaonkonalpcicgemnnijjhn) 可以設定休息時間還有音效，跳出通知也有簡單的護眼訊息
- 深色模式，這個在[chrome 應用商店](https://chrome.google.com/webstore/category/extensions?hl=zh-TW) 搜尋可以發現很多，會幫你把網頁改成深色底色。

---

## 網路參考文章

<div class="ref">

- Photo by <a href="https://unsplash.com/@mediamodifier?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Mediamodifier</a> on <a href="https://unsplash.com/photos/nPZzZpWhPwg?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>

</div>

---
