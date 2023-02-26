---
title: "[blog] hexo 在文章開頭加上內容目錄"
cover: /img/posts/post-map-unsplash.jpg
thumbnail: /img/posts/post-map-unsplash.jpg
tags:
  - blog
toc: true
date: 2023-02-26 21:17:34
categories:
  - [技術工具,blog]
---





{% raw %}<div class="notification is-info">{% endraw %}
內容目錄"toc“ 是代表 table of contents 目錄，上一篇透過內建的toc雖然可以長出側邊欄，但如果想要在撰寫markdown時讓他出現文章開頭，就需要安裝額外的插件來做到，以下研究了兩種插件的方式並記錄下來．
{% raw %}</div>{% endraw %}


<!--more-->

<div class="my-toc">

## 目錄 | Contents
<!-- toc -->
</div>


## 內建的側邊欄 toc
原本這個部落格的文章，就已經具有側邊欄toc了，只要在文章標頭放上`toc:true`即可，但我想要的效果是在文章開頭時就放上，這樣手機瀏覽時也能看到內容，這邊有找到安裝額外插件．

## 方法一：hexo-toc

### 安裝hexo-toc

- 安裝說明來自：https://github.com/bubkoo/hexo-toc
```
npm install hexo-toc --save
安裝完之後在文章內加入 <!-- toc --> 即可 //注意前後有空格
```
- 但這樣加完會出現所有階層，但我並不希望階層太多，可以出現第一層就好，需要再另外安裝插件markdown-toc並修改config
```_
1. npm install --save markdown-toc

2. _config.yml
toc:
  maxdepth: 2
  class: toc

```

- 記得 hexo clean & hexo g 然後啟動才會看到效果．

<div class="notification is-success">
這個插件的問題：
但這樣做完之後，側邊欄的階層也跟著被影響了，我希望側邊欄可以多階層並隨著文章閱讀而擴展，而內文開頭就顯示第一層就好．找不到方法所以先卸載hexo-toc．
</div>

## 方法二：hexo-insert-toc

### 安裝hexo-insert-toc
- 插件來自：https://github.com/bennycode/hexo-insert-toc
```  
npm i hexo-insert-toc
```
- 更改階層
```
hexo-insert-toc:
  maxdepth: 2
```
- 但是這個插件產生出來的 toc 並不能客制class name，需要再自己加入．



## 網路參考文章
本篇文章內容參考如下

- Photo by <a href="https://unsplash.com/@milanseitler?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Milan Seitler</a> on <a href="https://unsplash.com/photos/WzJoydMPTiI?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  