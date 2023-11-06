---
title: "[HTML & CSS][✍ 筆記] 初學 HTML & CSS "
tags:
  - note
  - css
  - html
  - ing
categories:
  - [Frontend,css/html]

date: 2020-09-15 20:27:29
toc: true
---



<article class="message is-info"><div class="message-body">
練習CSS & HTML 操作相關筆記．[✍ 持續更新]
</div></article>



<!--more-->

## HTML

### Html 基礎
- HTML 文件 (HTML document) 
- 標籤 (tag)<tagname>...</tagname>包圍著語意 (semantic) 內容(Content)區塊稱作 HTML 元素 (HTML element)，不同標籤表達不同語意
- 空元素 (Empty Element / Void Element)
有些 HTML 元素是不允許有內容的，稱之為空元素。沒有結束標籤
常見包括
```
<br>換行 <hr> <img>圖片 <input>輸入 <link> <meta>
```
- HTML 標籤中還有屬性 (Attribute)，來提供該標籤的額外資訊


### 撰寫規則
- 屬性值用單引號雙引號都可以
- 標籤與屬性大小寫都可以，常見且建議是固定使用小寫 (lowercase)。
- 雙引號間的屬性值不能空白
什麼是HTML 標籤Tag - HTML 語法教學Tutorial - Fooish 程式技術
https://www.fooish.com/html/tag.html


