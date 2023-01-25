---
title: "[Blog] 五分鐘教你使用 docusaurus 建立筆記部落格"
tags:
  - blog
  - docusaurus
categories:
  - [技術工具,blog]
date: 2021-05-21 18:39:33
---


>雖然說現在用的hexo技術建立的部落格就是為了寫筆記，但有時候只是為了真的純快速紀錄，之後待查或待看，但要整理成新的文章往往要一段時間，且很多不同的速記比較很難一下找出來，這時看到有另一種風格的部落格蠻適合當這樣的記錄的，適合作文檔的站點． 
> 
1.Docusaurus will help you ship a beautiful documentation site in no time.
2.是由[Faecbook團隊開源專案](https://github.com/facebook/docusaurus)，提供的一款易於維護的靜態網站建立工具，且可以使用react技術編輯．（MIT License）


---
個人選擇的優點：
  1. 左側有可以開闔的側欄，且進入文章後不會不見，可以快速瀏覽．
  2. 單純作為文檔保存筆記而建立
  3. 玩玩Docusaurus ！！

（第一點雖然hexo我有試圖找過有沒有不同主題可以符合這樣的需求，但搜尋上有點困難，就當作為了切開風格而另架一種風格的網站，而且也很快速．）

<!--more-->

## 建立Docusaurus
馬上就進入[官網](https://docusaurus.io/docs) 看 get started 說明流程只要三個指令：
```javascript
npx @docusaurus/init@latest init my-website classic
cd my-website
npx docusaurus start
```
Ex 我的配置流程，我用的命名為note-blog(你可以使用自訂的命名)：
```javascript
blog npx @docusaurus/init@latest init note-blog classic

npx: 40 安裝成功，花費 6.139 秒

Creating new Docusaurus project ...

Success! Created note-blog
Inside that directory, you can run several commands:

  npm start
    Starts the development server.

  npm run build
    Bundles the app into static files for production.

  npm deploy
    Publish website to GitHub pages.

We suggest that you begin by typing:

  cd note-blog
  npm start
```
這邊最後一步啟動介紹寫的有點不同，但是都可以啟動

一些基本的畫面就出來了☼☼☼
http://localhost:3000/note-blog/

<img src="/images/post/note-blog-ui.png" width="500px"/>

接著我先不改內容，先部署到網路上拿到正式網址．

----

## 上傳到github
這邊我用的方式是用gh-pages工具的做法，跟[官網deployment介紹](https://docusaurus.io/docs/deployment)的有點不同，（個人覺得官網寫的覺得有點難懂，但流程可能比較正式，有興趣的人可以試著做做看）


個人使用gh-pages工具流程記錄如下．

1. 先到github新增專案名為“”note-blog
2. 先把剛剛的專案上傳到GIT
```Bash 基本上照gutbuh建立完的提示輸入就好
git remote add origin XXX
git push -u origin master
```
3.安裝gh-pages工具
```
npm install --save gh-pages
```
3. 在專案的 package.json 中加入 homepage與scripts
```diff
"name": "note-blog",
+ "homepage": "https://minilabmemo.github.io/note-blog",
scripts": {
+   "predeploy": "npm run build",
+    "deploy": "gh-pages -d build",
     "docusaurus": "docusaurus",
    "start": "docusaurus start",
    "build": "docusaurus build",
    "swizzle": "docusaurus swizzle",
-    "deploy": "docusaurus deploy",
```
4.接著gh-page 就可以用下列指令上傳啦
```shell console
npm run deploy

略
Success! Generated static files in build.

Use `npm run serve` to test your build locally.
> note-blog@0.0.0 deploy /xxxx
> gh-pages -d build

Published
```
5. 成功部署到 Github 上後，會發現多了一個名為 gh-pages 的分支，教學文中說設定頁->GitHub Pages->Source要把頁面指到 gh-pages 這個分支（但我查看預設就是了）

6. 接著打開頁面，結果發現馬上跳[錯誤畫面](https://docusaurus.io/docs/docusaurus.config.js#baseurlissuebanner)，但有指示要更改docusaurus.config.js檔案內的
```
baseUrl: '/note-blog/',
```

7. 再開一次頁面會成功了！！
https://minilabmemo.github.io/note-blog/


（到這邊大約就五分鐘差不多，但為了看懂它的編輯設定還是花了我一點時間．）

---

## 開始編輯網站
建立完後基本畫面上就有教學了，而且覺得比官網上的說明還要清楚，可以直接查看這邊就好，我也保留了這些教學文件（->[點我](https://minilabmemo.github.io/note-blog/docs/docusaurus/tutorial-basics/create-a-page)）

---

以下就簡單紀錄使用用法:

### 更改設定檔 docusaurus.config.js
這邊可以更改網站標題與logo，看欄位一一修改應該沒什麼困難,但也有更多可以新增的欄位設定:
1. 主設定檔說明寫在[這邊](https://docusaurus.io/docs/docusaurus.config.js)
2. [主題使用設定](https://docusaurus.io/docs/api/themes/configuration)，可以修改導覽列的下拉清單，新增通知訊息等．

### 編輯的文件檔案說明
文件的編輯格式檔案有兩種選擇
1. 學過react可以用js撰寫
2. 一般可以使用Markdown(.md)撰寫（不知道什麼是Markdown的可以先去玩玩線上編輯工具),而docusaurus可以輸入前言作為描述顯示相關位置：
- [相關的markdown前言](https://docusaurus.io/zh-CN/docs/api/plugins/@docusaurus/plugin-content-docs#markdown-frontmatter)

#### 新增頁面 page
可以新增一個頁面，然後對應的網址就會出現對應內容了，這通常是獨立頁面，需要另外用超連結指到這個位置．
- 須注意對應的網址會在 baseUrl底下喔
```
ex
/src/pages/foo/index.js → <baseUrl>/foo/
```
- 看看效果：
note-blog/src/pages/markdown-page.md
 →https://minilabmemo.github.io/note-blog/markdown-page/

#### 建立文件 Document
可以直接把文章放到docs資料夾裡，並在前言編輯位置與標題就會出現在側邊欄了．



```markdown /docs/intro.md
+ ---
+ sidebar_label: "Hi!"  
+ sidebar_position: 3
+ ---

# Hello 這邊就是文章內容

This is my **first Docusaurus document**!
```

### 建立blog
這邊一樣方法，只是會建立在blog分頁，裡面已經有基本範本，且說明blog支援tags功能，如果不想要blog頁籤，可以把整個資料夾刪除（/your_repo/blog/2019-05-30-welcome.md）．

## 新增與修改插件設定
[插件列表](https://docusaurus.io/zh-CN/docs/api/plugins)

### plugin-content-docs
如果是有裝classic主題，就可以不用另外安裝，[plugin-content-docs](https://docusaurus.io/zh-CN/docs/api/plugins/@docusaurus/plugin-content-docs)裡的內容可以像下面修改：

- editUrl：修改進入github編輯的位址
- showLastUpdateTime：顯示修改日期
```diff /docusaurus.config.js 
presets: [
    [
      '@docusaurus/preset-classic',
      {
        docs: {
           editUrl:
            'https://github.com/<git_account>/<repo>/edit/master/', 
+          showLastUpdateTime: true,
        }

      },
    ],
  ],
```
-----

## 注意事項 - 錯誤狀況
不知道為什麼有的時候能顯示，但是跑到deploy & build時，如果文章中有錯誤連結，就會跑出一堆錯誤喔～！！！可以在一堆錯誤上方中找到,一不小心會以為是npm與libiary問題....

```
Exhaustive list of all broken links found
....
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/yiyin/.npm/_logs/2021-08-03T06_04_03_540Z-debug.log
```


## 網路參考文章

- [docusaurus 中文指南](https://www.docusaurus.cn/docs/configuration)
- [[Day 29 - 即時天氣] 寫網頁就是要炫耀啊，不然要幹麻？發布上 Github Pages 吧！](https://ithelp.ithome.com.tw/articles/10228423)