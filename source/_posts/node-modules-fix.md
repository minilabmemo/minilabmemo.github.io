---
title: "[分享] 修改依賴源碼超省時的補丁套件"
cover: /img/posts/tools.png

tags:
  - tool
  - modules
  - hexo 
toc: true
date: 2023-03-18 11:25:44

categories:
  - [技術工具,modules]

---

<article class="message is-info"><div class="message-body">
有的時候，因為一些個人因素，或是依賴庫的檔案有問題，使你不得不去修改 node_modules 裡某個套件的源碼，或許你修正了，也發出 PR 正在等待合併，可是如果你重新使用 npm install 可能還是會拉到尚未修正的源碼，而這個補丁工具 <a href="https://www.npmjs.com/package/patch-package">patch-package</a> 可以快速解決你的問題.
</div></article>


<!--more-->
## 目錄 | Contents
<div class="my-toc">
<!-- toc -->
</div>

## 起源
因為我去改了node_modules 裡某個套件的源碼，看了網路上說明為了避免下次拉依賴庫又會被修改回來，所以你可能要自己把修正拉進自己的庫，但修改起來看了有點麻煩，文章內有提到另一個補丁工具，索性就用用看，這工具實在好用，記錄下使用過程，如果有看不懂的地方可以看這篇最下方的參考文章．


## 安裝 patch-package

```
npm install patch-package --save-dev
```
## 修正源碼 
接著你可以去改 node_modules/xxx/xxx 的檔案


## 創建補丁
```
// npx patch-package package-name
npx patch-package xxx
```
- package-name 就是你依賴的node_modules/xxx 的名字
- 執行完成會發現生成patches文件夾，裡面有修改過的文件 diff 紀錄


## 部署
- 修改package.json，新增命令 postinstall
```diff
"scripts": {
+  "postinstall": "patch-package"
 }
```
<article class="message is-info"><div class="message-body">
之後再下`npm install` 就會發現它幫你下載相依庫時又修正更改了，這真是太神奇了！
<b>（你可以刪掉相依在讓它載回來看看，記得備份）</b>
</div></article>
```diff
+ $npm install

> hexo-site@0.0.0 postinstall xx/blog/minilabmemo.github.io
> patch-package

+ patch-package 6.5.1
+ Applying patches...  //下面的檔案進行修改
hexo-insert-toc@1.1.2 ✔
audited 543 packages in 2.279s

```

## 實際應用

### hexo主題魔改
之後曾有提過我有針對主題底層更改[魔改-theme-主題樣式](https://minilabmemo.github.io/2023/01/22/blog-hexo-04-theme-icarus/#%E9%AD%94%E6%94%B9-theme-%E4%B8%BB%E9%A1%8C%E6%A8%A3%E5%BC%8F)，後來又備份自己修改的地方，想一想或許可以用這個套件修補．

- 原本架構
```
themes/icarus  //不會上傳  install from source git clone來的
themes/icarus_fix_record //自己的修改備份紀錄
```
- 改用 install from NPM
```
npm install -S hexo-theme-icarus
專案出現相依庫
"hexo-theme-icarus": "^5.2.1",

```
- 接著移除掉themes/icarus 資料夾
原本修改的地方就被恢復成原主題了

- 接著再把我備份的修改紀錄去修改node_modules/hexo-theme-icarus
```
themes/icarus_fix_record/include/style/base.styl
themes/icarus_fix_record/include/style/card.styl
themes/icarus_fix_record/include/style/helper.styl
themes/icarus_fix_record/layout/common/article.jsx
...
```
- 創建補丁 `npx patch-package hexo-theme-icarus`
  - 因為檔案會有點多，所以也可以再加上 --include ".*include.*" 讓他針對部分去修改就好
  - 完成後去生成的檔案夾確認diff，這邊也可以記錄你的修改
```
$ npx patch-package hexo-theme-icarus
patch-package 6.5.1
• Creating temporary folder
• Installing hexo-theme-icarus@5.2.1 with npm
• Diffing your files with clean files
✔ Created file patches/hexo-theme-icarus+5.2.1.patch

💡 hexo-theme-icarus is on GitHub! To draft an issue based on your patch run

    npx patch-package hexo-theme-icarus --create-issue
$ npx patch-package hexo-theme-icarus --include ".*include.*"
$ npx patch-package hexo-theme-icarus --include ".*(?:include|common).*"
```

- 重新安裝確認
你可以刪除相依再次下 `npm install`確認，但似乎用 `npm install -S hexo-theme-icarus`是沒有作用的



## 網路參考文章

<article class="message is-warning"><div class="message-body">
本篇文章內容參考如下，如有引用錯誤或須加註問題，歡迎提出喔．
</div></article>


- [修改nodejs项目中node_modules的代码，不能生效吗？](https://www.zhihu.com/question/302249432)
  - 配置webpack alias 的方法介紹 （沒用過）
- [使用 patch-package 修改第三方模块](marketplace.visualstudio.com)
  - 更多選項介紹
- [Super Easy NPM Package Patching with ‘patch-package’](https://javascript.plainenglish.io/live-npm-package-patching-with-patch-package-b8f30d47779c)

- Photo by <a href="https://unsplash.com/it/@webstacks?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Webstacks</a> on <a href="https://unsplash.com/photos/WbOR54pzvLM?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
- Photo by <a href="https://unsplash.com/@sincerelymedia?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Sincerely Media</a> on <a href="https://unsplash.com/photos/HoEYgBL_Gcs?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  