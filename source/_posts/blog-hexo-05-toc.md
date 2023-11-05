---
title: '[Blog] hexo 在文章開頭加上內容目錄'
cover: /img/posts/post-map-unsplash.jpg
thumbnail: /img/posts/post-map-unsplash.jpg
tags:
  - blog
toc: true
date: 2023-02-26 21:17:34
categories:
  - [技術工具, blog]
---

<article class="message is-info"><div class="message-body">
內容目錄"toc“ 是代表 table of contents 目錄，上一篇透過內建的toc雖然可以長出側邊欄，但如果想要在撰寫markdown時讓他出現文章開頭，就需要安裝額外的插件來做到，以下研究了兩種插件的方式並記錄下來．
</div></article>

<!--more-->

## 目錄 | Contents

<!-- toc -->

## 效果介紹

原本這個部落格的文章，就已經具有側邊欄 toc 了，只要在文章標頭放上`toc:true`即可，但我想要的效果是在文章開頭時就放上，這樣手機瀏覽時也能看到內容，這邊有找到安裝額外插件．

## 方法一: use hexo-toc

### 安裝 hexo-toc

- 安裝說明來自：https://github.com/bubkoo/hexo-toc

```
npm install hexo-toc --save
安裝完之後在文章內加入 <!-- toc --> 即可 //注意前後有空格
```

- 但這樣加完會出現所有階層，但我並不希望階層太多，可以出現第一層就好，需要再另外安裝插件 markdown-toc 並修改 config

```_
1. npm install --save markdown-toc

2. _config.yml
toc:
  maxdepth: 2
  class: toc

```

<div class="notification is-warning">
記得 hexo clean & hexo g 後啟動才會看到效果．
</div>

<article class="message is-warning"><div class="message-body">
這個插件的問題：這樣做完之後，側邊欄的階層也跟著被影響了，我希望側邊欄可以多階層並隨著文章閱讀而擴展，而內文開頭就顯示第一層就好．找不到方法所以先卸載hexo-toc．
</div></article>

## 方法二 use hexo-insert-toc

### 安裝 hexo-insert-toc

- 插件來自：https://github.com/bennycode/hexo-insert-toc

```shell
npm i hexo-insert-toc
```

- 更改階層

```_config.yml
hexo-insert-toc:
  maxdepth: 2
```

- 成功安裝完的 dependencies 版本

```go “展開查看dependencies版本” json >folded
  "dependencies": {
    "bulma-stylus": "^0.8.0",
    "hexo": "^6.3.0",
    "hexo-asset-image": "^1.0.0",
    "hexo-component-inferno": "^2.0.2",
    "hexo-deployer-git": "^2.1.0",
    "hexo-generator-archive": "^1.0.0",
    "hexo-generator-category": "^1.0.0",
    "hexo-generator-index": "^2.0.0",
    "hexo-generator-tag": "^1.0.0",
    "hexo-insert-toc": "^1.1.2",
    "hexo-log": "^3.2.0",
    "hexo-pagination": "^2.0.0",
    "hexo-renderer-ejs": "^1.0.0",
    "hexo-renderer-inferno": "^0.1.3",
    "hexo-renderer-marked": "^3.0.0",
    "hexo-renderer-stylus": "^2.0.0",
    "hexo-server": "^2.0.0",
    "hexo-theme-landscape": "^0.0.3",
    "markdown-toc": "^1.2.0"
  },
```

<article class="message is-warning"><div class="message-body">
這個插件產生出來的 toc 並不能客制class name，需要再自己加入，而且中文連結會無法跳轉，英文是正常的「尚不知如何解決，只好先練練英文了（誤）」．
</div></article>

#### 後記

<article class="message is-success">
  <div class="message-header">
    <p>20230318更新</p>
  </div>
  <div class="message-body">
    關於中文問題，後來有在這個作者的github上詢問.似乎是這個檔案   
    <a href="https://github.com/bennycode/hexo-insert-toc/blob/v1.1.2/src/slugify.js">slugify.js</a>造成，嘗試修改 replace 其實沒有什麼用，所以我就整段註解掉（後來有照作者建議修改），重新 hexo clean/hexo g ，就正常了，不太了解細節，看來是這個位置會變成<b>％E6</b>，但後來又變成<b>%25E6</b>，百分比符號又被變成<b>%25</b>，或許我使用的主題不需要這段，但這樣可以解決我的問題就好了，有時間再來研究．
    
  </div>
</article>

## reference

<div class="ref">

- Photo by <a href="https://unsplash.com/@milanseitler?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Milan Seitler</a> on <a href="https://unsplash.com/photos/WzJoydMPTiI?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>

</div>
