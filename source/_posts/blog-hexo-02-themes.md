---
title: "[Blog] 使用 Hexo 撰寫部落格 02- 更換主題編寫與個人化設定"
tags:
  - hexo
  - blog
toc: true
categories:
  - [開發相關,blog]
date: 2022-05-01 10:06:30
---

> 上一篇已經建立好基本網站架構了，這篇收集本站所有更改主題為NextT及更換的個人化設定．

#### 效果
<img src="/images/next-home.png" width="200px" />
<img src="/images/next_post.png" width="200px" />
<img src="/images/next_tags.png" width="200px" />

<!--more-->

### 更換主網站設定檔

主網站設定檔位置：/your folder/\_config.yml，可以在此編輯基本網站說明．

```
title: '程式筆記
subtitle: ' Ｍemo '
description: ''
keywords:
author: xxx
language: zh-TW
語言可以改為繁體中文，但對應顯示語言可以在以下位置修改：
/your folder/themes/next-reloaded/languages/zh-TW.yml
```

#### 更換主題

- Hexo 預設主題是 landscape

- 想要更換主題依下列步驟即可：

1. 在 hexo 網站上挑選主題：https://hexo.io/themes/
2. 然後依照教學 ~~clone 對方的主題到自己的 theme 資料夾(通常都有 git 指令，在自己資料夾照下即可)~~
- 20220405更新 使用fork對方的主題庫到自己的庫，然後用submodule進theme資料夾
3. 修改主網站設定\_config.yml 來更換


---
##### 部署修改紀錄 （可跳至最後一步）


- 本部落格採用 Next，它是一個相當熱門的主題,且有很多中文文檔說明，我也是看了範例網站，真的太喜歡才決定架 hexo 的，紀錄操作步驟如下．

- (`嘗試1:啟動失敗`)>label danger@失敗 %} 更換主題

  1. git clone https://github.com/iissnan/hexo-theme-next themes/next:

  2. config.yml 換成 theme：next，但是啟動 hexo s 後，開啟的網站卻是亂碼參數頁面＠＠
     啟動畫面也出現以下訊息：

```
WARN  ========================= ATTENTION! ==========================
  ===============================================================
WARN   NexT repository is moving here: https://github.com/theme-next
  ===============================================================
WARN   It's rebase to v6.0.0 and future maintenance will resume there
 ===============================================================
```

原因應該是找到的文章教學，clone 來源太舊了？改參考官方更新步驟[从 NexT v5.1.x 更新](https://github.com/theme-next/hexo-theme-next/blob/master/docs/zh-CN/UPDATE-FROM-5.1.X.md "从 NexT v5.1.x 更新")

- （`嘗試2:啟動成功 但曾經部署網站成功後來失敗`)>label danger@失敗 %} 試著更換主題

1. Clone v7.8.0 最新的倉庫（如放在 next-reloaded）：
   $ git clone https://github.com/theme-next/hexo-theme-next themes/next-reloaded
   （v.5.1.4）
2. 在 Hexo 的主配置文件中设置主题：
   theme: next-reloaded
3. 重新開啟就正常了

