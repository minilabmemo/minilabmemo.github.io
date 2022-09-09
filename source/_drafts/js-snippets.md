---
title: js--snippets
tags:
  - test
categories:
  - Tech.
  - Web
  - front-end
  - react
  - Tech.
  - back-end
  - golang
date: 2021-04-04 11:31:01
---

{% note info %} 藍色簡單區塊 {% endnote %}


<!--more-->


### ES7 React/Redux/React-Native/JS Snippets



#### rafc - ReactArrowFunctionComponent
- const App: () => JSX.Element
- 縮寫 如果只有return 可以去掉{}與return
- 快速鍵 rafc - ReactArrowFunctionComponent
- 可以視情況拿掉import & export
```
import React from 'react'

export const App = () => {
  return (
    <div>
      
    </div>
  )
}
```

#### nfn named function
在commponent(大寫)中如果要加入函式用named function
- params可以視情況移除
```
  const name = (params) => {

  }
```




# 網路參考文章
- [VS Code ES7 React/Redux/React-Native/JS snippets](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets)