---
title: "[Blog] 使用 Hexo 撰寫部落格-04更換ICARUS主題"
cover: /img/posts/dariusz-sankowski-3OiYMgDKJ6k-unsplash.jpg
thumbnail: /img/posts/dariusz-sankowski-3OiYMgDKJ6k-unsplash.jpg
tags:
  - blog
  - hexo
toc: true
categories:
  - [技術工具,blog]
date: 2023-01-22 16:31:36
---



<article class="message is-info"><div class="message-body">
2023年新的一年，突然想要來幫部落格換個新主題，這陣子看到 ICARUS 主題，覺得蠻喜歡它的版面配置的，於是就把主題換一下，目前的環境已經裝好hexo了，這篇就直接從更換主題開始～<
</div></article>
<!--more-->


{% raw %}<div class="notification is-warning">{% endraw %}
更換主題注意事項：原本有一些主題特殊的標籤或是插件及文章內容有可能會發生失效或排版混亂，更換後需要再花時間修正過去的功能．
{% raw %}</div>{% endraw %}


## 目錄
<!-- toc -->

## hexo 版本 與相依設定
使用 hexo version 可以查詢版本
```diff “點我查看hexo version ” >folded 
+ $ hexo -v
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
hexo: 6.3.0
hexo-cli: 4.3.0
os: darwin 22.2.0 13.1

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
    "version": "6.3.0"
  },
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
    "hexo-log": "^3.2.0",
    "hexo-pagination": "^2.0.0",
    "hexo-renderer-ejs": "^1.0.0",
    "hexo-renderer-inferno": "^0.1.3",
    "hexo-renderer-marked": "^3.0.0",
    "hexo-renderer-stylus": "^2.0.0",
    "hexo-server": "^2.0.0",
    "hexo-tag-cloud": "^2.1.2",
    "hexo-theme-landscape": "^0.0.3"
  },
  "devDependencies": {}
}

```

## 更換主題

### 執行安裝指令 - 安裝位置
安裝時有兩種安裝方式  see [Getting Started with Icarus](https://ppoffice.github.io/hexo-theme-icarus/uncategorized/getting-started-with-icarus/)
1. install from source
```
git clone https://github.com/ppoffice/hexo-theme-icarus.git themes/icarus --depth 1

```
1. install from NPM
```
npm install -S hexo-theme-icarus hexo-renderer-inferno
```

<article class="message is-info"><div class="message-body">
Note:一開始我是用第二種安裝方式就裝起來了，不過看起來hexo-theme-icarus會出現在node_modules裡，不是在自己的themes/icarus
兩種方式都可以正確套用到主題效果，不過考慮到之後可能自己會想改主題底層效果當作自己的部分，後來改用第一種方式安裝．

20230319 更新，後來使用補丁，又改用第二種方式，這邊就依使用習慣即可．

</div></article>


- 執行
```
$ hexo config theme icarus
然後執行hexo s 就可以了
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
+    busuanzi: true
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
#### logo
logo可以放置自己的圖片，svg檔案或png檔案都可以．
#### highlight 
  代碼區塊我改成深色主題atom-one-dark，從它們提供的 [styles 檔案位置](https://github.com/highlightjs/highlight.js/tree/9.18.1/src/styles) 中找到的，預覽可以從[highlight.js demo](https://highlightjs.org/static/demo/) 看到效果．
#### sidebar
  left/right.sticky: true 這設定可以固定左右側邊欄，閱讀時到下方時才會不會看不到
#### toc 
   這個是設定出現在部落格側邊的文章目錄，需配合文章開啟Front-Matter才能用，預設是顯示三層，我習慣改成四層．
#### plugins
      busuanzi: true 這是開啟網站底部及和每篇文章頭部，顯示共多少訪客的開關，上線後數字才會正常．

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
  - [技術工具,blog]
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


<article class="message is-success"><div class="message-header">Tip
</div><div class="message-body">
默認文章都是不開啟toc的，要手動添加在文章開頭，但網路上有教學使之預設開啟．或者你也可以加入到文章模板中．
</div></article>


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




## 魔改 theme 主題樣式
有時候套用主題，可能會有些地方格式想要調整，就要去更改底層主題的檔案，另外，這邊的更改發布之後，可能會需要清除 cache 才能看到效果．
### 更改 header logo 高度
- 因為自己的logo 內容較多，上傳時發現會被自動縮小，為了清楚顯示，所以我把高度調高了，
``` themes/icarus/include/style/base.styl
$logo-height ?= 5rem
```

<article class="message is-warning"><div class="message-header">Warning
</div><div class="message-body">
這邊要注意圖片是否會模糊（雖然在電腦檔案中看來正常），要設定適當的大小，或是換成svg檔案試試．
</div></article>

### 更改卡片懸浮效果
這個教學是來自 [挂件卡片增加浮动效果](https://astrobear.top/2021/08/23/Hexo%E4%B8%BB%E9%A2%98Icarus%E7%9A%84%E8%87%AA%E5%AE%9A%E4%B9%89/#%E6%8C%82%E4%BB%B6%E5%8D%A1%E7%89%87%E5%A2%9E%E5%8A%A0%E6%B5%AE%E5%8A%A8%E6%95%88%E6%9E%9C)

```diff include/style/card.styl 當滑鼠移到卡片上時添加陰影及上移效果
.card
+    &:hover
+        box-shadow: 0 6px 15px rgba(0,0,0,0.15), 0 0 1px rgba(0,0,0,0.1)
+        transform: translateY(-3px);
```

```diff source/js/animation.js 加上陰影漸變動畫效果
.card
-            element.style.transition = 'opacity 0.3s ease-out, transform 0.3s ease-out';
+            element.style.transition = 'opacity 0.3s ease-out, transform 0.3s ease-out, box-shadow 0.3s ease-in-out';
         });
