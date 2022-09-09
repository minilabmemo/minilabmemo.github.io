---
title: '[deploy]將網頁程式部署到heroku運行'
tags:
  - heroku
  - deploy
  - GUI

categories:
  - Tech.
  - deploy
  - heroku
date: 2020-09-18 10:46:22
---

 <blockquote class="blockquote-center">
Heroku是一個支援多種程式語言的雲平台即服務，免費版提供每個月平台550小時時間，但每 30 分鐘未使用都會休眠一次，需等待他從休眠時間中甦醒，時間大約 30 秒左右．</blockquote>

<!--more-->

## 註冊 heroku

- 先上官網註冊一個帳號

## 安裝 heroku CLI

參考：https://devcenter.heroku.com/articles/heroku-cli#download-and-install

- 安裝

```
  ➜  testmemooo git:(master) heroku version
 ›   Warning: heroku update available from 7.40.0 to 7.43.0.
heroku/7.40.0 darwin-x64 node-v12.16.2
➜  testmemooo git:(master) npm install -g heroku
/usr/local/bin/heroku -> /usr/local/lib/node_modules/heroku/bin/run
+ heroku@7.43.0
added 788 packages from 316 contributors in 54.332s
➜  testmemooo git:(master) heroku version
heroku/7.43.0 darwin-x64 node-v10.16.3
```

- 登入
  heroku login

- 查看每個月使用多少時間

Account Setting->Billing-> Free Dyno Usage

### 部署 React

#### 方式一：兩分鐘 0 配置快速部署

- 官方已先配置好並照說明指令輸入即可
  [Deploying React with Zero Configuration](https://blog.heroku.com/deploying-react-with-zero-configuration)

```
npm install -g create-react-app
create-react-app '自命名專案'
cd '自命名專案'
git init
heroku create -b https://github.com/mars/create-react-app-buildpack.git
git add .
git commit -m "react-create-app on Heroku"
git push heroku master
heroku open
```

其中中間那一句 heroku create 會在剛剛的網站上新增一個 damp-stream-02723 專案
最後一句是開啟網站：
https://damp-stream-02723.herokuapp.com/
這樣就看到網站了，命名應該是隨機的，但實際測試可以透過以下方式改名

- 更換專案名稱
  登入該網站後直接在專案上改名字
  之後要回到專案上改 git 上傳的位置
  [update git remote](https://devcenter.heroku.com/articles/renaming-apps#updating-git-remotes)

```
使用指令git remote rm heroku刪除舊有的 remote ‘heroku’
➜  demomemooo git:(master) git remote rm heroku

使用heroku指令綁定heroku git:remote -a newname

➜  demomemooo git:(master) heroku git:remote -a demomemooo
 ›   Error: Couldn't find that app.
 ›   Error ID: not_found
這邊會失敗是因為當時還沒有在網站上更名
➜  demomemooo git:(master) heroku git:remote -a demomemooo
set git remote heroku to https://git.heroku.com/demomemooo.git
```

https://demomemooo.herokuapp.com/

小提醒：之後如果要更新記得先在本地起看看，並且照一般在 vscode 操作 git 上傳即可．

部署設定：
- 保護源代碼
設定GENERATE_SOURCEMAP環境變數可以使得源代碼不會出現在dev tool中顯示
add into package.json:
```
"scripts": {    
    "start": "react-scripts start",
    "build": "GENERATE_SOURCEMAP=false react-scripts build",
}
```

## 現有專案上傳

```
cd '現有專案'
heroku create -b https://github.com/mars/create-react-app-buildpack.git
專案內容看不到有什麼變化＠＠ 但本地專案會多連接一個heroku遠端git連結
遠端heroku網站上一樣會多一個隨機命名的專案被建立．
git push heroku master
上傳，會直接執行build/deploy，等待它完就可以了．
heroku open
```

#### 方法二 自行建立設定

- 先建立 React 命名 testdemooo

```
create-react-app testdemooo
```

- 進入後 按 New->Create New App 輸入命名新增一個專案
  (ex testdemooo)

- 產生完會有部署指令，照做即可

```
新的 Git repository 需做

$ cd my-project/
$ git init
$ heroku git:remote -a testmemooo


針對已存在Git repository，簡單新增“ heroku remote

$ heroku git:remote -a testmemooo
```

- 但這樣做打開網站會錯誤，以下面文章的最佳解答照做即可
  [React 專案佈署 heroku 問題](https://ithelp.ithome.com.tw/questions/10198600)
  大致上做法是自行建立 server.js 與產生 build，只需要推 build 檔案上去即可（記得 gitignor 要拿掉 build folder）
  



{% note class_name %} ## 網路參考文章 {% endnote %}

- [Deploying create-react-app project isn't uglifying my code](https://stackoverflow.com/questions/58359500/deploying-create-react-app-project-isnt-uglifying-my-code)
- [React Create Script 2.0 減少維護環境配置](https://linyencheng.github.io/2019/02/27/react-create-script-2/)