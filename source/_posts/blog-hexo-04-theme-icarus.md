---
title: "[Blog] 使用 Hexo 撰寫部落格-04更換ICARUS主題"
cover: /img/posts/dariusz-sankowski-3OiYMgDKJ6k-unsplash.jpg
thumbnail: /img/posts/dariusz-sankowski-3OiYMgDKJ6k-unsplash.jpg
tags:
  - blog
  - hexo
toc: true
categories:
  - [開發相關,blog]
date: 2023-01-22 16:31:36
---



{% raw %}<div class="notification is-info">{% endraw %}
2023年新的一年，突然想要來幫部落格換個新主題🔆，原本用的 NextT 版面太容易看到了，這陣子看到 ICARUS 主題，覺得蠻喜歡它的版面配置的，於是就把主題換一下，目前的環境已經裝好hexo了，這篇就直接從更換主題開始～
{% raw %}</div>{% endraw %}

<!--more-->

## hexo 版本 與相依設定
使用 hexo version 可以查詢版本
```diff “點我查看hexo version ” >folded 
+ $ hexo version
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

```diff “點我查看package.json ” >folded 
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "build": "hexo generate",
    "clean": "hexo clean",
    "deploy": "hexo deploy",
    "server": "hexo server"
  },
  "hexo": {
    "version": "5.4.2"
  },
  "dependencies": {
    "hexo": "^5.4.2",
    "hexo-asset-image": "^1.0.0",
    "hexo-deployer-git": "^2.1.0",
    "hexo-generator-archive": "^1.0.0",
    "hexo-generator-category": "^1.0.0",
    "hexo-generator-index": "^2.0.0",
    "hexo-generator-tag": "^1.0.0",
    "hexo-renderer-ejs": "^1.0.0",
    "hexo-renderer-inferno": "^0.1.3",
    "hexo-renderer-marked": "^3.0.0",
    "hexo-renderer-stylus": "^2.0.0",
    "hexo-server": "^2.0.0",
    "hexo-tag-cloud": "^2.1.2",
    "hexo-theme-icarus": "^5.1.1",
    "hexo-theme-landscape": "^0.0.3"
  }
}
```

## 更換主題


- 執行安裝指令 
有兩種方式，我用的是ＮＰＭ安裝 see [Getting Started with Icarus](https://ppoffice.github.io/hexo-theme-icarus/uncategorized/getting-started-with-icarus/)
```
$ npm install -S hexo-theme-icarus hexo-renderer-inferno
$ hexo config theme icarus
然後執行hexo s 就可以了
> 這種安裝方式自己的目錄中不會出現/themes/xxx 這樣的資料夾，設定也都出現在外層喔
```

- 成功啟動後的初始畫面


<img src="/images/icarus_init_ui.png" width="auto" />
可以看到這邊很多介紹都還沒有更改，接下來可以開始更改內容．






## 替換配置


### 修正 ＿config 檔案 基本設定
這裡面的設定就改成自己的資料，另外可以預設語言與時區
```diff _config.yml
+ language: zh-TW
+ timezone: 'Asia/Taipei'

```

### 修正 config.icarus 檔案 配置版面


```diff “點我查看config.icarus.yml細節” >folded 
version: 5.1.0
variant: default
- logo: /img/logo.svg
head:
-    favicon: /img/favicon.svg
    manifest:
        name: 
        short_name: 
        start_url: 
        theme_color: 
        background_color: 
        display: standalone
        icons:
            -
                src: ''
                sizes: ''
                type: 
    open_graph:
        title: 
        type: blog
        url: 
        image: 
        site_name: 
        author: 
        description: 
        twitter_card: 
        twitter_id: 
        twitter_site: 
        google_plus: 
        fb_admins: 
        fb_app_id: 
    structured_data:
        title: 
        description: 
        url: 
        author: 
        publisher: 
        publisher_logo: 
        image: 
    meta:
        - ''
    rss: 
navbar:
    menu:
        Home: /
        Archives: /archives
        Categories: /categories
        Tags: /tags
        About: /about
    links:
