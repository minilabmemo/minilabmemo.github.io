---
title: "[React][✍練習]套用 css-in-js (Emotion 庫)撰寫 CSS"
tags:
  - react
  - css
  - css-in-js
  - ing

categories:
  - Tech.
  - Web
  - front-end
  - react
date: 2021-04-18 21:21:19
---
[✍練習ing]

> 練習React JS寫法與 css-in-js( Emotion 庫) 撰寫 CSS

<!--more-->

# 一般要在 React 中撰寫 CSS 有幾種做法

## 1.撰寫在.CSS 檔案,再 import 套用。
- 把css寫在不同檔案中
```jsx
import "./styles.css";
<div className="App">   可定義 className
```
不便性：會需要考慮CSS優先度問題
## 2.直接在對應地方用style={JS寫法} 撰寫
- 直接用 Inline-style 在屬性中加入style
```jsx
<h2 style ={{color:'red', backgroundColor: "#3f51b5"}}>JS寫法</h2>
裡面是 JS 寫法，值需加''，且-需改成駱駝式寫法(不能含-字元)
```
不便性：會需要轉成ＪＳ寫法，有插件工具可以幫忙轉

## 3.套用css-in-js 庫 直接撰寫 CSS，不用再改 JS 寫法啦
  而 css-in-js 庫的主要有: styled-components, emotion, glamorous。


# 練習用emotion庫撰寫CSS
  - Emotion 是一個旨在使用 JavaScript 編寫 CSS 樣式的庫 - 加上兩個反引號，之間就可以直接撰寫 CSS ，有styled 寫法，本篇主要用這個練習看看。 
  - styled 寫法
    要建立 < div> 標籤樣式時，使用 styled.div；如果要建立的是 < button> 則是使用 styled.button 以此類推。

## 套用emotion庫撰寫

基礎使用方法：
1. 安裝 npm install --save emotion
2. 引入用className屬性套用
```jsx
import { css } from "emotion";
const myStyle = css`
  color: rebeccapurple;
`
 <div className="myStyle ">myStyle樣式</div>

```
更多範例可以看NPM上的emotion庫介紹[emotion](https://www.npmjs.com/package/emotion)


### 套用@emotion/styled
基礎使用方法：
1. 引入npm i @emotion/styled
2. 撰寫標籤tag
```jsx
const Container = styled.div` //外面
  background-color: skyblue;
`;
...
return (
    <Container  >
     </Container >
  );
    
```
- 變數修改方法
``` jsx
let displayNone = "block"

const Modal = styled.div`
display: ${displayNone}; 
  `;
```

### 套用@emotion/core庫撰寫
官方推薦＠＠ 但使用上有一些限制

基礎使用方法：
1. 引入npm i @emotion/core
2. 引入後用css屬性套用
  ```jsx
/** @jsx jsx */ import { css, jsx } from "@emotion/core"; 
//在無法配置babel配置（create-react-app，codesandbox等）的項目中
一定要加前述/** @jsx jsx */ 才有效果喔！！！ 之前漏了查好久＠＠

定義常數， CSS 區塊要用css`` 包起來
  const TextRed = css`
    color: red;
  `;

然後在要套用的地方加上css={xxx}
  <h2 css={TextRed}>emotion css 寫法</h2>


```
更多介紹範例： [emotion Introduction](https://emotion.sh/docs/introduction "emotion Introduction") 


------
## 練習區✍
持續練習其他進階套用法並更新在範例檔案中 ex: 多重套用，階層樣式，標籤樣式...


*可側邊開啟程式碼 
（如有更好的寫法介紹還請多多指教，謝謝🙏） 

<iframe src="https://codesandbox.io/embed/emotion-css-nqey4?fontsize=14&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="emotion CSS"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>


# 開發插件 in vscode
vscode中有一些針對css-in-js的插件可以幫助開發效率．
## Css-in-js
可以透過指令將 CSS 選取後切換 css & css-in-js 寫法，不用再自己改半天啦！！

## vscode-styled-components
可以自動完成在css-in-js區塊裡面的css補全提示．


----

# 網路參考文章

| 連結  | 摘要與大致內容 |
| ----- | ----------|
| [【Day 10】CSS && Inline-style](https://ithelp.ithome.com.tw/articles/10215415 "【Day 10】CSS && Inline-style")  | React CSS && Inline-style 介紹，JS 物件寫法。 |
|[https://github.com/rtsao/csjs/wiki/How-to-apply-multiple-classnames-to-an-element](https://github.com/rtsao/csjs/wiki/How-to-apply-multiple-classnames-to-an-element)|多重classnames寫法|
| [谈一谈在 React 项目中使用 css-in-js 方案](https://juejin.im/post/6844903993047531533 "谈一谈在React项目中使用css-in-js方案") | 鉴于 emotion 已经支持了 styled 模式，可以优先选择 emotion。內涵 emotion 用法示例(進階 待看 ☐👈) |
| [[Day 14 - 即時天氣] 把 CSS 寫在 JavaScript 中！？ - CSS in JS 的使用](https://ithelp.ithome.com.tw/articles/10223071 "[Day 14 - 即時天氣] 把 CSS 寫在 JavaScript 中！？ - CSS in JS 的使用") | 使用 emotion 撰寫 styled components  |
 | [介紹撰寫 React CSS 的神套件 Styled Components](https://medium.com/@shihKai/%E4%BB%8B%E7%B4%B9%E6%92%B0%E5%AF%ABreact-css%E7%9A%84%E7%A5%9E%E5%A5%97%E4%BB%B6styled-components-77455c849198 "介紹撰寫React CSS的神套件Styled Components") | Styled Components sample |
[emotion Composition](https://emotion.sh/docs/composition)|套用兩個樣式寫法  |
https://stackoverflow.com/questions/53803466/what-does-the-comment-jsx-jsx-do-in-the-emotion-css-in-js-library | 解釋要在import前加上/ ** @jsx jsx * /的原因|
|https://emotion.sh/docs/css-prop#jsx-pragma |在文件頂部設置jsx編譯指示才可以使用css prop。尤其在無法配置babel配置（create-react-app，codesandbox等）的項目中。|
[change-style-of-material-ui-textfield](https://stackoverflow.com/questions/61414356/change-style-of-material-ui-textfield-on-focus-react)|更改material-ui樣式的發問 
[Why you shouldn't use @emotion/core](https://vriad.com/essays/emotion-core-vs-vanilla-emotion)|有一篇文章分析不應使用emotion/core的原因




