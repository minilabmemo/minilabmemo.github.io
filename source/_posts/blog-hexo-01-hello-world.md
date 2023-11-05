---
title: '[Blog] 使用 Hexo 撰寫部落格 01- 建立部落格'
tags:
  - hexo
  - blog
categories:
  - [技術工具, blog]
date: 2021-01-31 10:06:20
---

> cq %}

# hexo 是什麼？

> endcq %}

 <blockquote class="blockquote-center">
 
Hexo 是一個快速、簡單且強大的網誌框架。Hexo 使用 Markdown 標記語言解析您的文章，並在幾秒鐘內，透過漂亮的主題產生靜態檔案。（來自 https://hexo.io/zh-tw/docs/ 說明）</blockquote>

# 本文將會知道

1. 如何使用 Hexo 產生部落格 （超快速，只要看到這邊就建好囉！）
2. 如何使用 markdown 撰寫文章
3. 如何部署到 github 個人網頁
4. 如何更改主題與內文風格 (本站用到的所有修改介紹，移到下一篇)

<!--more-->

## 安裝 hexo 與初始化部落格

### 產生基本部落格結構

```
安裝工具 （使用npm安裝 可先安裝Node：https://nodejs.org/en/）
$ npm install -g hexo-cli
初始資料夾
$ hexo init <folder>
進入資料夾及安裝相依
$ cd <folder>
$ npm install
這邊就已經做好初始化了
```

### 啟動部落格 Run server

```bash
$ hexo server
開啟瀏覽器 http://localhost:4000 就可以看到部落格了💕💕💕
```

More info: [Server](https://hexo.io/docs/server.html)

### （紀錄）顯示版本資訊

（有需要的話，可以查詢對應安裝版本）知道自己安裝的版本，對於之後查詢問題是很有幫助的喔！

```bash
$ hexo version
(node:5190) ExperimentalWarning: The fs.promises API is experimental
INFO  Validating config
hexo: 5.1.1
hexo-cli: 4.2.0
os: Darwin 19.0.0 darwin x64
http_parser: 2.8.0
node: 10.16.3
v8: 6.8.275.32-node.54
uv: 1.28.0
zlib: 1.2.11
brotli: 1.0.7
ares: 1.15.0
modules: 64
nghttp2: 1.39.2
napi: 4
openssl: 1.1.1c
icu: 64.2
unicode: 12.1
cldr: 35.1
tz: 2019a
```

---

## 開始撰寫文章

### 新增文章

```bash
$ hexo new "My New Post"
(預設)會在source/＿posts 底下新增一個 .md 檔案

$ hexo new draft "My New Post" //指定生成草稿
會在source/＿draft 底下新增一個 .md 檔案
```

More info: [Writing](https://hexo.io/docs/writing.html)

### 撰寫文章

在剛剛新增的檔案開始採用 markdown 語法開始撰寫文章．

- 可以找線上編輯器工具幫助撰寫及預覽，「自己習慣用這一個https://markdown-editor.github.io/」 ，編輯完再貼過來內文．
- 如對語法有一點熟悉，就直接用 vscode 打開檔案開始撰寫內文，並可以安裝 vscode markdown preview 插件，邊改邊預覽．

- 編寫完再啟動部落格並在瀏覽器查看效果． （可帶--draft 顯示草稿）

```
hexo s --draft
```

---

## 部署網站

### 建立與設定 Git 空間

- 先在 github 上新增一個專案叫與帳號一樣命名叫做“[yourname].github.io”

  > 建立完成後會有教你如何建立 commit & push 的語法，建議要先建立連結，之後部署才會順利．
  >
  > ```
  > git push -u origin master
  > ```

- 配置 \_config.yml

```
deploy:
  type: git
  repo: https://github.com/yourname/yourname.github.io
  branch: master
```

### 產生靜態文件 Generate static files

```bash
$ hexo generate 或是hexo g
會在public資料夾產生網站靜態檔案
這是用來部署到網站的檔案，記得每次部署前都要更新喔
```

More info: [Generating](https://hexo.io/docs/generating.html)

### 一鍵部署

```bash
$ hexo deploy
（略）
Branch 'master' set up to track remote branch 'master' from 'https://github.com/minilabmemo/minilabmemo.github.io'.
INFO  Deploy done: git
要看到這句才是部署成功，如果卡住可能要先檢查git連結是否正常．
```

其他空間部署說明(ex:heroku) More info: [Deployment](https://hexo.io/docs/one-command-deployment.html)

> 註：部署會上傳至剛剛 config 的位置，測試發現只會上傳 web 檔案相關如果有上傳 source/theme 檔案也會被移除．
> 因為在開發環境時可以先開一個 src branch 來控管原始檔案．
> <br>branch - src (have all files)
> <br>branch - master (only web files)

### 個人網站網址

https://yourname.github.io/

這樣就大功告成啦！🎉🎉🎉（註：有時要稍等一下才會看到更新）

### 清理靜態文件 Clean static files

```bash
$ hexo clean
清除快取檔案 (db.json) 和已產生的靜態檔案 (public)
```

> 下一篇會介紹如何更換主題及內文撰寫%}

---

## 參考文章

- Quick Start
  Welcome to [Hexo](https://hexo.io/)! Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues)

- [HEXO 指令](https://hexo.io/zh-tw/docs/commands.html)
