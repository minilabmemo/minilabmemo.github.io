---
title: "[JS 02] 同步與非同步"
tags:
  - javascript
  - ES6
  - callback
  - Promises
  - aync/await
categories:
  - [Frontend,js]

date: 2021-02-20 11:33:18
---

>延續學習ＪＳ的同步與非同步概念 

☝☝本記錄為個人學習整理，如有誤還請您不吝指教，也有引用文章位置，如有問題也請告知．

<!--more-->



## 同步 vs 非同步

<img src="/images/sync_async.png" width="350px"/>



## 同步
- 一個線程是一個基本的處理過程，程序用它来完成任務。每個線程一次只能執行一个任務
- JavaScript 是一種同步的、阻塞的、單線程的语言。即使有多個ＣＰＵ，也只能在單一線程上運行多個任務，此線程稱為主線程


## 異步/非同步 用法

- 很多網頁API都使用異步代码，特别是從外部的設備來或許資源，譬如，抓取網路上文件，訪問DB，獲取影片流等等，在瀏覽器端只有一個使用者，但事件或網路要求(AJAX)要求不能阻塞其他程式的進行，通常需要等待一段時間後才會返回，所以需要讓使用者可以繼續進行目前的畫面操作．
- JS有分為同步及異步callback，setTimeout與setinterval是種異步函數。
- >label warning@而所有的同步回調函式都執行完成了，才會開始依順序執行異步的回調函式  %}。

### 異步 callbacks
異步callback(回調)其实就是函数，只不過是作為參數傳遞给那些後台执行的其他函数. 讓會造成阻塞的程式組成一個異步回調函式，先丟往一個任務佇列(task queue)先丟，當某個時間後台運行的代碼结束，就调用callbacks函数，通知你工作已经完成，

#### 什麼是callback function？
  - callback 將函數作為參數作為傳遞
  - 讓函式控制參數函式的執行時機 ex 有的情境是當A作完再作B
  - 使用上會有問題在於callback hell回呼地獄，不易閱讀 -->老派callbacks(會有回呼地獄)，新派promise

#### Promises
  - Promises 是新派的异步代码
  - 具有fetch(來源黨或url)
  - 可以有多個then(func 回乎，當前一個成功後呼叫) 
  - 其中任何一个then()块失败，则在末尾运行catch() -->避免callback hell，錯誤不是在“金字塔”的每一层单独处理。
  - 還有其他.all()...等func，Promise.all 等到全部實現（或一個拒絕）。詳細請見：[MDN-Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise)

#### aync/await
  - ECMAScript 2017 JavaScript版
  - 基于promises的语法糖，使异步代码更易于编写和阅读，讓非同步的程式碼讀起來更像在寫「同步程式碼」
  - async function 回傳的一樣是 Promise 物件，可以混合使用.then 語法
  - await 關鍵字 等待這個非同步的作業完成





``` js Promises寫法

    fetch('test.json')
        .then(response => response.json())
        .then(myData => {
            console.log(myData.name);
        })
        .catch(e => {
            console.log('catch a problem: ' + e.message);
        });
```



    
```js await/aync 寫法
async function myFetch() {
        let response = await fetch('test.json');
        let myData = await response.json();
        console.log(myData.name);

    }

    myFetch()
        .catch(e => {
            console.log('catch a problem: ' + e.message);
        });
```



```js Promises & await/aync混合用法
    async function myFetch2() {
        let response = await fetch('test.json');
        return await response.json();
    }

    myFetch2().then((myData) => {
        console.log(myData.name);
    }).catch(e => {
        console.log('catch a problem: ' + e.message);
    });;
```




## 網路參考文章

  - [MDN-异步JavaScript简介](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Asynchronous/Introducing)
  - [你懂 JavaScript 嗎？#23 Callback](https://cythilya.github.io/2018/10/30/callback/)
  - [MDN-async和await:让异步编程更简单](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Asynchronous/Async_await)
  - [MDN-response](https://developer.mozilla.org/zh-CN/docs/Web/API/Response)