-        Download on GitHub:
-            icon: fab fa-github
-            url: https://github.com/ppoffice/hexo-theme-icarus
footer:
    links:
        Creative Commons:
            icon: fab fa-creative-commons
            url: https://creativecommons.org/
        Attribution 4.0 International:
            icon: fab fa-creative-commons-by
            url: https://creativecommons.org/licenses/by/4.0/
        Download on GitHub:
            icon: fab fa-github
            url: https://github.com/ppoffice/hexo-theme-icarus
article:
    highlight:
-        theme: atom-one-light
+       theme: atom-one-dark
        clipboard: true
        fold: unfolded
    readtime: true
    update_time: true
    licenses:
        Creative Commons:
            icon: fab fa-creative-commons
            url: https://creativecommons.org/
        Attribution:
            icon: fab fa-creative-commons-by
            url: https://creativecommons.org/licenses/by/4.0/
        Noncommercial:
            icon: fab fa-creative-commons-nc
            url: https://creativecommons.org/licenses/by-nc/4.0/
search:
    type: insight
    index_pages: true
comment:
    type: disqus
    shortname: ''
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
share:
    type: sharethis
    install_url: ''
sidebar:
    left:
        sticky: false
    right:
        sticky: false
widgets:
    -
        position: left
        type: profile
        author: Your name
        author_title: Your title
        location: Your location
        avatar: 
        avatar_rounded: false
        gravatar: 
        follow_link: https://github.com/ppoffice
        social_links:
            Github:
                icon: fab fa-github
                url: https://github.com/ppoffice
            Facebook:
                icon: fab fa-facebook
                url: https://facebook.com
            Twitter:
                icon: fab fa-twitter
                url: https://twitter.com
            Dribbble:
                icon: fab fa-dribbble
                url: https://dribbble.com
            RSS:
                icon: fas fa-rss
                url: /
    -
        position: left
        type: toc
        index: true
        collapsed: true
+        depth: 4
    -
        position: left
        type: links
        links:
            Hexo: https://hexo.io
            Bulma: https://bulma.io
    -
        position: left
        type: categories
    -
        position: left
        type: recent_posts
    -
        position: left
        type: archives
    -
        position: left
        type: tags
        order_by: name
        amount: 
        show_count: true
    -
        position: left
        type: subscribe_email
        description: 
        feedburner_id: ''
    -
        position: left
        type: adsense
        client_id: ''
        slot_id: ''
    -
        position: left
        type: followit
        description: 
        action_url: ''
        verification_code: ''
plugins:
    animejs: true
    back_to_top: true
    baidu_analytics:
        tracking_id: 
    bing_webmaster:
        tracking_id: 
    busuanzi: false
    cnzz:
        id: 
        web_id: 
    cookie_consent:
        type: info
        theme: edgeless
        static: false
        position: bottom-left
        policyLink: https://www.cookiesandyou.com/
    gallery: true
    google_analytics:
        tracking_id: 
    hotjar:
        site_id: 
    katex: false
    mathjax: false
    outdated_browser: false
    progressbar: true
    statcounter:
        project: 
        security: 
    twitter_conversion_tracking:
        pixel_id: 
providers:
    cdn: jsdelivr
    fontcdn: google
    iconcdn: fontawesome
```

- highlight 
  - 代碼區塊我改成深色主題atom-one-dark，從它們提供的 [styles 檔案位置](https://github.com/highlightjs/highlight.js/tree/9.18.1/src/styles) 中找到的，預覽可以從[highlight.js demo](https://highlightjs.org/static/demo/) 看到效果．
- sidebar:
  - left/right.sticky: true 這設定可以固定左右側邊欄，閱讀時到下方時才會不會看不到
- toc 這個是文章目錄，需配合文章開啟Front-Matter才能用，預設是顯示三層，我習慣改成四層

### 新增文章
#### 文章的 Front-Matter设置

```diff
---
title: "[Blog] 使用 Hexo 撰寫部落格-04更換ICARUS主題"

+ //文章封面
cover: /img/posts/dariusz-sankowski-3OiYMgDKJ6k-unsplash.jpg 

