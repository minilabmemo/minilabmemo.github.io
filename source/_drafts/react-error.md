---
title: react-error
tags:
  - error
categories:
  - Tech.
  - Web
  - front-end
  - react
date: 2021-04-01 20:19:29
---


{% note info %} 紀錄前端開發時會遇到的錯誤狀況 {% endnote %}


<!--more-->


在開發環境執行程式時，點擊某一些動作會跳一些錯誤畫面，Runtime Error就是運行時錯誤
### Babel
Babel 是 JavaScript 的編譯器用來把 ES6 的程式碼轉化為瀏覽器或者其它環境支援的程式碼。

- 參考文 babel的細節解說：[前端科普系列（4）：Babel —— 把 ES6 送上天的通天塔](https://www.mdeditor.tw/pl/pNFj/zh-tw)


 #### JSX must be wrapped in an enclosing tag.
 JSX的return，必須回傳一層的根節點，在撰寫時就會有problem提示，執行也會直接跳出紅色錯誤．
 ```
return (
    <> //要加這個 或是<React.Fragment>
      <div className="App"></div>
      <div className="App"></div>
    </> //或是</React.Fragment>
  );
 ```
 Failed to compile
{% note danger %}
 SyntaxError: xxx/src/App.js: Adjacent JSX elements must be wrapped in an enclosing tag. Did you want a JSX fragment <>...</>? (13:4)
  {% endnote %}
  
#### 錯誤修改const
```
const count = 0;
  return (
      <ActionBlock onClick={() => {
        count = count + 1;
        ....
```

{% note warning %}
 _readOnlyError
node_modules/babel-preset-react-app/node_modules/@babel/runtime/helpers/esm/readOnlyError.js
 {% endnote %}

#### hook應該寫進function component裡
```
  46 | const [count, setCount] = useState(0); //如果沒有把hook寫在下面的component裡
  47 | export default function Counter() {
```
執行後畫面會出現警語
{% note warning %}
Error: Invalid hook call. Hooks can only be called inside of the body of a function component. This could happen for one of the following reasons:
1. You might have mismatching versions of React and the renderer (such as React DOM)
2. You might be breaking the Rules of Hooks
3. You might have more than one copy of React in the same app
See https://reactjs.org/link/invalid-hook-call for tips about how to debug and fix this problem.
 {% endnote %}

#### 不小心寫出無限迴圈re-render

例如：當onclick 後的函數(沒return func.)且帶有參數值時會馬上執行，而不是點擊時執行
```
<ActionBlock onClick={handelAction(SubtractAct)} }}

正確寫法要把函示加上（）＝>包在裡面
<ActionBlock onClick={() => handelAction(SubtractAct)}
```
{% note warning %}
Error: Too many re-renders. React limits the number of renders to prevent an infinite loop.
 {% endnote %}


#### ReferenceError: dis is not defined
設定一個不存在的變數