- `嘗試3:成功`) >label success@現況Ｖ %} 2022 04 發現部署後 網站一直沒有更新，部署上傳後會跑部署流程，正常會有綠色勾勾，但某次之後都是紅色勾勾，點擊發現一直沒有辦法找到submoudule themes/next-reloaded
 - 排查過程：蠻奇怪的，不太懂沒有用到submoudule，不知道是不是殘留，部署的源碼也有看到theme/next-reloaded的連接．
  1. 決定用fork方式一份自己的主題[my-hexo-theme-next)](https://github.com/minilabmemo/my-hexo-theme-next)，並用submoudule加入
 ```
 git submodule add https://github.com/xxx/my-hexo-theme-next.git themes/my-hexo-theme-next
 ```
  2. 然後砍掉其他不要的主題，另外發現.deploy_git裡面有殘留theme/next-reloaded...等東西，就直接把.deploy_git資料夾整個砍掉，重新跑就部署成功了． （這時會發現.deploy_git跟上傳的檔案裡面都沒有theme中奇怪的next-reloaded的連接）


>之後想更換別的主題也是這樣喔


### 主題設定

主題設定位置：/hexo-web/themes/next-reloaded/\_config.yml

#### 更換 NexT 版面風格

```
NextT 提供不同風格可以更換
#scheme: Muse 選單在上方
#scheme: Mist 選單在上方
scheme: Pisces 選單在側邊
```

#### 新增文章標籤與分類

1. 新增標籤與分類頁面

```
hexo new page tags
hexo new page categories
=====
index.md
---
title: categories
date: 2021-01-11 17:25:08
type: "categories"

```

2. 為文章加上 Tag 與 categories
   在\_posts/xxx.md 文章上方新增，差別在於標籤是並行的標示，而分類會有階層式關係．

```
---
title: 使用Ｈexo 撰寫部落格
tags:
  - Testing
  - Another Tag

比較特別以下這種寫法代表階層關係Web->blog
categories:
  - Web
  - blog

或是多分類表示法：代表Diary->Food...
categories:
- [Diary, Food]
- [Diary, Games]
- [Life]
---
```

3. 開啟menu頁面(側邊欄)

```yaml _config.yml
# Usage: `Key: /link/ || icon`
# icon 也可以自由置換 https://fontawesome.com/v4.7.0/icons/
menu:
  home: / || fa fa-home
  categories: /categories/ || fa fa-th
  archives: /archives/ || fa fa-archive
  tags: /tags/ || fa fa-tags
  about: /about/ || fa fa-user
```

#### 新增個人頁面

1. 新增關於我頁面

```
hexo new page about
```

2. 編輯頁面內容
   [your folder]/source/about/index.md

```
---
title: About Me
date: 2020-09-06 13:53:06
---
bla bla bla bla...
```

3. 開啟頁面

```
_config.yml
# Usage: `Key: /link/ || icon`
# icon 也可以自由置換 https://fontawesome.com/v4.7.0/icons/
menu:
  home: / || fa fa-home
  categories: /categories/ || fa fa-th
  archives: /archives/ || fa fa-archive
  tags: /tags/ || fa fa-tags
  about: /about/ || fa fa-user
```

#### 文章中顯示引言 (標籤外掛（Tag Plugins）)

```
有分號的上下引言，兩種皆可
<!-- 标签 方式，要求版本在0.4.5或以上 -->
>centerquote %}blah blah blah>endcenterquote %}
<!-- 标签别名 -->
blah blah blah

單純的置中引言
<!-- HTML方式: 直接在 Markdown 文件中编写 HTML 来调用 -->
<!-- 其中 class="blockquote-center" 是必须的 -->
<blockquote class="blockquote-center">blah blah blah</blockquote>

顯示效果在本文開頭喔

```

#### 文章中程式碼區塊

##### 更改主題 
/themes/next-reloaded/_config.yml

```
  highlight_theme: night
  # Add copy button on codeblock
  copy_button:
    enable: true
    # Show text copy result.
    show_result: true
    # Available values: default | flat | mac
    style: default
```

##### 標籤外掛（Tag Plugins）
```go
依序為 語言 左上標題 右上網址 網址名稱
>codeblock lang:go terminal https://minilabmemo.github.io/ 完整程式碼 %}
go xxx
>endcodeblock %}

\\ Backtick Code Block
```go  terminal https://minilabmemo.github.io/ 完整程式碼
```diff
- 
+ 
```
- codeblock效果
>codeblock lang:go terminal https://minilabmemo.github.io/ 完整程式碼 %}
go xxx
>endcodeblock %}

- Backtick Code Block效果
```golang terminal https://minilabmemo.github.io/ 完整程式碼
go xxx
```
- diff效果
```diff
- go xxx
+ go xxx
```