+ //文章縮圖
thumbnail: /img/posts/dariusz-sankowski-3OiYMgDKJ6k-unsplash.jpg

+ // 文章目錄導覽
toc: true

+ // 文章標籤
tags:
  - blog
+ // 文章目錄
categories:
  - [開發相關,blog]
date: 2023-01-22 16:31:36

+ 更改某篇文章的代码高亮主题
article:
    highlight:
        theme: atom-one-dark
---
+ 這邊可以加入一些引言
Post content...
<!--more-->
Post content...
```

>Tip: 默認文章都是不開啟toc的，要手動添加在文章開頭，但網路上有教學使之預設開啟．




#### 文章插入圖片
根據這篇說明[Asset Folders](https://hexo.io/docs/asset-folders.html)，有兩種方式，一種是放在/source/images，一種是依文章分類放置．
```Bash
// 第一種方法 一定要取名images資料夾 不知道為什麼不能隨便命名
<img src="/images/icarus_init_ui.png" width="auto" />


// 第二種方法 hexo new xxx 時會有一個獨立資料夾可以放圖片
不知道為什麼我這邊是開啟
post_asset_folder: true 
permalink: ':year/:month/:day/:title/'
![icarus_init](icarus_init.png)
update link as:-->/.io//icarus_init.png
但是發現無法找到資料，推判可能是我的插件有什麼插件無法對應到日期 待查

```

---

#### 文章插入代碼

```go

//第一種可以簡單用```diff “hexo version” >folded 

//第二種放入codeblock 
{% codeblock  "config.icarus.ym" lang:diff >folded %}
{% endcodeblock %}

//可以指定是否折疊,沒指定就照預設黨
```

---------
## [後記] 過程中處理問題
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
如果下hexo clean hexo g 會發現文章會產生在public資料夾裡，以前舊的主題先刪除

```diff >folded
- 2020
- 2021
+ .....
+ public
+   2020
+   2021


```

- 插入圖片時不知道為什麼不能用與文章放置一起的設定
```
// 第一種方法 hexo new xxx 時會有一個獨立資料夾可以放圖片
不知道為什麼我這邊是開啟
post_asset_folder: true 
permalink: ':year/:month/:day/:title/'
![icarus_init](icarus_init.png)
update link as:-->/.io//icarus_init.png
但是發現無法找到資料，推判可能是我的插件有什麼插件無法對應到日期 待查

```

- 未完待續 待研究中...
```
多語言
看板娘
留言區
buymecoffee
Icarus用户指南 - 主题配置 Google Structured Data 你可以在head配置中设置Google Structured Data。 你应该在配置文件中将绝大部分配置留空。 仅在需要的时候在文章的front-matter中为这些设置赋值。


```


## 網路參考文章
- [hexo-theme-icarus](https://github.com/ppoffice/hexo-theme-icarus) github
- [Icarus快速上手](https://ppoffice.github.io/hexo-theme-icarus/uncategorized/icarus%E5%BF%AB%E9%80%9F%E4%B8%8A%E6%89%8B/)
- [Icarus用户指南 - 主题配置](http://ppoffice.github.io/hexo-theme-icarus/Configuration/icarus%E7%94%A8%E6%88%B7%E6%8C%87%E5%8D%97-%E4%B8%BB%E9%A2%98%E9%85%8D%E7%BD%AE/#%E9%A1%B5%E8%84%9A)
  >Icarus的默认主题配置文件为_config.icarus.yml。 此文件定义了站点全局的布局与样式设置，同时也控制了例如插件与挂件等外部功能的配置。 本文详细介绍了本主题的一般配置，并且解释了Icarus使用哪些配置文件和它是如何生成并验证这些配置。
- [Hexo-Icarus主题配置建议](https://blog.andycen.com/2020/03/07/Hexo-Icarus%E4%B8%BB%E9%A2%98%E9%85%8D%E7%BD%AE%E5%BB%BA%E8%AE%AE/)

- [活用 Bulma 美化 Icarus 文章](https://www.imaegoo.com/2020/icarus-with-bulma)
- 圖片來源：https://unsplash.com/
