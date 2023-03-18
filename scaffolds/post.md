---
title: {{ title }}
date: {{ date }}
tags:
  - test
toc: true



categories:
  - [Backend,golang]
  - [Frontend,css/html]
  - [Frontend,js]
  - [Frontend,react]
  - [技術工具,devOps]
  - [技術工具,blog]
  - [技術工具,未分類]
  - [技術工具,modules]
---


<article class="message is-info"><div class="message-body">
引言
<a href="xx">xx</a>
</div></article>

<!--more-->
## 目錄 | Contents
<div class="my-toc">
<!-- toc -->
</div>

## 網路參考文章

<div class="notification is-warning">
本篇文章內容參考如下
</div>


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

### 引言樣式

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