#### 文章開頭標記

```
>note class_name %} Content (md partial supported) 
其中class_name可不設或是改成下方關鍵字
```

>note class_name %} Content (不設定) 淡灰色 

>note default %} 灰色 default 

>note primary %} 紫色 primary 

>note success %} 綠色 success 

>藍色 info 

>note warning %} 黃色 warning 

>note danger %} 紅色 danger 

主題\_config 文件配置关键字：note，可修改成想要的風格

```
note:
  # Note tag style values:
  #  - simple    bs-callout old alert style. Default.
  #  - modern    bs-callout new (v2-v3) alert style.
  #  - flat      flat callout style with background, like on Mozilla or StackOverflow.
  #  - disabled  disable all CSS styles import of note tag.
  style: flat
  icons: true
  # Offset lighter of background in % for modern and flat styles (modern: -12 | 12; flat: -18 | 6).
  # Offset also applied to label tag variables. This option can work with disabled note tag.
  light_bg_offset: 0
```

#### 標籤標注
>label info@標示藍色底色 %}
>label warning@標示黃色底色 %}
>label danger@標示danger底色 %}
```
>label info@標示藍色底色 %}
>label warning@標示黃色底色 %}
>label danger@標示danger底色 %}
```

#### 文章中貼上圖片

```

放置圖片在/your folder/themes/next-reloaded/source/images
貼上相對路徑
![my](/images/avatar_memo.png)
或是用html寫法，可以控制大小
<img src="/images/avatar_memo.png" width="150px" />

```

#### 開啟文章與網站訪問數字

```
主題內建不蒜子計數器
_config.yml
busuanzi_count:
  enable: true
  total_visitors: true
  total_visitors_icon: fa fa-user
  total_views: true
  total_views_icon: fa fa-eye
  post_views: true
  post_views_icon: fa fa-eye

本地預覽時底部訪問人數與總訪問的數字會異常大，這是正常现象
只需要部署至雲端即可恢復正常
```

#### 在標頭放上可愛的 git 連結

```
_config.yml
github_banner:
  enable: true
（本部落格右上角範例）
```

#### 顯示部落格作者照片

```
_config.yml
avatar：圖片網址
```

#### 放上個人社群連結

```
social
可自由新增
```

#### 顯示閱讀進度百分比

```
back2top:
  enable: true
  # Back to top in sidebar.
  sidebar: false 顯示在右下角 true代表顯示在側邊欄
  # Scroll percent label in b2t button.
  scrollpercent: true 顯示百分比
```


### 個人化設定

#### 預設新增文章模板

修改 /scaffolds/post.md 新增自己預設內容

```
---
title: {{ title }}
date: {{ date }}
tags:
categories:
---
blabla..... 前言
<!--more-->
```

意外發現的方法，藉由這樣修改 hexo new post 時就可以把基本的設定加好了


### 參考文章
- [NextT 開始使用](https://theme-next.iissnan.com/getting-started.html)
- [NextT 主题配置](https://theme-next.iissnan.com/theme-settings.html)
- [NextT 內置標籤](https://theme-next.iissnan.com/tag-plugins.html)
- [Hexo 个人博客 NexT 主题设置 Scheme 外观](https://blog.csdn.net/mqdxiaoxiao/article/details/92843057?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.channel_param)
- [hexo 页脚添加访客人数和总访问量](https://chrischen0405.github.io/2018/09/11/post20180911/)
- [【Hexo插件系列】 常用tag](https://blog.eson.org/pub/fc959554/)

#### deploy
- [在 hexo 中使用 git submodules 管理主題](https://www.gushiciku.cn/pl/2Vvn/zh-tw)
- [用Github Pages+Hexo搭建博客之(七)如何删除一篇已经发布的文章 #成功解决：同时删除掉.deploy_git文件夹](https://blog.csdn.net/qq_34243930/article/details/109046120)