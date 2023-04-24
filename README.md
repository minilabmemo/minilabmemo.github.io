---
title:  HEXO BLOG

這是一個使用 HEXO 主題架設的部落格，方便快速建立文章及部屬在 github 上。



## 安裝工具
- node.js
- install hexo-cli
```
 npm install -g hexo-cli
 ```

- first download node_modules
```
 npm install
```

### 版本資訊
```
$ hexo -v
INFO  Validating config
hexo: 5.3.0
hexo-cli: 4.3.0
os: darwin 21.4.0 12.3.1

node: 14.17.0
v8: 8.4.371.23-node.63
uv: 1.41.0
zlib: 1.2.11
brotli: 1.0.9
ares: 1.17.1
modules: 83
nghttp2: 1.42.0
napi: 8
llhttp: 2.1.3
openssl: 1.1.1k
cldr: 38.1
icu: 68.2
tz: 2020d
unicode: 13.0
```


### Create a new post 新增文章

```bash
$ hexo new "My New Post"
```

### Run server

```bash
$ hexo server
```

### Generate static files

```bash
$ hexo clean
$ hexo generate
```

### Deploy to remote sites

```bash
$ hexo deploy
略
Branch 'master' set up to track remote branch 'master' from 'https://github.com/yumememooo/yumememooo.github.io.git'.
INFO  Deploy done: git

// 部署時有時會卡住，這時可以停掉再試一次
// 看看從別的分支用vscode上傳是不是正常，需不需要驗證
// 其他看git 問題紀錄https://app.gitbook.com/s/g0YeSII30XzmXFpIwfHd/tools-cmd/cli/git/wen-ti-ji-lu
```

## upload

branch - src (have all files)
branch - master (only web files)
----

### image
要把圖片放到source/images裏面
> reminder:hexo g
```
![my](/images/avatar_memo.png)
或是用html寫法，可以控制大小
<img src="/images/avatar_memo.png" width="150px" />

//
<a href=""></a>
```



### 個人分類清單
```
Front-Matter
categories:
  - [Backend,golang]
  - [Backend,java]
  - [Backend,python]
  - [Frontend,css/html]
  - [Frontend,js]
  - [Frontend,react]
  - [Frontend,tips]
  - [技術工具,devOps]
  - [技術工具,blog]
  - [技術工具,未分類]
  - [技術工具,效能]
  - [技術工具,Tips]
  - [技術工具,IDE]
  - [技術工具,Linux/Mac]
  - [技術工具,測試]
  - [技術工具,modules]

```




### 程式碼區塊
diff >folded
diff “點我查看config.icarus.yml細節” >folded 


### 引言樣式
在我的文章裡面有沒有加raw都可以顯示 不知用意
```
{% raw %}<div class="notification is-info">{% endraw %}xxx
{% raw %}</div>{% endraw %}
//色彩
success
warning
danger
```

- 三種樣式
```
//全底色彩
<div class="notification is-info">
xxx
</div>

//側邊
<article class="message is-info"><div class="message-body">
xxx
</div></article>

//header
<article class="message is-info"><div class="message-header">title
</div><div class="message-body">
message
</div></article>
```

## 創建補丁
```
// npx patch-package package-name
npx patch-package xxx

npx patch-package hexo-insert-toc
npx patch-package hexo-theme-icarus --include ".*(?:include|common).*"
npx patch-package hexo-component-inferno --include ".*.js"
```