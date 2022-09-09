---
title: '[✍練習][🚧進行中][react] 使用ramda整理資料'
tags:
  - react
  - ramda
  - map
  - ing
categories:
  - Tech.
  - Web
  - front-end
  - react
date: 2020-10-01 16:20:06
---

> ramda 一款實用的 JavaScript 函數编程库



<!--more-->

## 安裝 ramda

\$ npm install ramda

## 使用

import \* as R from "ramda";

### 過濾資料

```
const datas = [
  {
    name: "Cupcake",
    pri: 1,
    status: "OPEN",
    type: "blog",
    protein: 4.3
  },
  {
    name: "Donut",
    pri: 2,
    status: "OPEN",
    type: "go",
    protein: 4.9
  },]

找出所有datas.name="Cupcake"的資料
let f = R.filter(R.propEq("name", "Cupcake"), datas);


```

## 延伸用法介紹

### JavaScript 的 map() function
Array.prototype.map()map() 方法會建立一個新的陣列，其內容為原陣列的每一個元素經由回呼函式運算後所回傳的結果之集合。
[Array.prototype.map()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

### react 列表與 Key
含index 輸出介紹範例
[react lists-and-keys](https://zh-hant.reactjs.org/docs/lists-and-keys.html)

👇👇👇未完待續 您可以拉到底部先看參考文章👇👇👇

---

### 練習區 ✍

- 持續練習並更新



<iframe src="https://codesandbox.io/embed/reactramda-qvjp4?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="react_ramda"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

{% note class_name %} ## 網路參考文章 {% endnote %}

[官方文檔](https://ramdajs.com/)
[中文官方文黨](https://ramda.cn/)
[Display JSON Data in React JS](https://www.golangprograms.com/display-json-data-in-reactjs.html)
[Ramda,从开始到重构](http://quanweili.com/2016/12/18/ramda-beginning-to-refactor.html)
