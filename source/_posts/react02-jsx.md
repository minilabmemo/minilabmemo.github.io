---
title: "[React 02] react JSX 基本語法"
tags:
  - react
  - JSX
  - Babel
categories:
  - Tech.
  - Web
  - front-end
  - react
date: 2020-05-30T18:32:15+08:00
---

{% note info %} 上一篇已建立一個基本專案，開始可以對index.js做一些改寫練習，並使用JSX語法 {% endnote %}


<!--more-->

# JSX 
看起來是html與ＪＳ混合使用，比較接近 JavaScript 而不是 HTML，ＪＳＸ允許你使用 JavaScript 所有的功能。
- Ref :https://zh-hant.reactjs.org/docs/introducing-jsx.html

## html 區域
剛剛產生的public/index.html，含有基本HTML範本id="root"的div區塊<br>
```
"<div id="root"></div>"
```
------------


## React 中的 JSX 區域
接著看一下src/index.js裡的程式碼

### 基本範例: 直接撰寫html
```javascript
ReactDOM.render(<App />, document.getElementById('root'));

或是改成
ReactDOM.render(
  <h1> Hello world!</h1>,
document.getElementById('root'));
```
解說：
- 由 React DOM 函式將元素渲染 ROOT 這個DOM 節點中
- 而將 html當參數傳遞是使用一種Javascript語法: JSX
```
const name = 'Josh Perez'; //一般javascript
const element = <h1>Hello, {name}</h1>;//混和的html與字串 特殊JSX語法

ReactDOM.render(
  element,
  document.getElementById('root')
);

```

#### 關於Babel
 是JavaScript 前處理器，編譯器，主要能轉換JSX與ES6成各瀏覽器支持的ＪＳ
```
const element = (
  <h1 className="text">
    Hello, World!
  </h1>
);
```
Babel 將 JSX 編譯為呼叫 React.createElement() 的程式。
```
const element = React.createElement(
  'h1',
  {className: 'text'},
  'Hello, World!'
);
```
------------
### 範例: 在html中可以用{JS} 表達式崁入變數

```javascript
//js函式宣告或是變數宣告區
const styleRed = { color: 'red' };
const pic=()=>{ //html語法可以當作參數傳遞
  return (
  <div><img src="https://picsum.photos/200/200?image=229" alt="" class="circle-profile"/></div>);
}
var arr = [
        <h1>REACT學習</h1>,
        <h2>如何使用JSX！</h2>,
];

ReactDOM.render(
<React.StrictMode>
   <h1 style = { styleRed } > Hello, world! </h1>
   <div>{ pic()} </div> {/*註解這樣寫*/}
   <div>{arr}</div>,{/*可以放入數組*/}
 </React.StrictMode>,
    document.getElementById('root')
);

- 可在 html 標籤中利用 {} 寫 javascript 表示式
- 其中style = {{ color: 'red' }} 這樣的表示也可以。
```


### 範例: 帶入屬性命名與Event
```javascript
const getValue=(event)=>{
  console.log(event.target.value)
}
ReactDOM.render(
<React.StrictMode>
    <h1 className = "title" > Hello, world! </h1>
	 <button value onClick={getValue}>按下以取得數值 </button>
    <button value={true} onClick={getValue}>按下以取得數值 </button>
</React.StrictMode>,
    document.getElementById('root')
);
```
- 駱駝式命名
	- class 要用 className 然後可以在 style.css中更改樣式
	- onclick 也要改onClick{函數名稱} 駱駝式命名
	- 實測命名打錯 console 會出現報 Warning: Invalid DOM property `class`. Did you mean `className`?
- 輸入類的元件button/input/textarea互動事件觸發時，函式只會接收到一個event類別的參數，並不能傳遞其他參數
- 布林=true 的屬性值可以不寫

### 範例 JSX引入Inline-style
```
export default function App() {
  return (
    <div className="App" style={{
      color: 'blue',fontSize:'19px'
    }}>
    </div>
  );
}

```
- 在style內的是ＪＳ物件也可以把他們只給一個const變數
- 內容與css不同的是必須是小寫駱駝且去除'-'
- 這種寫法的缺點是不行用hover等特殊效果，需利用其他模組化stylr寫法





# 網路參考文章
{% note warning %} <span style="font-size: 9px;">
學習路上感謝網路大神們，如果你發現了我，可以查看參考文章了解更多概念👇👇👇
</span>{% endnote %}
- [【React.js入門 - 06】 JSX](https://ithelp.ithome.com.tw/articles/10216468)
- [React篇: JSX語法撰寫指引](https://eyesofkids.gitbooks.io/react-basic-zh-tw/content/day18_deeper_jsx/ "React篇: JSX語法撰寫指引")