-                    element.style.transition = 'opacity 0.3s ease-out, transform 0.3s ease-out';
+                    element.style.transition = 'opacity 0.3s ease-out, transform 0.3s ease-out, box-shadow 0.3s ease-in-out';
                 }, i * 100);
```



---------
## [後記] 過程中處理問題

{% raw %}<div class="notification is-warning">{% endraw %}
這個段落是用來記錄過程中遇到的問題，如果你沒有遇上問題可以直接跳過這個章節．
{% raw %}</div>{% endraw %}
###  安裝啟動錯誤

```
註：因為我是從NextT轉換過來的，才發現有些特殊標籤在這邊啟動會爆錯
> ：``` Error [Nunjucks Error]: about/index.md [Line 7, Column 4] unknown block tag: note```
> 因此我把文章中的找到`{%  `與`{% endnote %}`。移除．
```


- 再次啟動還是爆錯
```diff
const { Component } = require('inferno'); const classname = require('hexo-component-inferno/lib/util/classname'); const Head = require('./common/head'); const Navbar = require('./common/navbar'); const Widgets = require('./common/widgets'); const Footer = require('./common/footer'); const Scripts = require('./common/scripts'); const Search = require('./common/search'); module.exports = class extends Component { render() { const { site, config, page, helper, body } = this.props; const language = page.lang || page.language || config.language; const columnCount = Widgets.getColumnCount(config.widgets); return ; } };

// 解法因為官網github 少了hexo-renderer-inferno 用另一個月再次安裝即可
- $ npm install hexo-theme-icarus
+ $ npm install -S hexo-theme-icarus hexo-renderer-inferno
```


###  刪除舊的NextT主題預設產生位置
如果下hexo clean hexo g 會發現文章會產生在public資料夾裡，以前舊的主題先刪除

```diff >folded
- 2020
- 2021
+ .....
+ public
+   2020
+   2021


