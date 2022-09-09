---
title: "[React 03] React 組件、函式與生命週期"
tags:
  - react
categories:
  - Tech.
  - Web
  - front-end
  - react
date: 2021-02-27 20:40:59
---

{% note info %} 整理react學習“個人筆記” {% endnote %}

本文內容：
- React component (組件)語法
- props 是什麼
  - ES6箭頭函式組件
- State的用法
- 生命週期


### React component (組件)語法
- component 就像是 JavaScript 的 function
- ReactDOM.render 中{函式名稱}變成了<函式名稱/> see:[Render Element](https://zh-hant.reactjs.org/docs/rendering-elements.html)
- Component 命名首字必須大寫，大寫駝峰的方式，否則 React 會把它當作一般的 HTML 元素處理，並跳出Warning提示，看到大寫駝峰命名變數時，可以知道是 React 組件而非一般函式。
- 其他 HTML 屬性、CSS 樣式屬性或一般的函式來說，則會遵行 JavaScript 以小寫駝峰來命名變數的慣例，例如在 className、maxLength、backgroundColor 等等。

----

### props 是什麼
- component 就像是 JavaScript 的 function，它接收任意的參數（稱之為「props」）並且回傳畫面的 React element。
- props 通常是不可變的(唯獨Immutable)，不能修改自己的

Ref:[Components 與 Props] (https://zh-hant.reactjs.org/docs/components-and-props.html)
<!--more-->



#### function component vs class component
接著看看兩種寫法轉換 Function 成 Class ：

##### 使用function 來做 component
- 如果需要向component傳参数，可以使用 props 對象，
- 用return (html)


````javascript function component

function HelloName(props) {
	return <h1>Hello {props.name}!</h1>;
}
ReactDOM.render(
 <React.StrictMode>
	 <HelloName name="May"/>
	</React.StrictMode>,
	document.getElementById('example')
);
````

##### 使用ES6 class來做 component
- 也可以使用ES6  class來 來定義 
- 繼承React.Component且在用render(){}包一層
- props 要改用 this.props
- 用render(){return html}

````javascript class來 component
class HelloName extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}

ReactDOM.render(
 <React.StrictMode>
	<HelloName name="May" />;,
	</React.StrictMode>,
	document.getElementById('example')
);
````



組件裡面可以再包組件，透過這樣可以重新利用
範例練習: [USER info](https://codesandbox.io/s/usercard-vh0e4 "USER info")



#### React組件 ES6箭頭函式組件 寫法
接著看看`箭頭函式語法`可以簡潔,少打很多字元
- const App: () => JSX.Element //大寫駱駝命名
- 縮寫：如果裡面只有return 可以去掉{}與return，但通常會有一些變數存在，個人習慣保留．
- 箭頭函式不可以使用於建構式，可以見[[JS 01] javascript 新手上路與概念筆記](https://minilabmemo.github.io/2021/02/20/js-start-01/)
- 使用插件快速鍵 rafc - ReactArrowFunctionComponent
[紀錄](https://github.com/minilabmemo/counter-water/commit/aea85efa5f2e4a1f073cd7c89f96a458b00ab24c)
```
const Hello = () => {
  return ( <div>hello</div> )
}
```

------



### State的用法
Props 是唯讀的(Immutable)，State 類似於 prop，但它是私有且由 component 完全控制的。當state被改變時，會進入re-render的update程序，更新畫面

#### class(setState) vs function(useState)

##### 1. 使用class來改state（setState）
- 使用 ES6 class來 來定義 
- 繼承React.Component且在用render(){}包一層
- props 要改用 this.props
- 如果想要更改props ，要改用setState
- [根據React 與 bind this](https://medium.com/reactmaker/react-%E8%88%87-bind-this-%E7%9A%84%E4%B8%80%E4%BA%9B%E5%BF%83%E5%BE%97-323c8d3d395d)
- 範例練習:透過一個新的按鈕去改變時間 [Refresh Time](https://codesandbox.io/s/refreshtime-ju4pv?file=/src/index.js "Refresh Time")


````javascript
import React from "react";
import ReactDOM from "react-dom";

import App from "./App";

const rootElement = document.getElementById("root");

class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
    // this.changeTime=this.changeTime.bind(this);
  }

  // changeTime(){
  //   this.setState({date: new Date()})

  // }
  //根據React 與 bind this

  //以上可以簡化 改箭頭含式寫法
  changeTime = () => {
    this.setState({ date: new Date() });
  };

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>现在是 {this.state.date.toLocaleTimeString()}.</h2>
        <button onClick={this.changeTime}>刷新 </button>
      </div>
    );
  }
}

ReactDOM.render(
  <React.StrictMode>
    <Clock />,
  </React.StrictMode>,
  rootElement
);


````

#### 2.使用function component更改state（用useState）
- 沒有內部狀態（State），是 Stateless Components。
- 沒有 Lifecycle Hooks 和 refs。
- 如果想要更改props 要改用useState，useState-是一個基礎的Hook，是可以在function component中使用設定state，而不需要轉換成class。
> hook意思是“鈎子”，在音樂上，指的是一首歌曲中最能鈎人的部分。Hook 是 React 16.8 增加的新功能。讓你不必寫 class 就能使用 state 以及其他 React 的功能。使用hook可以更簡化且被推崇使用。

- useState它回傳了一對值：目前的 state 跟一個可以更新 state 的 function。
- 範例改寫練習 [Refresh_Time_useState](https://codesandbox.io/s/refreshtimeusestate-xns3c?file=/src/index.js "Refresh_Time_useState")

```javascript
//1.加上useState引入
import React, { useState } from 'react';
import ReactDOM from "react-dom";

const Clock=()=>{
  // 2.宣告一個 state 變數，命名date。
  // 傳入 useState() 的參數就是 state 起始值
  const [date, changeTime] = useState(new Date());
// 3-1 return中直接寫上state變數-在 function 中可以直接使用 state
// 3-2 當使用者點擊，我們就呼叫 函式 並傳入新的值。
  return(
      <div>
        <h1>Hello, world!</h1>
        <h2>现在是 {date.toLocaleTimeString()}.</h2>
        <button onClick={()=>{changeTime(new Date())}}>刷新 </button>
      </div>
  );
}

const rootElement = document.getElementById("root");
ReactDOM.render(
  <React.StrictMode>
    <Clock/>
  </React.StrictMode>,
  rootElement
);

```


----

#### （延伸說明）hooks 與 Function Component

[使用 State Hook](https://zh-hant.reactjs.org/docs/hooks-state.html)

- 用 Function Component 代替 Stateless Component 的说法，原因是：自从 Hooks 出现，函数式组件功能在不断丰富，函数式组件不再需要强调其无状态特性，因此叫 Function Component 更为恰当。

- 從[精读《Function VS Class 组件》](https://zhuanlan.zhihu.com/p/59558396)
中可以看的使用class component,會因為使用this問題而需要修復，要follow class結構與巢狀太過雜亂，再者，而function component沒有this,如果希望拿到稳定的 props，使用 Function Component 是更好的選擇。而
- Function Component + Hooks 可以实现 Class Component 做不到的 capture props、capture value，而且 `React 官方也推荐 新的代码使用 Hooks 编写`。


-----

### 生命週期
元件被安裝時(Mount)、元件被更新時(Update)、元件被移除時(Unmount)
*註：原本想要一樣比較一下class 原本的用法，但還是直接介紹function component(useEffect)更簡潔．

#### useEffect hook

```
useEffect(() => {
    /*  componentDidMount 和  componentDidUpdate */
    return () => {
      /* componentWillUnmount */   //在 component unmount 時，React 會執行清除。
    };
    
}, [dependencies參數]); /* 是用來限定當哪些變數被改變時useEffect要觸發 */

```

Ref:
- [官方-hooks-effect](https://zh-hant.reactjs.org/docs/hooks-effect.html) 重點：
  - 內有使用class與hook 的範例對比說明
  - 很多待細讀 ＴＢＤ
  - 我們建議使用 exhaustive-deps 規則作為我們 eslint-plugin-react-hooks package 的一部分。當不正確地指定依賴時，它會發出警告，並提出修改建議。

----

### 網路參考範例:

[React State(状态)](https://www.runoob.com/react/react-state.html "React State(状态)") @runoob基礎與線上範例
**[State 和生命週期](https://zh-hant.reactjs.org/docs/state-and-lifecycle.html "State 和生命週期") @React中文React解說
[【React.js入門 - 11】 開始進入class component](https://ithelp.ithome.com.tw/articles/10219057 "【React.js入門 - 11】 開始進入class component") @IT邦幫忙的系列文
[React 與 bind this ](https://medium.com/reactmaker/react-%E8%88%87-bind-this-%E7%9A%84%E4%B8%80%E4%BA%9B%E5%BF%83%E5%BE%97-323c8d3d395d "React 與 bind this ") @medium


[React hook](https://zh-hant.reactjs.org/docs/hooks-intro.html) @React 中文解說Hook系列
[使用 State Hook](https://zh-hant.reactjs.org/docs/hooks-state.html "使用 State Hook") @React 中文解說State Hook中寫法對比
