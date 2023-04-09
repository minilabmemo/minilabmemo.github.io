---
title: "[Blog] 在文章底部加上 分享/贊助/評論 內容"
tags:
  - blog
  - hexo
toc: true
categories:
  - - 技術工具
    - blog
date: 2023-02-27 21:17:34
---


<article class="message is-info"><div class="message-body">
一開始設置完 blog，底部有幾個區塊- 分享/贊助/評論 沒有設定，是會跳出紅色框框的，這篇就來把文章底部相關的互動給補齊吧．
</div></article>

<!--more-->
## 目錄 | Contents
<div class="my-toc">
<!-- toc -->
</div>


## 分享按鈕
依照[Icarus用户指南 - 分享按钮](http://ppoffice.github.io/hexo-theme-icarus/Plugins/Share/icarus%E7%94%A8%E6%88%B7%E6%8C%87%E5%8D%97-%E5%88%86%E4%BA%AB%E6%8C%89%E9%92%AE/) 選擇一個喜歡的按鈕，我是用 addthis，依照說明填入，需注意要填入正確，不然會看不見．這一個用法要先去 addthis 上面註冊，然後可以在addthis時時更改樣式．

```diff _config.icarus.yml
share:
+    type: addthis
+    install_url:  '要填入正確'
```
- 起在本地就可以看到效果了．


## 評論功能
依照 [Icarus用户指南 - 用户评论插件](http://ppoffice.github.io/hexo-theme-icarus/Plugins/Comment/icarus%E7%94%A8%E6%88%B7%E6%8C%87%E5%8D%97-%E7%94%A8%E6%88%B7%E8%AF%84%E8%AE%BA%E6%8F%92%E4%BB%B6) 內有多種評論平台，我目前是直接使用 Facebook．

```diff _config.icarus.yml
comment:
+    type: facebook
```
- 起在本地就可以看到效果了．


## 贊助按鈕
依照 [Icarus用户指南 - 赞赏按钮](https://ppoffice.github.io/hexo-theme-icarus/Plugins/Donation/icarus%E7%94%A8%E6%88%B7%E6%8C%87%E5%8D%97-%E8%B5%9E%E8%B5%8F%E6%8C%89%E9%92%AE) 說明設定，選擇可以收款的方式．


```_config.icarus.yml
donates:
    -
        type: afdian
        url: ''
    -
        type: alipay
        qrcode: ''
    -
        type: buymeacoffee
        url: ''
    -
        type: patreon
        url: ''
    -
        type: paypal
        business: ''
        currency_code: USD
    -
        type: wechat
        qrcode: ''

```


## 網路參考文章

<div class="notification is-warning">
本篇文章內容參考如下
</div>

- AddThis 詳細的操作可以看這邊 [AddThis 現已免費！一行程式碼為網站加入分享追蹤按鈕，整合電子報等行銷功能](https://free.com.tw/addthis/)


Hey,I created a page here. You can now buy me a coffee!