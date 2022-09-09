---
title: "[python 02]初學 python 筆記"
tags:
  - python
  - call by sharing
categories:
  - Tech.
  - back-end
  - python
date: 2021-02-13 15:18:37
---

{% note info %} 初學 python 筆記 {% endnote %}


<!--more-->


## python 學習收藏文

[Day - 03] - Python 基礎語法教學 Part 1
https://ithelp.ithome.com.tw/articles/10200505


## Python 資料型態
- 常见的 immutable objects
Numeric types: int, float, complex
string
tuple
frozen set
參數傳遞行為同 pass-by-value。
- 常见的 mutable objects:
list
dict
set
byte array
參數傳遞行為同 pass-by-reference，但是不允許 re-assignment(會指向新的object，跟之前物件無關)。

參考文章: 
- 理解 Python object 的 mutable 和 immutable
http://wsfdl.com/python/2013/08/14/%E7%90%86%E8%A7%A3Python%E7%9A%84mutable%E5%92%8Cimmutable.html

- Python資料型態，可變與不可變物件
http://changlt.blogspot.com/2017/04/python_29.html

- Python 函式的參數傳遞方式：Passed by assignment
https://blog.hitripod.com/python-function-passed-by-assignment/

- python 並不會因為 data 是可變還是不可變的因素去決定是傳值還是傳參 (很多人都有這種誤解), 因為他都不是, 他自有其特殊的傳遞方式， python 是完完全全的 call by sharing!
http://dokelung.me/category/python/python-evaluation-strategy/

延伸:
JS的call by sharing [JS基本觀念：call by value 還是reference 又或是 sharing?]
https://medium.com/@mengchiang000/js%E5%9F%BA%E6%9C%AC%E8%A7%80%E5%BF%B5-call-by-value-%E9%82%84%E6%98%AFreference-%E5%8F%88%E6%88%96%E6%98%AF-sharing-22a87ca478fc

## 