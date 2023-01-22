---
title: "[Blog] 使用 Hexo 撰寫部落格 03 - 外部資源/插件設定"
tags:
  - hexo
  - blog
  - google_analytics
categories:
  - [開發相關,blog]
date: 2022-02-03 10:06:30
---

> 外部也有一些插件與資源可以幫助部落格更加豐富，本篇記錄用到的外部插件使用方式．
<!--more-->

## 外部資源/插件設定

### 標籤雲

1.安裝插件

```
npm i hexo-tag-cloud --save
```

2.配置主網站\_config.yml
要注意不要改錯檔案，不然可以看到標籤雲卻改不了樣式

```
# hexo-tag-cloud 標籤雲：see https://github.com/MikeCoder/hexo-tag-cloud
tag_cloud:
  textFont: Trebuchet MS, Helvetica # 字体
  textColor: '#869ABF' # 字體颜色
  textHeight: 12 # 字體高度
  outlineColor: '#FFCFAB' # 字體背景色
  maxSpeed: 0.1 # 標籤雲最大移動速度
  pauseOnSelected: true # true 選中時停止移動
```

3. 修改主題側邊欄的語言內容
   以 NexT 主题為例修改 layout/\_macro/sidevar.swig 文件中在 sidebar-inner 新增

```
>if site.tags.length > 1 %}
<script type="text/javascript" charset="utf-8" src="{{ url_for('/js/tagcloud.js') }}"></script>
<script type="text/javascript" charset="utf-8" src="{{ url_for('/js/tagcanvas.js') }}"></script>
<div class="widget-wrap">
    <div id="myCanvasContainer" class="widget tagcloud">
    <canvas width="220" height="250" id="resCanvas" style="width=100%">
        {{ list_tags() }}
    </canvas>
    </div>
</div>
>endif %}

```

4. 作者 git 上的 Readme 說明 [by version 2.1.2]
   建議可以關注 https://github.com/MikeCoder/ 說明動作操作

```
完成安装和显示，可以通过 hexo clean && hexo g && hexo s 来进行本地预览, hexo clean 为必须选项。
**PS:不要使用 hexo g -d 或者 hexo d -g 这类组合命令。**详情见: Issue 7
```


### 新增Google Analytics 流量分析
Google分析是一個由Google所提供的網站流量統計服務。Google 分析現在是網際網路上使用最廣泛的網路分析服務。

（雖然這部落格只是用來來自己筆記的，流量應該很少，但想要用來玩玩看google的分析網站而試試）

#### 1.註冊 google analysis
這邊我註冊了一個帳戶名（yume），資源名稱為hexo_blog，名稱之後都可以更改，接著填寫一些想要分析的內容與目的等等，完成後就會得到一個資源，也會有資源ID（但這不是我們要的），點入該新建的資源後，再新增一個資源串流，就可以得到評估ＩＤ了．

##### 代碼設定操作說明
這邊提供了兩種方式說明：
- 1.新增網頁內代碼，全域網站內有說明如果在網站上head區塊加入代碼範例或是使用google代碼管理工具．
- 2.使用現有的網頁內代碼：內有提到gtag.js與你的評估ID資訊．

#### 2.修改hexo的主題設定檔
由於目前我用的主題已經有現有的相關代碼設定，因此只要在上面拿到的評估ID，貼到主題設定檔中的app_id裡就可以了．

```yml themes/next-reloaded/_config.yml
# Google Analytics
google_analytics:
  tracking_id: # <app_id>
  # By default, NexT will load an external gtag.js script on your site.
  # If you only need the pageview feature, set the following option to true to get a better performance.
  only_pageview: false
```

- 當然有的時候會遇到不失效的問題，網路有說有的代碼會去判斷主設定檔的hostname與github 是否
```
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: https://minilabmemo.github.io/
```

#### 最終效果
網路上可說可以在剛剛的分頁按下測試，但發現並沒有，且一直出現過去48小時並未收到資料，
不過實際瀏覽可以看到分析結果喔!!
![GA.png)](/images/GA.png)


## 參考文章
- [Hexo 添加标签云](https://www.jianshu.com/p/2bb36378045d)
- [Hexo 加上 Google analysis](https://op30132.github.io/2019/12/27/hexo-google-analysis/)
- [Hexo的Next主题中配置Google Analytics之后不生效的问题](https://iamlay.com/2020/06/27/HexoGoogleAnalytics/)
- [Hexo fluid 中关联 Google Anlytics 的具体方法](https://zhuanlan.zhihu.com/p/338903685)
