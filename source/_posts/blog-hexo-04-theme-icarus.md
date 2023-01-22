---
title: "[Blog] 使用 Hexo 撰寫部落格 2023 更換ICARUS主題"
cover: /img/posts/dariusz-sankowski-3OiYMgDKJ6k-unsplash.jpg
tags:
  - blog
categories:
  - [開發相關,blog]
date: 2023-01-22 16:31:36
---


>2023年 突然想要來換了主題，原本用的 NextT 版面配置似乎較少，來換一下



<!--more-->

## 更換主題
根據主題的[github教學](https://github.com/ppoffice/hexo-theme-icarus)
- 
```
$ npm install hexo-theme-icarus
$ hexo config theme icarus

```

> 註：因為我是從NextT轉換過來的，才發現有些特殊標籤在這邊啟動會爆錯
> ：``` Error [Nunjucks Error]: about/index.md [Line 7, Column 4] unknown block tag: note```
> 因此我把文章中的找到`{% note info %} `與`{% endnote %}`。移除．
> 其實很喜歡這些主題的顏色標籤，有點不忍心．

- 再次啟動還是爆錯
```
const { Component } = require('inferno'); const classname = require('hexo-component-inferno/lib/util/classname'); const Head = require('./common/head'); const Navbar = require('./common/navbar'); const Widgets = require('./common/widgets'); const Footer = require('./common/footer'); const Scripts = require('./common/scripts'); const Search = require('./common/search'); module.exports = class extends Component { render() { const { site, config, page, helper, body } = this.props; const language = page.lang || page.language || config.language; const columnCount = Widgets.getColumnCount(config.widgets); return ; } };
```
- 找到比較細部的安裝說明，如下
```
npm install -S hexo-theme-icarus hexo-renderer-inferno
然後執行hexo s 就可以了
```
- 成功啟動後的初始畫面
![theme](img/posts/new-theme.png)

## 替換配置
基本教學手冊[Icarus用户指南 - 主题配置](http://ppoffice.github.io/hexo-theme-icarus/Configuration/icarus%E7%94%A8%E6%88%B7%E6%8C%87%E5%8D%97-%E4%B8%BB%E9%A2%98%E9%85%8D%E7%BD%AE/#%E9%A1%B5%E8%84%9A)

- 修正檔案

```
hhh

```

## 網路參考文章
> - []()
> <span style="font-size: 9px;">
學習路上感謝網路大神們，如果你發現了我，可以查看以下參考文章了解更多概念👇👇👇</span>