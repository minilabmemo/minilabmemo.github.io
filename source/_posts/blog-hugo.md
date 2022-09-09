---
title: "[Blog] 使用 Hugo 撰寫部落格"
date: 2020.09.01 17:23:46
tags:
  - hugo
  - blog
categories:
  - Tech.
  - Web
  - blog
---

> 本章介紹如何在套用 hugo 做好一個自己的部落格網站．並上傳 github

---

2020.09 更新： 因為找不到主題可以將文章標題透過階層式瀏覽，所以後來改用 hexo（就是現在這邊網站用的樣式），使用上部署也較 hugo 方便，本篇紀錄當時的 hugo 建立留存．

- 建立部落格前可以先分別上 hexo/hugo 官網查看主題效果，看自己喜歡哪一種再建立．
- hexo 教學文請看： [使用Ｈ exo 撰寫部落格](https://minilabmemo.github.io/2020/08/31/hexo-hello-world/)

<!--more-->

#### Step 1: 安裝 Hugo

開啟終端機，依序執行下列指令：

```
* brew install hugo
//macOs 須先安裝Homebrew
* hugo version
//確認安裝成功版本
Hugo Static Site Generator v0.69.0/extended darwin/amd64 BuildDate: unknow
* hugo new site **website-hugo**
* cd **website-hugo**
// 新增網站，粗體可以自命名，安裝完會新增該資料夾
```

#### Step 2: 新增主題

https://themes.gohugo.io/
hugo 網站有很多可以選擇與查看效果
進入該主題的 github/README 可以看安裝步驟執行
基本執行：git submodule add https://github.com/alex-shpak/hugo-book themes/book
//這樣就會在**website-hugo**/themes/新增主題

#### Step 3: 編輯 config.toml

這檔案與整體網站設定有關

> baseURL = "https://xxx.github.io/"  
> languageCode = "zh-tw"
> title = "xxx Blog"

- #domain 設定 xxx 改成你的 GitHub 帳號名稱
- 根據主題不同 這檔案也可能會有更多不同設定
  ex: 設定主題 theme = "ananke"

#### Step 4: 新增文章

- hugo new posts/my-first-post.md
  新增預設檔案在以下位置 採用 markdown 編寫
  content/<CATEGORY>/<FILE>.<FORMAT>
  > title: "My First Post"
  > date: 2019-03-26T08:47:11+01:00
  > draft: true //是草稿是否 改成 false 可被發布

可以根據主題新增：
tags: ["hugo", "web"]
summary: "The summary image should be a custom one"
summaryImage: "summary_2.jpg"
resources:

- src: summary_2.jpg

- 圖片新增
  將圖片放置在 website-hugo/static/images
  文章內可用相對路徑新增![](/images/xxx)

#### Step 5: 啟動本地 server

- hugo server -D
  Web Server is available at http://localhost:1313/
  Press Ctrl+C to stop
  記得結束務必按 不然下次啟動會佔用

#### Step 6: 產生靜態檔案

Ｄ 參數代表要不要輸出草稿文章
Build static pages

- hugo -D

將會生成./public/ 資料夾，
每次編輯完要記得更新，之後發布的時候也要上傳

---

#### Step 7:githug 網站上傳

新增兩個 repo
xxx.github.io (xxx 改成自己的帳號名稱)
website-hugo 上述的 site 名稱

上傳 public 資料夾

> cd public
> git init
> git remote add origin https://github.com/xxx/xxx.github.io.git
> git add .
> git commit -m "Initial commit"
> git push -u origin master

上傳整個 website-hugo 資料夾

> cd ../
> git init
> git remote add origin https://github.com/xxx/website-hugo.git
> git add .
> git commit -m "Initial commit"
> git push -u origin master

開啟https://xxx.github.io/ 等個幾分鐘會看到結果

{% note class_name %} #### 參考文章 {% endnote %}

- [ＨＵＧＯ官網](https://gohugo.io/getting-started/quick-start/)
- [在-github-部署-hugo-靜態網站](https://medium.com/@chswei/%E5%9C%A8-github-%E9%83%A8%E7%BD%B2-hugo-%E9%9D%9C%E6%85%8B%E7%B6%B2%E7%AB%99-9c40682dfe40)