```

###   插入圖片時不知道為什麼不能用與文章放置一起的設定(尚未解)
```
// 第一種方法 hexo new xxx 時會有一個獨立資料夾可以放圖片
不知道為什麼我這邊是開啟
post_asset_folder: true 
permalink: ':year/:month/:day/:title/'
![icarus_init](icarus_init.png)
update link as:-->/.io//icarus_init.png
但是發現無法找到資料，推判可能是我的插件有什麼插件無法對應到日期 待查

```
###   highlight 主題部分無效果
  不知道為什麼除了atom-one-dark，換成別的都沒有效果．


### hexo 版本升級
一開始用的hexo版本是5.4.2，但是啟動時噴ERRROR 提示要升至hexo: 6，還有其他錯誤...，於是就一步步照著指令安裝就啟動成功了．


### 主題備份
自己有開了一個 src 分支用來記錄所有原生檔案，因為上傳只會紀錄 public 檔案，但是theme這個資料夾裡面是 git clone 別人的（theme作者），所以其實是不會出現在自己分支內的，如果有魔改theme的要記得自己在備份一下．我自己是開了一個icarus_fix_record來記錄，雖然有點麻煩，但以後要更新比較方便（或許會更新ＸＤ），如果改得太多可以考慮解除git綁定上傳整個theme．

<article class="message is-info"><div class="message-body">
20230319更新：改用補丁更新，可以看最新文章．
</div></article>

### 部署時卡住
- 1.檢查token有沒有過期
- 2.檢查上傳使用者是否錯誤
```
git config --global -l
user.name=xxx
user.email=xxx@gmail.com
credential.username=xxx
credential.helper=osxkeychain
```


### 未完待續 待研究中...
```
多語言
多階層
Submenu
https://github.com/ppoffice/hexo-theme-icarus/issues/527
看板娘
留言區
魔改SEO
buymecoffee
Open Graph
Icarus用户指南 - 主题配置 Google Structured Data 你可以在head配置中设置Google Structured Data。 你应该在配置文件中将绝大部分配置留空。 仅在需要的时候在文章的front-matter中为这些设置赋值。
https://ppoffice.github.io/hexo-theme-icarus/Widgets/icarus%E7%94%A8%E6%88%B7%E6%8C%87%E5%8D%97-%E6%8C%82%E4%BB%B6/


添加404公益页面
中文分類或標籤 tag_map

```


## 網路參考文章
- [hexo-theme-icarus](https://github.com/ppoffice/hexo-theme-icarus) github
- [Icarus快速上手](https://ppoffice.github.io/hexo-theme-icarus/uncategorized/icarus%E5%BF%AB%E9%80%9F%E4%B8%8A%E6%89%8B/)
- [Icarus用户指南 - 主题配置](http://ppoffice.github.io/hexo-theme-icarus/Configuration/icarus%E7%94%A8%E6%88%B7%E6%8C%87%E5%8D%97-%E4%B8%BB%E9%A2%98%E9%85%8D%E7%BD%AE/#%E9%A1%B5%E8%84%9A)
  >Icarus的默认主题配置文件为_config.icarus.yml。 此文件定义了站点全局的布局与样式设置，同时也控制了例如插件与挂件等外部功能的配置。 本文详细介绍了本主题的一般配置，并且解释了Icarus使用哪些配置文件和它是如何生成并验证这些配置。
- [Hexo-Icarus主题配置建议](https://blog.andycen.com/2020/03/07/Hexo-Icarus%E4%B8%BB%E9%A2%98%E9%85%8D%E7%BD%AE%E5%BB%BA%E8%AE%AE/)

- [活用 Bulma 美化 Icarus 文章](https://www.imaegoo.com/2020/icarus-with-bulma)
- [Hexo博客指南|第十二篇:Icarus配置 - 网站分析插件](https://ji2xpro.github.io/88bd6454/)
    - 不蒜子网页计数器 及其他統計插件
- 圖片來源：https://unsplash.com/
