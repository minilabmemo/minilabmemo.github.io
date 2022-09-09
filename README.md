---
title:  HEXO BLOG


這是一個使用 HEXO 主題架設的部落格，方便快速建立文章及部屬在 github 上。

- github repo:
  https://github.com/minilabmemo/minilabmemo.github.io

- blog web IRL:
  https://minilabmemo.github.io/

## Quick Start
- node.js
- install hexo-cli
```
 npm install -g hexo-cli
 ```

- first download node_modules
```
 npm install
```

### hexo -v
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


### Create a new post

```bash
$ hexo new "My New Post"
```

### Run server

```bash
$ hexo server
```

### Generate static files

```bash
$ hexo generate
```

### Deploy to remote sites

```bash
$ hexo deploy
略
Branch 'master' set up to track remote branch 'master' from 'https://github.com/minilabmemo/minilabmemo.github.io.git'.
INFO  Deploy done: git
```

## upload

branch - src (have all files)
themes/next-reloaded will not upload
themes-bk/_config.yml will backup to upload
branch - master (only web files)


## post
```
{% note class_name %} Content (不設定) 淡灰色 {% endnote %}
{% note default %} 灰色 default {% endnote %}
{% note primary %} 紫色 primary {% endnote %}
{% note success %} 綠色 success {% endnote %}
{% note info %} 藍色 info {% endnote %}
{% note warning %} 黃色 warning {% endnote %}
{% note danger %} 紅色 danger {% endnote %}
```
## 重點標籤
```
{% label default@標示灰色底色 %}
{% label primary@標示紫色底色 %}
{% label success@標示綠色底色 %}
{% label info@標示藍色底色 %}
{% label warning@標示黃色底色 %}
{% label danger@標示danger底色 %}
```

{% label info@ES6%}

## image
- reminder:hexo g
```
![my](/images/avatar_memo.png)
或是用html寫法，可以控制大小
<img src="/images/avatar_memo.png" width="150px" />
```