### 語意標籤
HTML5中新增了語意化標籤(Semantic Elements)，目的是為了讓標籤(Tag)更具意義，以加強文件的結構化，讓搜尋引擎更清楚了解
```
Header 可於body內或是article或是section代表頁首或是首要區塊
Nav 導覽區塊
Main 主要區塊，整頁只有一個
Article 包覆文章
Section 區塊
Div 無意義為包裹區塊排版用
Aside 用來代表主內容的附加內容，未必是側邊欄，廣告等等都可以用
Footer 頁尾
Time 時間
Mark 似螢光筆重點
details 文章的細節
Figure /figcaption區塊 引用與標題
<hgroup> 當內容有主標題及次標題等多個標題的狀況下使用。
<cite> 引用其他文獻或作品(例如書籍、歌曲、電影、繪畫、雕塑等）的標題

<String>  粗體相對於<b></b>更有強烈意思
<i></i>italic(斜體)的字首。em 的完整名稱則是 emphasized(強調/注重)
s 原文是 strikethrough(刪除線)，del 這個標籤一看就會明白：delete(刪除)。
```
好文參考：
- [快速了解HTML語意化標籤](https://medium.com/@changru.studio/%E5%BF%AB%E9%80%9F%E4%BA%86%E8%A7%A3html%E8%AA%9E%E6%84%8F%E5%8C%96%E6%A8%99%E7%B1%A4-33dd8247d779)

- [[HTML5]b,i,s 跟 strong,em,del 這些看起來一樣，但意義不同的標籤們](
https://km.nicetypo.com/doc/ead903b94bb8bf01974d3ccdb91a117b)



## CSS

### 權重計算
<blockquote class="instagram-media" data-instgrm-captioned data-instgrm-permalink="https://www.instagram.com/p/Cy2zpI2ScJs/?utm_source=ig_embed&amp;utm_campaign=loading" data-instgrm-version="14" style=" background:#FFF; border:0; border-radius:3px; box-shadow:0 0 1px 0 rgba(0,0,0,0.5),0 1px 10px 0 rgba(0,0,0,0.15); margin: 1px; max-width:540px; min-width:326px; padding:0; width:99.375%; width:-webkit-calc(100% - 2px); width:calc(100% - 2px);"><div style="padding:16px;"> <a href="https://www.instagram.com/p/Cy2zpI2ScJs/?utm_source=ig_embed&amp;utm_campaign=loading" style=" background:#FFFFFF; line-height:0; padding:0 0; text-align:center; text-decoration:none; width:100%;" target="_blank"> <div style=" display: flex; flex-direction: row; align-items: center;"> <div style="background-color: #F4F4F4; border-radius: 50%; flex-grow: 0; height: 40px; margin-right: 14px; width: 40px;"></div> <div style="display: flex; flex-direction: column; flex-grow: 1; justify-content: center;"> <div style=" background-color: #F4F4F4; border-radius: 4px; flex-grow: 0; height: 14px; margin-bottom: 6px; width: 100px;"></div> <div style=" background-color: #F4F4F4; border-radius: 4px; flex-grow: 0; height: 14px; width: 60px;"></div></div></div><div style="padding: 19% 0;"></div> <div style="display:block; height:50px; margin:0 auto 12px; width:50px;"><svg width="50px" height="50px" viewBox="0 0 60 60" version="1.1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink"><g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd"><g transform="translate(-511.000000, -20.000000)" fill="#000000"><g><path d="M556.869,30.41 C554.814,30.41 553.148,32.076 553.148,34.131 C553.148,36.186 554.814,37.852 556.869,37.852 C558.924,37.852 560.59,36.186 560.59,34.131 C560.59,32.076 558.924,30.41 556.869,30.41 M541,60.657 C535.114,60.657 530.342,55.887 530.342,50 C530.342,44.114 535.114,39.342 541,39.342 C546.887,39.342 551.658,44.114 551.658,50 C551.658,55.887 546.887,60.657 541,60.657 M541,33.886 C532.1,33.886 524.886,41.1 524.886,50 C524.886,58.899 532.1,66.113 541,66.113 C549.9,66.113 557.115,58.899 557.115,50 C557.115,41.1 549.9,33.886 541,33.886 M565.378,62.101 C565.244,65.022 564.756,66.606 564.346,67.663 C563.803,69.06 563.154,70.057 562.106,71.106 C561.058,72.155 560.06,72.803 558.662,73.347 C557.607,73.757 556.021,74.244 553.102,74.378 C549.944,74.521 548.997,74.552 541,74.552 C533.003,74.552 532.056,74.521 528.898,74.378 C525.979,74.244 524.393,73.757 523.338,73.347 C521.94,72.803 520.942,72.155 519.894,71.106 C518.846,70.057 518.197,69.06 517.654,67.663 C517.244,66.606 516.755,65.022 516.623,62.101 C516.479,58.943 516.448,57.996 516.448,50 C516.448,42.003 516.479,41.056 516.623,37.899 C516.755,34.978 517.244,33.391 517.654,32.338 C518.197,30.938 518.846,29.942 519.894,28.894 C520.942,27.846 521.94,27.196 523.338,26.654 C524.393,26.244 525.979,25.756 528.898,25.623 C532.057,25.479 533.004,25.448 541,25.448 C548.997,25.448 549.943,25.479 553.102,25.623 C556.021,25.756 557.607,26.244 558.662,26.654 C560.06,27.196 561.058,27.846 562.106,28.894 C563.154,29.942 563.803,30.938 564.346,32.338 C564.756,33.391 565.244,34.978 565.378,37.899 C565.522,41.056 565.552,42.003 565.552,50 C565.552,57.996 565.522,58.943 565.378,62.101 M570.82,37.631 C570.674,34.438 570.167,32.258 569.425,30.349 C568.659,28.377 567.633,26.702 565.965,25.035 C564.297,23.368 562.623,22.342 560.652,21.575 C558.743,20.834 556.562,20.326 553.369,20.18 C550.169,20.033 549.148,20 541,20 C532.853,20 531.831,20.033 528.631,20.18 C525.438,20.326 523.257,20.834 521.349,21.575 C519.376,22.342 517.703,23.368 516.035,25.035 C514.368,26.702 513.342,28.377 512.574,30.349 C511.834,32.258 511.326,34.438 511.181,37.631 C511.035,40.831 511,41.851 511,50 C511,58.147 511.035,59.17 511.181,62.369 C511.326,65.562 511.834,67.743 512.574,69.651 C513.342,71.625 514.368,73.296 516.035,74.965 C517.703,76.634 519.376,77.658 521.349,78.425 C523.257,79.167 525.438,79.673 528.631,79.82 C531.831,79.965 532.853,80.001 541,80.001 C549.148,80.001 550.169,79.965 553.369,79.82 C556.562,79.673 558.743,79.167 560.652,78.425 C562.623,77.658 564.297,76.634 565.965,74.965 C567.633,73.296 568.659,71.625 569.425,69.651 C570.167,67.743 570.674,65.562 570.82,62.369 C570.966,59.17 571,58.147 571,50 C571,41.851 570.966,40.831 570.82,37.631"></path></g></g></g></svg></div><div style="padding-top: 8px;"> <div style=" color:#3897f0; font-family:Arial,sans-serif; font-size:14px; font-style:normal; font-weight:550; line-height:18px;">在 Instagram 查看這則貼文</div></div><div style="padding: 12.5% 0;"></div> <div style="display: flex; flex-direction: row; margin-bottom: 14px; align-items: center;"><div> <div style="background-color: #F4F4F4; border-radius: 50%; height: 12.5px; width: 12.5px; transform: translateX(0px) translateY(7px);"></div> <div style="background-color: #F4F4F4; height: 12.5px; transform: rotate(-45deg) translateX(3px) translateY(1px); width: 12.5px; flex-grow: 0; margin-right: 14px; margin-left: 2px;"></div> <div style="background-color: #F4F4F4; border-radius: 50%; height: 12.5px; width: 12.5px; transform: translateX(9px) translateY(-18px);"></div></div><div style="margin-left: 8px;"> <div style=" background-color: #F4F4F4; border-radius: 50%; flex-grow: 0; height: 20px; width: 20px;"></div> <div style=" width: 0; height: 0; border-top: 2px solid transparent; border-left: 6px solid #f4f4f4; border-bottom: 2px solid transparent; transform: translateX(16px) translateY(-4px) rotate(30deg)"></div></div><div style="margin-left: auto;"> <div style=" width: 0px; border-top: 8px solid #F4F4F4; border-right: 8px solid transparent; transform: translateY(16px);"></div> <div style=" background-color: #F4F4F4; flex-grow: 0; height: 12px; width: 16px; transform: translateY(-4px);"></div> <div style=" width: 0; height: 0; border-top: 8px solid #F4F4F4; border-left: 8px solid transparent; transform: translateY(-4px) translateX(8px);"></div></div></div> <div style="display: flex; flex-direction: column; flex-grow: 1; justify-content: center; margin-bottom: 24px;"> <div style=" background-color: #F4F4F4; border-radius: 4px; flex-grow: 0; height: 14px; margin-bottom: 6px; width: 224px;"></div> <div style=" background-color: #F4F4F4; border-radius: 4px; flex-grow: 0; height: 14px; width: 144px;"></div></div></a><p style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; line-height:17px; margin-bottom:0; margin-top:8px; overflow:hidden; padding:8px 0 7px; text-align:center; text-overflow:ellipsis; white-space:nowrap;"><a href="https://www.instagram.com/p/Cy2zpI2ScJs/?utm_source=ig_embed&amp;utm_campaign=loading" style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; font-style:normal; font-weight:normal; line-height:17px; text-decoration:none;" target="_blank">Mini Lab memo 軟工女孩×小研究式（@minilab_memo）分享的貼文</a></p></div></blockquote> <script async src="//www.instagram.com/embed.js"></script>


-------------------

### 區塊計算 Box Model
- Box Model 預設 box-sizing: content-box
  - content 內容 
  ```
  width: 寬度值;height: 高度值;
  ```
  - padding 內距
  ```
  padding:上 右 下 左;　padding:上下 左右;　
  padding:上 左右 下;　padding:四邊同値;
  ```
  - border 邊框
  ```
  border: 邊框粗細 邊框顏色 邊框樣式 ;
  ```
  - margin 物件與物件間距離
  ```
   margin:上 右 下 左;margin:上下 左右;
   margin:上 左右 下;margin:四邊同値;
  ```
- 該物件整體的大小會是content+padding+border，不要以為真的是width; height大小
- 然後margin是占空間但不可視的地方。


<img src="/images/content-box.png" width="500px" />

- 可以改變屬性 box-sizing: border-box;
- 就會幫你把整體物件大小設定為width+height
- 但這樣表示content內容只有width/height-padding-border(看左右/上下設定多少)
- 然後margin還是占空間但不可視的地方。

<img src="/images/border-box.png" width="500px" />



範例：可以用開發模式查看它的設定
<iframe src="https://codesandbox.io/embed/box-concept-f37fr-f37fr?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="Box concept-f37fr"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>


### css reset
撰寫時會發現元素與視窗有空隙，css reset可以清楚，還有其他一些效果

- React + @emotion/css 套用範例
```
import reset from 'react-style-reset';
import { injectGlobal } from '@emotion/css';
injectGlobal(reset, {
});
```


### 排版


#### display

##### 隱藏元素
- display預設為none

```
 display: none; //空間消失
 visibility:hidden //空間仍存在

```
 [w3schools Hide an Element](https://www.w3schools.com/css/css_display_visibility.asp)

##### 區塊元素 
- display預設為block，區塊元素排列都會另起一行，除非被改變
- 可設置寬高 width hight
- 默認情况下，其寬度自動填满其父元素寬度，即寬度100%
- 高度，行高以及頂和底邊距都可控制；

```
常見包括 div、p、h1~h6、
ul、ol、li、
dl、dt、dd、
form、table、hr、
blockquote 、
address、menu、pre.....等等
```
##### 行內元素
- display預設inline，除非被改變
- 設置寬高無效，只能由内容撑起来，行內元素會依照物件內容的大小決定占用的版面
- 行内元素会排列在同一行，直到一行排不下，才會換行，其寬度隨元素的内容而變化。
- 設置上下margin、padding无效，左右padding 、margin有效
```
常見包括
span、em、i、b、strong、
a、img、input、br、select、textarea、q、bdo、
sub、sup...等等
```
- 行內不能包含區塊元素
*可變元素 依上下文決定

Ref:https://www.jianshu.com/p/9fa96ece88f1

##### 行內區塊
- display：inline-block
- 以inline的方式呈現，但同時擁有block的屬性


------
#### Position
Static：默認值，沒有定位。
##### 固定定位fixed
- 不管滾軸移動，依然在一樣位置
- 空間不佔據，會蓋住別人
- 固定他在原本寫的位置上
- 有寫上右下左就會定位在視窗頂端的相對位置（非自身）
- 應用：
   - 蓋版廣告（左右上下置中 設立五個 為什麼）
   - 頂置導覽列top0
   - 回到上面 bottom 0

##### relative
- 空間會佔據，也會蓋住沒有設定定位的物件
- 相對於原本的位置上
- 兩個都有定位物件，後面蓋前面
- 可以設定z-index 設定優先，預設0

##### absolute
- 空間不佔據，資料會在原本資料的位置
- 設定完上下左右它會往有定位的父層找
- 如果找不到會定位在視窗上，不是body(如果想要定在body上，body需要設定定位，往上還有html,有一點差別 )
- 應用在不想與人排列的情況，通常父層會用relative,父層想要有排列
- 應用：
    - 特賣標籤absolute,父層項目relative
    - 改版廣告的(X)

----
#### float

----
#### Flex
- 父層設定可以控制子層的排列方式
<iframe src="https://codesandbox.io/embed/flex-base1-xhwn8?fontsize=14&hidenavigation=1&theme=dark&view=preview"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="flex-base1"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

----
#### 關於置中
##### margin
“margin:0 atuo;”所代表的的意思是水平居中，區塊元素的容器水平置中。
關於
[margin:0 atuo;”是什么意思？](https://www.html.cn/qa/css3/19856.html)
[不要告訴我你懂margin](https://fredevangigi.pixnet.net/blog/post/57202532)

ＴＢＤ
1.align-content
2.延伸設定
3. default: align-items: stretch; 上下高度自動滿版時有出現空白問題

-----

## 範例版面與物件
###  互動式視窗 Modal window 
原理：製作一置中視窗，然後先隱藏起來，該位置距離上方可以百分比設定．
- margin: 15% auto; / 15% from the top and centered /
  [w3schools=How TO CSS/JS Modal](https://www.w3schools.com/howto/howto_css_modals.asp)

*My React版練習[Add: Model](https://github.com/minilabmemo/counter-water/commit/fd3a285c515fa8cdea8e94a965c6bcd95eff4996)

-----
### input 欄位
- 一般的輸入數字框，可以看到預設會有上下箭頭出現
```
<input type="number" value="5">
```
<input type="number" value="5">

  - 如果要隱藏上下箭頭可以這樣寫：[howto_css_hide_arrow_number](https://www.w3schools.com/howto/howto_css_hide_arrow_number.asp)
  - css-in-js 版- [Hiding input spinner using styled-component](https://stackoverflow.com/questions/56352294/hiding-input-spinner-using-styled-component)

