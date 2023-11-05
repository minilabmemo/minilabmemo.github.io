---
title: "[css] position 位置介紹"
tags:
  - css
toc: true
categories:
  - - Frontend
    - css/html
date: 2023-10-26 13:44:03
---


<article class="message is-info"><div class="message-body">
css position 位置介紹
<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/position">MDN</a>
</div></article>

<!--more-->
## 目錄 | Contents
<div class="my-toc">
<!-- toc -->
</div>

-----
<div class="blockquote">
 重點引言
</div>
<span class="my-hightlight ">備忘筆記</span>

## position 介紹
- 控制元素顯示位置，其值有：預設值：static , 相對定位：relative,絕對定位：absolute,固定定位：fixed,黏性定位：sticky
- 當設定非static以外值後，可以設定top，right，bottom 和 left 屬性與z-index來決定最終位置。

<div class="blockquote">
CSS z-index 屬性設定定位元素及其後代元素或 flex 專案的 Z 軸順序。 <span class="my-hightlight ">z-index 較大的重疊元素會涵蓋較小的元素。</span>
</div>


### 相對定位 relative
- 偏離自身原始的位置
- 仍保留空間。
```html
<div class="box" id="two">Two</div>
```

```css
#two {
  position: relative;
  top: 20px;
  left: 20px;
  background: blue;
}

```

## 絕對定位 absolute
- 定位相對於最近的非 static 祖先元素定位。 當這樣的祖先元素不存在時，則相對於 ICB（initial containing block，初始包含區塊）。
- 自己獨立一層出來，不保留空間
- 最後定位在視窗，並非是body，捲動時仍然在視窗上固定位置，可能捲動會消失。
- 很常出現在折價標籤上。


## 固定定位 
- 定位相對於最近的非 static 祖先元素定位。
- 自己獨立一層出來，不保留空間
- 與絕對定位不同之處：相對於螢幕視窗（viewport）的位置來指定元素位置。 元素的位置在螢幕滾動時不會改變
>当元素祖先的 transform、perspective、filter 或 backdrop-filter 属性非 none 时，容器由视口改为该祖先
- 常見於 蓋板廣告/modal組件/回到頂端 等應用

## stick
 sticky 元素会“固定”在离它最近的一个拥有“滚动机制”的祖先上


## 網路參考文章

<div class="ref">
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
-------------


## 網路參考文章

<div class="ref">

- Photo by <a href="https://unsplash.com/@mediamodifier?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Mediamodifier</a> on <a href="https://unsplash.com/photos/nPZzZpWhPwg?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>

  
</div>