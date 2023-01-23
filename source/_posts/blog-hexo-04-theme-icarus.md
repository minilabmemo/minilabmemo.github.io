---
title: "[Blog] 使用 Hexo 撰寫部落格 2023 更換ICARUS主題"
cover: /img/posts/dariusz-sankowski-3OiYMgDKJ6k-unsplash.jpg
thumbnail: /img/posts/dariusz-sankowski-3OiYMgDKJ6k-unsplash.jpg
tags:
  - blog
toc: true
categories:
  - [開發相關,blog]
date: 2023-01-22 16:31:36
---


>2023年 突然想要來換了主題，原本用的 NextT 版面配置似乎較少，來換一下



<!--more-->

## hexo 版本
```
$ hexo version
INFO  Validating config
Inferno is in development mode.
INFO  =======================================
 ██╗ ██████╗ █████╗ ██████╗ ██╗   ██╗███████╗
 ██║██╔════╝██╔══██╗██╔══██╗██║   ██║██╔════╝
 ██║██║     ███████║██████╔╝██║   ██║███████╗
 ██║██║     ██╔══██║██╔══██╗██║   ██║╚════██║
 ██║╚██████╗██║  ██║██║  ██║╚██████╔╝███████║
 ╚═╝ ╚═════╝╚═╝  ╚═╝╚═╝  ╚═╝ ╚═════╝ ╚══════╝
=============================================
INFO  === Checking package dependencies ===
INFO  === Checking theme configurations ===
INFO  === Registering Hexo extensions ===
hexo: 5.4.2
hexo-cli: 4.3.0
os: darwin 22.1.0 13.0.1

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

## 更換主題
根據主題的[hexo-theme-icarus](https://github.com/ppoffice/hexo-theme-icarus) github教學

- 執行安裝指令 
有兩種方式，我用的是ＮＰＭ安裝
```
$ npm install -S hexo-theme-icarus hexo-renderer-inferno
$ hexo config theme icarus
然後執行hexo s 就可以了
> 這種安裝方式自己的目錄中不會出現/themes/xxx 這樣的資料夾，設定也都出現在外層喔
```

- 成功啟動後的初始畫面


<img src="/images/icarus_init_ui.png" width="auto" />
可以看到這邊很多介紹都還沒有更改，接下來可以開始更改內容．

- 用

![icarus_init](icarus_init.png)




## 替換配置


### 修正 ＿config 檔案

```_config.yml
language: zh-TW
timezone: 'Asia/Taipei'
sidebar:
    left:
        sticky: false
    right:
        sticky: true  // 側邊欄固定，文章移動也可以見到

```

### 修正 config.icarus 檔案
```/_config.icarus.yml

```

### 新增文章
#### 文章的 Front-Matter设置

```diff
title: Getting Started with Icarus

//文章封面
cover: /img/posts/dariusz-sankowski-3OiYMgDKJ6k-unsplash.jpg 

//文章縮圖
thumbnail: /img/posts/dariusz-sankowski-3OiYMgDKJ6k-unsplash.jpg

// 文章目錄導覽
toc: true

```

>Tip: 默認文章都是不開啟toc的，要手動添加在文章開頭，但網路上有教學使之預設開啟．


#### 文章插入圖片
根據這篇說明[Asset Folders](https://hexo.io/docs/asset-folders.html)，有兩種方式，一種是放在/source/images，一種是依文章分類放置．
```插入圖片語法
// 第一種方法 一定要取名images資料夾 不知道為什麼不能隨便命名
<img src="/images/icarus_init_ui.png" width="auto" />


// 第一種方法 hexo new xxx 時會有一個獨立資料夾可以放圖片
不知道為什麼我這邊是開啟
post_asset_folder: true 
permalink: ':year/:month/:day/:title/'
```

---

#### [後記] 過程中處理問題
- 安裝啟動錯誤

```
註：因為我是從NextT轉換過來的，才發現有些特殊標籤在這邊啟動會爆錯
> ：``` Error [Nunjucks Error]: about/index.md [Line 7, Column 4] unknown block tag: note```
> 因此我把文章中的找到`{% note info %} `與`{% endnote %}`。移除．
```


- 再次啟動還是爆錯
```diff
const { Component } = require('inferno'); const classname = require('hexo-component-inferno/lib/util/classname'); const Head = require('./common/head'); const Navbar = require('./common/navbar'); const Widgets = require('./common/widgets'); const Footer = require('./common/footer'); const Scripts = require('./common/scripts'); const Search = require('./common/search'); module.exports = class extends Component { render() { const { site, config, page, helper, body } = this.props; const language = page.lang || page.language || config.language; const columnCount = Widgets.getColumnCount(config.widgets); return ; } };

// 解法因為官網github 少了hexo-renderer-inferno 用另一個月再次安裝即可
- $ npm install hexo-theme-icarus
+ $ npm install -S hexo-theme-icarus hexo-renderer-inferno
```


- 刪除舊的NextT主題預設產生位置

```diff
- 2020
- 2021
+ .....
+ public
+   2020
+   2021

//如果下hexo clean hexo g 會發現文章會產生在public資料夾裡，以前舊的主題先刪除
```



- TBD
```
看板娘
留言區


```


 網路參考文章
- [Icarus快速上手](https://ppoffice.github.io/hexo-theme-icarus/uncategorized/icarus%E5%BF%AB%E9%80%9F%E4%B8%8A%E6%89%8B/)
- [Icarus用户指南 - 主题配置](http://ppoffice.github.io/hexo-theme-icarus/Configuration/icarus%E7%94%A8%E6%88%B7%E6%8C%87%E5%8D%97-%E4%B8%BB%E9%A2%98%E9%85%8D%E7%BD%AE/#%E9%A1%B5%E8%84%9A)
- [Hexo-Icarus主题配置建议](https://blog.andycen.com/2020/03/07/Hexo-Icarus%E4%B8%BB%E9%A2%98%E9%85%8D%E7%BD%AE%E5%BB%BA%E8%AE%AE/)
