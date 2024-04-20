---
title: '[JS 筆記 01] javascript 新手上路與概念'
tags:
  - javascript
  - ES6
  - 閉包
  - 解構賦值
  - note
toc: true
categories:
  - [Frontend, js]
date: 2021-02-20 11:33:18
---

<article class="message is-info"><div class="message-body">

本章由 [MDN-JavaScript](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript) 開始著手練習，並紀錄學習重點。

</div></article>

<!--more-->

## 目錄 | Contents

<div class="my-toc">
<!-- toc -->
</div>

## JS 歷史- ES6 2015

ECMAScript 是一種由 Ecma 國際定義的手稿語言規範，它往往被稱為 JavaScript 或 JScript (維基)

- ES6 第 6 版為 ECMAScript2015，是大幅度的更新，討論度較高，
- 2022 年 6 月 ECMAScript 2022 （ES2022），第 13 版

---

## 宣告與各用法概念

### 命名規則

- 小寫駱駝
- 大小寫相異(敏感)
- 有意義的名字

ref:[关于变量命名的规则](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/First_steps/Variables#%E5%85%B3%E4%BA%8E%E5%8F%98%E9%87%8F%E5%91%BD%E5%90%8D%E7%9A%84%E8%A7%84%E5%88%99)

### 變數

- 宣告變數但不賦值 = undefined （不知道值）
- 未宣報變數是 is not defined
- null 常見於宣告後面定義成沒有值或找不到
- 全域屬性 NaN 表示「非數值」（Not-A-Number）的數值
  - NaN 不等於（==、!=、===、!==）任何值，包括 NaN 本身。請使用 Number.isNaN() 或 isNaN() 來確認某個數值是否為 NaN。

#### var

- [var 与 let 的区别](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/First_steps/Variables#var_%E4%B8%8E_let_%E7%9A%84%E5%8C%BA%E5%88%AB)
- [let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
- [NaN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/NaN)

<blockquote class="instagram-media" data-instgrm-permalink="https://www.instagram.com/p/CyPmdp3SDLb/?utm_source=ig_embed&amp;utm_campaign=loading" data-instgrm-version="14" style=" background:#FFF; border:0; border-radius:3px; box-shadow:0 0 1px 0 rgba(0,0,0,0.5),0 1px 10px 0 rgba(0,0,0,0.15); margin: 1px; max-width:540px; min-width:326px; padding:0; width:99.375%; width:-webkit-calc(100% - 2px); width:calc(100% - 2px);"><div style="padding:16px;"> <a href="https://www.instagram.com/p/CyPmdp3SDLb/?utm_source=ig_embed&amp;utm_campaign=loading" style=" background:#FFFFFF; line-height:0; padding:0 0; text-align:center; text-decoration:none; width:100%;" target="_blank"> <div style=" display: flex; flex-direction: row; align-items: center;"> <div style="background-color: #F4F4F4; border-radius: 50%; flex-grow: 0; height: 40px; margin-right: 14px; width: 40px;"></div> <div style="display: flex; flex-direction: column; flex-grow: 1; justify-content: center;"> <div style=" background-color: #F4F4F4; border-radius: 4px; flex-grow: 0; height: 14px; margin-bottom: 6px; width: 100px;"></div> <div style=" background-color: #F4F4F4; border-radius: 4px; flex-grow: 0; height: 14px; width: 60px;"></div></div></div><div style="padding: 19% 0;"></div> <div style="display:block; height:50px; margin:0 auto 12px; width:50px;"><svg width="50px" height="50px" viewBox="0 0 60 60" version="1.1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink"><g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd"><g transform="translate(-511.000000, -20.000000)" fill="#000000"><g><path d="M556.869,30.41 C554.814,30.41 553.148,32.076 553.148,34.131 C553.148,36.186 554.814,37.852 556.869,37.852 C558.924,37.852 560.59,36.186 560.59,34.131 C560.59,32.076 558.924,30.41 556.869,30.41 M541,60.657 C535.114,60.657 530.342,55.887 530.342,50 C530.342,44.114 535.114,39.342 541,39.342 C546.887,39.342 551.658,44.114 551.658,50 C551.658,55.887 546.887,60.657 541,60.657 M541,33.886 C532.1,33.886 524.886,41.1 524.886,50 C524.886,58.899 532.1,66.113 541,66.113 C549.9,66.113 557.115,58.899 557.115,50 C557.115,41.1 549.9,33.886 541,33.886 M565.378,62.101 C565.244,65.022 564.756,66.606 564.346,67.663 C563.803,69.06 563.154,70.057 562.106,71.106 C561.058,72.155 560.06,72.803 558.662,73.347 C557.607,73.757 556.021,74.244 553.102,74.378 C549.944,74.521 548.997,74.552 541,74.552 C533.003,74.552 532.056,74.521 528.898,74.378 C525.979,74.244 524.393,73.757 523.338,73.347 C521.94,72.803 520.942,72.155 519.894,71.106 C518.846,70.057 518.197,69.06 517.654,67.663 C517.244,66.606 516.755,65.022 516.623,62.101 C516.479,58.943 516.448,57.996 516.448,50 C516.448,42.003 516.479,41.056 516.623,37.899 C516.755,34.978 517.244,33.391 517.654,32.338 C518.197,30.938 518.846,29.942 519.894,28.894 C520.942,27.846 521.94,27.196 523.338,26.654 C524.393,26.244 525.979,25.756 528.898,25.623 C532.057,25.479 533.004,25.448 541,25.448 C548.997,25.448 549.943,25.479 553.102,25.623 C556.021,25.756 557.607,26.244 558.662,26.654 C560.06,27.196 561.058,27.846 562.106,28.894 C563.154,29.942 563.803,30.938 564.346,32.338 C564.756,33.391 565.244,34.978 565.378,37.899 C565.522,41.056 565.552,42.003 565.552,50 C565.552,57.996 565.522,58.943 565.378,62.101 M570.82,37.631 C570.674,34.438 570.167,32.258 569.425,30.349 C568.659,28.377 567.633,26.702 565.965,25.035 C564.297,23.368 562.623,22.342 560.652,21.575 C558.743,20.834 556.562,20.326 553.369,20.18 C550.169,20.033 549.148,20 541,20 C532.853,20 531.831,20.033 528.631,20.18 C525.438,20.326 523.257,20.834 521.349,21.575 C519.376,22.342 517.703,23.368 516.035,25.035 C514.368,26.702 513.342,28.377 512.574,30.349 C511.834,32.258 511.326,34.438 511.181,37.631 C511.035,40.831 511,41.851 511,50 C511,58.147 511.035,59.17 511.181,62.369 C511.326,65.562 511.834,67.743 512.574,69.651 C513.342,71.625 514.368,73.296 516.035,74.965 C517.703,76.634 519.376,77.658 521.349,78.425 C523.257,79.167 525.438,79.673 528.631,79.82 C531.831,79.965 532.853,80.001 541,80.001 C549.148,80.001 550.169,79.965 553.369,79.82 C556.562,79.673 558.743,79.167 560.652,78.425 C562.623,77.658 564.297,76.634 565.965,74.965 C567.633,73.296 568.659,71.625 569.425,69.651 C570.167,67.743 570.674,65.562 570.82,62.369 C570.966,59.17 571,58.147 571,50 C571,41.851 570.966,40.831 570.82,37.631"></path></g></g></g></svg></div><div style="padding-top: 8px;"> <div style=" color:#3897f0; font-family:Arial,sans-serif; font-size:14px; font-style:normal; font-weight:550; line-height:18px;">在 Instagram 查看這則貼文</div></div><div style="padding: 12.5% 0;"></div> <div style="display: flex; flex-direction: row; margin-bottom: 14px; align-items: center;"><div> <div style="background-color: #F4F4F4; border-radius: 50%; height: 12.5px; width: 12.5px; transform: translateX(0px) translateY(7px);"></div> <div style="background-color: #F4F4F4; height: 12.5px; transform: rotate(-45deg) translateX(3px) translateY(1px); width: 12.5px; flex-grow: 0; margin-right: 14px; margin-left: 2px;"></div> <div style="background-color: #F4F4F4; border-radius: 50%; height: 12.5px; width: 12.5px; transform: translateX(9px) translateY(-18px);"></div></div><div style="margin-left: 8px;"> <div style=" background-color: #F4F4F4; border-radius: 50%; flex-grow: 0; height: 20px; width: 20px;"></div> <div style=" width: 0; height: 0; border-top: 2px solid transparent; border-left: 6px solid #f4f4f4; border-bottom: 2px solid transparent; transform: translateX(16px) translateY(-4px) rotate(30deg)"></div></div><div style="margin-left: auto;"> <div style=" width: 0px; border-top: 8px solid #F4F4F4; border-right: 8px solid transparent; transform: translateY(16px);"></div> <div style=" background-color: #F4F4F4; flex-grow: 0; height: 12px; width: 16px; transform: translateY(-4px);"></div> <div style=" width: 0; height: 0; border-top: 8px solid #F4F4F4; border-left: 8px solid transparent; transform: translateY(-4px) translateX(8px);"></div></div></div> <div style="display: flex; flex-direction: column; flex-grow: 1; justify-content: center; margin-bottom: 24px;"> <div style=" background-color: #F4F4F4; border-radius: 4px; flex-grow: 0; height: 14px; margin-bottom: 6px; width: 224px;"></div> <div style=" background-color: #F4F4F4; border-radius: 4px; flex-grow: 0; height: 14px; width: 144px;"></div></div></a><p style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; line-height:17px; margin-bottom:0; margin-top:8px; overflow:hidden; padding:8px 0 7px; text-align:center; text-overflow:ellipsis; white-space:nowrap;"><a href="https://www.instagram.com/p/CyPmdp3SDLb/?utm_source=ig_embed&amp;utm_campaign=loading" style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; font-style:normal; font-weight:normal; line-height:17px; text-decoration:none;" target="_blank">Mini Lab memo 軟工女孩×小研究式（@minilab_memo）分享的貼文</a></p></div></blockquote> <script async src="//www.instagram.com/embed.js"></script>

---

### 操作

#### 比對

##### 嚴格相等（===）

先比較型別

##### 一般相等（==）

一般相等會先將比較值轉換成同型別後比較。轉換後（可能一個或兩個都被轉換），接著進行的幾乎和嚴格比較（===）一樣。

```js
console.log(123 === '123');
false;
console.log(false === 0);
false;
console.log(false == 0);
true;
console.log(123 == '123');
true;
```

- 部分開發者認為最好別用一般相等。嚴格比較更容易預測，且因為不必轉型，因此效率更好。

##### 同值相等

> 提出同值相等演算法，用來解決這個問題。Object.is 就是部署這個演算法的新方法。同值相等解決了最後一個情況：比較兩個值是否功能相同 。
> Object.is 會和嚴格相等做同樣的事，但會將 NaN、-0 和 +0 獨立處理，因此這三個不會相等

##### 零值相等

和同值相等一樣，但將 +0 和 -0 視為相同。

```js
console.log(-0 == +0);
true;
console.log(-0 === +0);
true;
```

- 更多比較表可以看 [Equality_comparisons_and_sameness](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Equality_comparisons_and_sameness)
- 陣列比較 more [如何在 JavaScript 中比較兩個陣列](https://www.delftstack.com/zh-tw/howto/javascript/compare-two-arrays-javascript/)

#### 二元邏輯運算子

JavaScript 中的真假值在判斷會自動作轉型，像是 null、NaN、0、空字串（""、''）、undefined 都會被轉型並判斷為「false」。

- &&
  a= 條件式 ＆＆“”

```js
a5 = 'Cat' && 'Dog'; // t && t returns "Dog"
a6 = false && 'Cat'; // f && t returns false
```

- ||

```js
const a = 0 || 'hidden';
// 因為 0 被轉型後為 false，所以 a 會是 'hidden'

const b = 26900 || 24900;
// 因為 26900 會轉型為 true，所以 b 會是 26900
```

#### 展開語法（spread syntax）& 其餘語法（rest syntax）

展開運算子(...) 允許可迭代的陣列或字串展開成０到多個參數

#### 字符操作

- 一個字符串和一個数字可以直接相加變成字串
- 把字串當作對象，或許長度或大小寫轉換去處理字符串

```js
<script>
    let s = 19 + '67';
    console.log("s:"+s+" type:"+typeof s);
    //鍵入s.可以找到很多以字符為對象的操作
</script>
s:1967 type:string
```

#### Number()

对象将把传递给它的任何东西转换成一个数字

```js
let myString = '123';
let myNum = Number(myString);
typeof myNum;
```

#### toString()

每个数字都有一个名为 toString() 的方法，它将把它转换成等价的字符串。

ref:[JavaScript 中的字符串](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/First_steps/Strings)

#### [樣板字面值](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Template_literals)

> 樣板字面值（Template literals）是允許嵌入運算式的字串字面值（string literals）。

- 被反引號（back-tick，重音符號` ` )字元封閉，代替了雙或單引號。
- 可以包含由錢字元及花括號所構成（${expression}）的佔位符（placeholders）

```js
`string text line 1
 string text line 2``string text ${expression} string text`;

tag`string text ${expression} string text`;
```

- 標籤樣板字面值是一種更高級的樣板字面值形式，允許你透過自訂命名標籤函數 操作樣板字面值的輸出。
- 巢狀的樣板字面值的應用[Javascript 進階 10-3 巢狀結構](https://ithelp.ithome.com.tw/articles/10231520)

#### 物件屬性名稱縮寫（Shorthand property names）

- Key 與 Value 名稱相同，可進行縮寫
- 物件內可直接省略 function 關鍵字進行縮寫

#### 解構賦值 Destructuring assignment

可以把陣列或物件中的資料解開擷取成為獨立變數
詳細請見:[MDN-解構賦值](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

```js
const o = { p: 42, q: true };
const { p, q } = o;

console.log(p); // 42
console.log(q); // true

///
const o = { p: 42, q: true };
const { p: foo, q: bar } = o;

console.log(foo); // 42
console.log(bar); // true
```

---

### 函式宣告

- 可用函式宣告（Function Declaration）（ES5）
- 函式運算式(表達式)（Function Expressions）（ES5）
  - 宣告一個函數，或匿名函數 (anonymous function / function literal) 當作值指定給一個變數
- 箭頭函式運算式（arrow function expression）（ES6）
  - 它沒有自己的 this、arguments、super、new.target 等語法。

function 建構子說明

- JavaScript 使用稱為建構子函式（constructor function）的特殊函式，定義物件與功能。

```JavaScript
// 自己的一些東西
function Person(first, last, age, gender, interests) {
  this.name = {
    first,
    last
  };
  this.age = age;
  this.gender = gender;
  this.interests = interests;
  this.bio = function() {
    alert(this.name.first + ' ' + this.name.last + ' is ' + this.age + ' years old. He likes ' + this.interests[0] + ' and ' + this.interests[1] + '.');
  };
  this.greeting = function() {
    alert('Hi! I\'m ' + this.name.first + '.');
  };
};
var person1 = new Person('Bob', 'Smith', 32, 'male', ['music', 'skiing']);

```

Ref:[初學者應知道的物件導向 JavaScript](https://developer.mozilla.org/zh-TW/docs/Learn/JavaScript/Objects/Object-oriented_JS)

- 箭頭函式不可作為建構式使用；若使用於建構式，會在使用 new 時候拋出錯誤。
- 沒有 arguments "引數"參數,當需要使用 arguments 請維持使用 function。[->參數引數的概念請先知道]
- 宣告 ＸＸＸ等於 (參數 1, 參數 2, …, 參數 N) => { return 表示式; }

```JavaScript
  //箭頭 宣告 ＸＸＸ等於 (參數1, 參數2, …, 參數N) => { return 表示式; }
  const Pet_Arr = (color) => {
    this.color = color;
  }
  // ini_constructor_proto.html:99 Uncaught TypeError: Pet_Arr is not a constructor
  //箭頭函式不可作為建構式使用；若使用於建構式，會在使用 new 時候拋出錯誤。
  const PetA = new Pet_Arr('yellow'); //
```

Ref: [箭頭函式 MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

#### 宣告練習

使用及細節可以看下方

```JavaScript (js_func.html)
    <script>
        // ES5 函式宣告（Function Declaration）
        //function 函式名稱(參數) {
        function Add(A, B) {
            return A + B;
        }
        /* 或 */
        // ES5  函式運算式(表達式)（Function Expressions）
        // var 函式名稱 = function (參數) {
        var Add2 = function (A, B) {//匿名函式
            return A + B;
        }
        var Add3 = function add3(A, B) {//#1 非匿名函式
            console.log(typeof add3);//#1 但只在自身有效
            return A + B;
        }
        console.log(Add(1, 2))//3
        console.log(Add2(1, 2))//3
        console.log(Add3(1, 2))//3
        //console.log(add3(1, 2))//#1 ReferenceError: add3 is not defined


        //ES6 宣告型態 函式名稱 = (參數) => {
        var Add4 = (A, B) => {
            return A + B;
        }
        //縮寫 如果只有return 可以去掉{}與return
        var Add5 = (A, B) => A + B;

         //縮寫 如果只有一個參數 可以去掉（）
        var AddS1 = (A) => A;
        var AddS2 = A => A;

        console.log("ES6:" + Add4(1, 2))//3
        console.log("ES6:" + Add5(1, 2))//3
    </script>
```

#### this 的問題與箭頭函數的出現

箭頭函式有兩個重要的特性：更短的函式寫法與 this 變數的非綁定。

- 使用及細節可以看下方

```JavaScript (js_func_this.html)
    <script>
        //ES5 函示內this會指向windows而非Person，因此要像PersonSolve寫法
        function Person() {
            // Person() 建構式將 this 定義為它自己的一個實體
            this.age = 0;
            console.log("Person():" + this.constructor.name);
            setTimeout(function growUp() {
                // 在非嚴格模式下, growUp() 函式把 this 定義為全域物件
                // (因為那是 growUp()執行的所在)，
                // 與 Person() 建構式所定義的 this 有所不同
                this.age++;
                console.log("Person.setTimeout():" + this.constructor.name);
                console.log("Person.setTimeout():" + this.age)
            }, 1000);
        }
        function PersonSolve() {
            var self = this; // 有些人喜歡 `that` 而不是 `self`.
            // 選好一種取法後始終如一
            self.age = 0;
            console.log("PersonSolve():" + this.constructor.name);
            setTimeout(function growUp() {
                // 這個 callback 參考 `self` 變數，為預期中的物件。
                self.age++;
                console.log("PersonSolve.setTimeout():" + self.constructor.name);
                console.log("PersonSolve.setTimeout():" + self.age)

            }, 1000);
        }
        var p1 = new Person();
        var p2 = new PersonSolve();
        //---------

        //ES6 箭頭函示------------------------------
        function Person_Arr() {
            this.age = 0;
            console.log("Person_Arr():" + this.constructor.name);
            setTimeout(() => {
                this.age++; // |this| 適切的參考了Person建構式所建立的物件
                console.log("Person_Arr.setTimeout():" + this.constructor.name);
                console.log("Person_Arr.setTimeout():" + this.age)
            }, 1000);
        }

        var p3 = new Person_Arr();
        //ES6 箭頭函示------------------------------

       // OUTPUT
        // js_func_this.html: 17 Person(): Person
        // js_func_this.html: 31 PersonSolve(): PersonSolve
        // js_func_this.html: 47 Person_Arr(): Person_Arr

        // js_func_this.html: 23 Person.setTimeout(): Window -->發現竟然指向Window
        // js_func_this.html: 24 Person.setTimeout(): NaN  -->內容不見！！
        // js_func_this.html: 35 PersonSolve.setTimeout(): PersonSolve  -->workaround解法
        // js_func_this.html: 36 PersonSolve.setTimeout(): 1
        // js_func_this.html: 50 Person_Arr.setTimeout(): Person_Arr -->ES6 arrow解法
        // js_func_this.html: 51 Person_Arr.setTimeout(): 1
    </script>
```

- 箭頭函式並沒有原型（prototype）屬性。
  more ref: [this 不分家](https://developer.cdn.mozilla.net/zh-TW/docs/Web/JavaScript/Reference/Functions/Arrow_functions#this_%E4%B8%8D%E5%88%86%E5%AE%B6)

ＴＢＤ
no this new
https://developer.cdn.mozilla.net/zh-TW/docs/Web/JavaScript/Reference/Functions/Arrow_functions#this_%E4%B8%8D%E5%88%86%E5%AE%B6

### JS 的 Hoisting (提升)顶置特性

- 變數(var hoisting)與函數(function hoisting)都可以先使用再宣告
- 提升的是宣告並非是初始化的賦值
- 但提升操作如果用於 let 會引起錯誤(Uncaught ReferenceError)
  ref:[JavaScript Hoisting (提升)](https://shubo.io/javascript-hoisting/#javascript-hoisting-%E6%8F%90%E5%8D%87) 在「提升之後」以及「賦值之前」這段「期間」，如果你存取它就會拋出錯誤

### 使用 module 分檔 (import & export)

### 閉包（Closure）

閉包是函式以及該函式被宣告時所在的作用域環境的組合。

- 閉包的好處能把變數隱藏在裡面讓外部存取不到
- 閉包在 callback 上的應用尤其常見
- 在迴圈建立閉包：一個常見錯誤
  在 ECMAScript 2015 導入 let 前，迴圈內建立的閉包，常會發生問題。
  範例請見： [simple_js_demo-closure](https://github.com/minilabmemo/simple_js_demo/blob/master/04_js_closure/closure.html)

Ref:

- [MDN-閉包](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Closures)
- [你懂 JavaScript 嗎？#15 閉包（Closure）]（https://cythilya.github.io/2018/10/22/closure/）

## 探討：JavaScript OOP

OOP （(Object-oriented programming）物件導向/對象編程，在 JavaScript 中，大多数事物都是对象, 从作为核心功能的字符串和数组。你甚至可以自己创建对象，在调用函数前加一个 new ，它就会返回一个这个函数的实例化对象，. 然后，就可以在这个对象上面添加一些属性．[JavaScript 对象入门](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Objects)

舉例：

- 用 new func()來建構新的物件，func 內部 this 可以指項新屬性
- 透過建構子（constructor）所建立出來的物件，我們稱為實例（instance）
- 如果忘記打 new，變數會出現 undifined

```javascript
//this 指向了代码所在的对象(其实代码运行时所在的对象)。
function Pet(first, last, age) {
  this.name = {
    first: first,
    last: last,
  };
  (this.interests = ['food', 'sleep']), (this.age = age);
  this.walk = function () {
    console.log(this.name.first + ' walk...');
  }; //這樣寫會佔用不同的對象空間
}

//函数的实例化对象
var cat1 = new Pet('dotdot', 'wu', 11);
var dog1 = new Pet('lucky', 'wu', 9);

//通过简单的语法访问他们
console.log(cat1.name.first); //点表示法访问
console.log(cat1['name']['first']); //括号表示法
console.log(cat1.interests[1]); //数组属性的一个子元素
console.log(cat1.walk()); //对象的方法调用
```

ref:[[筆記] 談談 JavaScript 中的 function constructor 和關鍵字 new](https://pjchender.blogspot.com/2016/06/javascriptfunction-constructornew.html)

### Prototype 原型鏈的原理

上述的寫法，cat1.walk()與 dog1.walk()是兩個不同對象的方法，為解決這問題．

- walk 指定在 Pet.prototype 上面，所有 Pet 的 instance 都可以共享這個方法

```javascript
Pet.prototype.walk = function () {
  console.log(this.name.first + ' walk...');
};
```

- 因為 cat1 這個 instance 本身並沒有 walk 這個 function， 找不到，它會試著從 Pet.prototype 去找，一直往上找，直到找到 Object，如果還是沒有，就會回傳 undefined
- 而這個連接的方式，就是**proto**。
- 同时也有一些其他成员—— watch、valueOf 等等——这些成员定义在 Person() 构造器的原型对象、即 Object 。

ref:[該來理解 JavaScript 的原型鍊了](https://blog.techbridge.cc/2017/04/22/javascript-prototype/)
<br>[ **proto** 和 prototype 到底有什麼區別](https://kknews.cc/code/6agvk2v.html)

#### JavaScript 中的繼承 (prototypal inheritance)

- call()函数。基本上，这个函数允许您调用一个在这个文件里别处定义的函数。
- 设置 Teacher() 的原型和构造器引用
  - create()这意味着 Teacher.prototype 现在会继承 Person.prototype 的所有属性和方法
  - prototype 的 constructor 属性指向的是 Person(),要改指向 Teacher
- 可重寫 Teacher 的 greeting

```
//定义 Teacher() 构造器函数
  function Teacher(first, last, age, gender, interests, subject) {
    Person.call(this, first, last, age, gender, interests);

    this.subject = subject;
  }
  //这意味着Teacher.prototype现在会继承Person.prototype的所有属性和方法
  Teacher.prototype = Object.create(Person.prototype);
  Teacher.prototype.constructor = Teacher;//原本的是指向Ｐerson
  Teacher.prototype.greeting = function () {//重開改寫
    var prefix;

    if (this.gender === 'male' || this.gender === 'Male' || this.gender === 'm' || this.gender === 'M') {
      prefix = 'Mr.';
    } else if (this.gender === 'female' || this.gender === 'Female' || this.gender === 'f' || this.gender === 'F') {
      prefix = 'Mrs.';
    } else {
      prefix = 'Mx.';
    }

    alert('Hello. My name is ' + prefix + ' ' + this.name.last + ', and I teach ' + this.subject + '.');
  };
  var teacher1 = new Teacher('Dave', 'Griffiths', 31, 'male', ['football', 'cookery'], 'mathematics');

  teacher1.greeting()

```

ref:[JavaScript 中的继承](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Objects/Inheritance) 探討何時使用與參考網站練習

TBD:
https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Inheritance_and_the_prototype_chain

### 類別 (class)

ECMAScript 6 中引入了類別 (class) 作為 JavaScript 現有原型程式(prototype-based)繼承的語法糖。類別語法並不是要引入新的物件導向繼承模型到 JavaScript 中，而是提供一個更簡潔的語法來建立物件和處理繼承。

ref:[Classes](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Classes)

#### 類別宣告 (class declaration)

- 使用關鍵字 class

```
class Polygon {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
 var p = new Polygon();
```

- 相較函數宣告有 Hoisting，類別宣告則否。 你需要先宣告類別，然後存取它，否則就會丟出 ReferenceError:
  > var p = new Polygon(); // ReferenceError
  > class Polygon {}

#### 類別敘述(class expressions)

- 類別敘述是定義類別的另一種方法。類別敘述可以有名稱或是無名稱。賦予一個有名稱類別敘述的名稱只在類別主體(class's body)中有作用。（✍ 其實跟之前提到的 Function Expressions 一樣概念）

```
// unnamed
var Polygon = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};

// named
var Polygon = class Polygon {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
```

---

### 使用 JSON

- JSON 要求在字符串和属性用雙引號， 但引號無效。
- 我们使用 . 或 [] 訪問对象内的数据
- JSON.parse
  用於將文字轉成 json object

```js
request.responseType = 'text';
var superHeroes = JSON.parse(superHeroesText);
```

- JSON.stringify
  用於將 json object 轉成 json string

```js
var myJSON = { name: 'Chris', age: '38' };
console.log(myJSON);
var myString = JSON.stringify(myJSON);
console.log(myString); //string:{"name":"Chris","age":"38"}
```

## 事件(Event)

- 好得寫法是找到(select)button 並添加事件，避免汙染 HTML。
- 關於 button.onclick vs addEventListener
  - on 會覆蓋上一个事件
  - addEventListener 事件，可以多次绑定同一个事件并且不会覆盖上一个事件

ref:[JS 裡 addEventListener 和 on 的區別](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/42343/)

## 延伸：Lint 工具

在電腦科學中，lint 是一種工具程式的名稱，它用來標記原始碼中，某些可疑的、不具結構性（可能造成 bug）的段落。它是一種靜態程式分析工具

### JSLint

JSLint 幫你檢查未定義的變數、函數、陳述式結尾有沒有加分號(;)、變數使用之前要先用 var 宣告、使用非數字的變數要用 === 或 !== 讓比對的時候不要自動進行轉型(Casting)、盡量不要使用 eval 函數、... 好多好多

### ESLint

包括格式檢驗及質量效驗（未使用變量、三等號、全局變量聲明等問题）
自由選擇要使用哪些規則，對 還有 JSX 的支援度跟其他 linter 相較之下也是最高的

註： prettier 只是格式的檢驗（空格 格式化），不会對代码质量进行校验。但有些檢驗，ESLint 沒有，所以可以 ESLint ＋ prettier 一起使用，也可以視使用情況不使用 Prettier。

## 其他練習

## 上述概念練習

[simple_js_demo](https://github.com/minilabmemo/simple_js_demo)

## JS 與 canvas 元素

### 基礎繪製說明

Canvas 是 H5 新出來的標籤

- 元素需要有闭合标签
- 基本上現今所有主流的瀏覽器都有支援
- 所有元素定位皆相對於此左上角原點
  <br>

- HTML

```
<canvas id="canvas" width="300" height="300">
</canvas>

```

- JS
- 圓形 ctx.arc(x, y, 半徑, 開始弧度, 結束弧度 )
  0~2 pi =360°
  更多弧度示意圖：[弧度](https://zh.wikipedia.org/wiki/%E5%BC%A7%E5%BA%A6)

```
var canvas = document.getElementById('canvas');
var ctx = canvas.getContext('2d');
ctx.fillStyle = 'green';
ctx.fillRect(10, 10, 100, 100);//畫矩形 x start,y start,width,height
```

利用漸變色及貝斯曲線或是填入圖案，繪製文字，可做出很多豐富的圖案，還有動畫行星/時鐘，滑鼠動畫，像素控制等，詳請見下方文件

ref:[Canvas 教學文件](https://developer.mozilla.org/zh-TW/docs/Web/API/Canvas_API/Tutorial)

### 彈跳彩球範例

Ｒ ef: [物件建構實作](https://developer.mozilla.org/zh-TW/docs/Learn/JavaScript/Objects/Object_building_practice)

### 破撞說明

```
https://developer.mozilla.org/zh-CN/docs/Games/Techniques/2D_collision_detection
var circle1 = {radius: 20, x: 5, y: 5};//radius半徑及座標
var circle2 = {radius: 12, x: 10, y: 5};

var dx = circle1.x - circle2.x;
var dy = circle1.y - circle2.y;
var distance = Math.sqrt(dx * dx + dy * dy);//平面兩點之間距離公式

if (distance < circle1.radius + circle2.radius) { //原形半徑相加=兩圓碰撞時的距離
    // collision detected!
}
```

### 動畫操控範例說明

https://developer.mozilla.org/zh-TW/docs/Web/API/Canvas_API/Tutorial/Basic_animations

### 排程更新

第一種作法是利用 window.setInterval()與 window.setTimeout()方法。

Note: 針對新版瀏覽器建議採用 window.requestAnimationFrame()方法。方法為動畫提供更順暢更有效率的方式來執行,當系統準備好繪製畫面時,藉由呼叫動畫 andmation frame()的 callback 函數。

[requestanimationframe-with-react](https://www.pluralsight.com/guides/how-to-use-requestanimationframe-with-react)
[深入理解 requestAnimationFrame 的動畫迴圈](https://codertw.com/%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC/260087/)
[Web 計時與動畫 ](https://www.dazhuanlan.com/2019/12/25/5e024ca3eeb4d/)
[[javascript] requestAnimationFrame 優化動畫效率與資源](https://blog.camel2243.com/2017/01/31/javascript-requestanimationframe-%E5%84%AA%E5%8C%96%E5%8B%95%E7%95%AB%E6%95%88%E7%8E%87%E8%88%87%E8%B3%87%E6%BA%90/)

### Event 操控範例說明

https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Advanced_animations
這邊的話可以看到，Event 滑鼠控制只能針對整個畫布做操作，每次更新都是更新畫布，內容物件是不存在的。

延伸:[Canvas 和 SVG](https://www.itread01.com/content/1544856246.html)
Canvas 是點陣圖，受解析度影響，SVG 是向量圖。
使用 svg 有好有壞:
好處是方便操作 dom 元素, 可操作元素。
壞處是渲染效率不高, 在數據量較大時頁面易掉幀, 卡頓，不適合遊戲。

### D3 操控 SVG 或是 Canvas

http://blog.infographics.tw/2015/07/optimize-d3-with-canvas/
