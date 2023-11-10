---
title: "[react + typescript + jest] 為你的 react 項目引入測試工具與問題排解 "
tags:
  - test
  - jest
  - react
  - typescript
  - create-react-app
toc: true
categories:
  - - Frontend
    - react
  - - 技術工具
    - test
cover: /img/posts/list.jpg
thumbnail: /img/posts/list.jpg
date: 2023-11-05 14:12:25
---


<article class="message is-info"><div class="message-body">
我的 react 項目是採 create-react-app ＋ typescript 創建的，現在要讓它加入 jest 測試項目，記錄整個創建過程及工具，過程中的問題排解。
</div></article>

<!--more-->
## 目錄 | Contents
<div class="my-toc">
<!-- toc -->
</div>

-----



## 初始專案建置
 首先你要有一個 react  ＋ typescript 項目
```
npm install -g create-react-app //有裝過可以不用跑
create-react-app <你的專案名稱> --template typescript
//要注意後方是否正確 否則可能回出現非 ts 版本的專案
```
另外它會幫你自動生成 tsconfig.json 配置
- target:Modern browsers support all ES6 features, so ES6 is a good choice.
- 其他解釋請見 [typescript lang](https://www.typescriptlang.org/tsconfig#target)
```json "展開查看 tsconfig.json 內容" >folded 
{
  "compilerOptions": {
    "target": "es2015",
    "lib": [
      "dom",
      "dom.iterable",
      "esnext"
    ],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noFallthroughCasesInSwitch": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx"
  },
  "include": [
    "src"
  ]
}
```


## 新增測試 
<div class="blockquote">
Create React App 使用 Jest 作為其測試運行器，透過 package.json 中的 Jest 配置可以覆寫配置，Jest 是一個流行的 JavaScript 測試框架，只需使用 it() 或 test() 及 expect 等及可編寫測試程式。 
</div> 

- 只要在對應檔案下新增 xxx.test.tsx 即可。如果你用 react-create-app 生成預設會有一個 App.test.tsx
撰寫測試內容，以下是簡單的測試範例：
- jest 斷言可以參考 [jest js](https://jestjs.io/docs/expect#content) 
- 而 @testing-library/react 有一些 render, screen 可用
```jsx
import React from 'react';
import { render, screen } from '@testing-library/react';
import App from './App';
test('render app toMatchSnapshot', () => {
  const view = render(<App />);
  expect(view).toMatchSnapshot();
});

test('renders the title with the correct text', () => {
  render(<App></App>);
  const titleElement = screen.getByText('首頁');
  expect(titleElement).toBeInTheDocument();
});
```


## 運行測試

Create React App 本身就可以直接使用 npm run test 開始執行測試。
- `npm test -- --coverage`可以看到多了覆蓋率與未覆蓋的地方，這指令也會多出一個 coverage 資料夾，裡面有 index.html 也可以看到結果，不過這個資料夾是被 git 濾掉不會上傳的。。
```json
 "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "testC": "npm test -- --coverage",
  },
```
```tsx "點我展開">folded

npm test -- --coverage 

 PASS  src/components/twDistricts.test.tsx
 PASS  src/App.test.tsx
------------------|---------|----------|---------|---------|---------------------
File              | % Stmts | % Branch | % Funcs | % Lines | Uncovered Line #s   
------------------|---------|----------|---------|---------|---------------------
All files         |   81.15 |       50 |   63.63 |   82.35 |                     
 src              |     100 |      100 |     100 |     100 |                     
  App.tsx         |     100 |      100 |     100 |     100 |                     
 src/components   |    80.3 |       50 |    61.9 |   81.53 |                     
  xxx.tsx   |   77.08 |      100 |      60 |   77.08 | 150-155,172-191,248 
  header.tsx      |     100 |      100 |     100 |     100 |                     
             
------------------|---------|----------|---------|---------|---------------------

Test Suites: 2 passed, 2 total
Tests:       3 passed, 3 total
Snapshots:   0 total
Time:        3.496 s, estimated 4 s
```

## 插件
因為我是用 vscode 做開發，而安裝插件 jest 可以有更好的測試面板做使用，安裝完之後只要檔案有任何更動，不管是不是測試檔案都會重新執行測試。
- 通過的項目就會在左側出現打勾。
- 上面測試報告的未覆蓋範圍可以透過 cmd+shift+P->Jest:Toggle Coverage 提示未覆蓋範圍。

<img src="/images/jest-vscode.png" width="ˇ300px" />


## 問題

### 運行後出現 SyntaxError 問題


<div class="blockquote">
原本在一般簡單的專案執行測試都沒問題，直到我用了一些複雜的外部元件 EX:axios，炸出一堆錯誤訊息，根據提示的方法 moduleNameMapper 與 transform 解一個又一個都出現問題，原本以為是編譯問題也因此研究了 tsconfig 與 jest.config.js/babel-jest 等概念設置都沒有效果，最後使用了 issue 上列的 transformIgnorePatterns 來排除問題，如果有人有其他解法可以一起討論一下。
</div>

- 錯誤訊息
```shell
SyntaxError: Cannot use import statement outside a module
Here's what you can do:
     • If you are trying to use ECMAScript Modules, see https://jestjs.io/docs/ecmascript-modules for how to enable it.
     • If you are trying to use TypeScript, see https://jestjs.io/docs/getting-started#using-typescript
     • To have some of your "node_modules" files transformed, you can specify a custom "transformIgnorePatterns" in your config.
     • If you need a custom transformation specify a "transform" option in your config.
     • If you simply want to mock your non-JS modules (e.g. binary assets) you can stub them out with the "moduleNameMapper" config option.

    You'll find more details and examples of these config options in the docs:
    https://jestjs.io/docs/configuration
    For information about custom transformations, see:
    https://jestjs.io/docs/code-transformation
 import axios, { AxiosError } from 'axios';
        | ^
//有時是引入資源
import { useMediaQuery } from "@uidotdev/usehooks";
import SaveSvg from "../Icons/SaveSvg";
import construct_img from '../images/construct_img.png';
```
- 解法  [SyntaxError: Cannot use import statement outside a module #9938](https://github.com/facebook/create-react-app/issues/9938)

```
"jest": {
    "transformIgnorePatterns": [
      "node_modules/(?!@shotgunjed)/"
    ]
  },
```

-------------


## 網路參考文章

<div class="ref">


- [create-react-app](https://create-react-app.dev/docs/running-tests/)
- [使用 Jest 在 Visual Studio Code 中进行更好的单元测试](https://www.testwo.com/article/1789)
- [Photo by Unsplash](https://unsplash.com/photos/person-writing-bucket-list-on-book-RLw-UC03Gwc)

  
</div>