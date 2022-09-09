---
title: "[JAVA]有關java之OutOfMemory檢測等相關問題文章整理"
tags:
  - java
  - Memory
  - IDEA
categories:
  - Tech.
  - back-end
  - java
date: 2020-11-14 19:31:51
---


{% note info %}有關java之OutOfMemory檢測等相關問題文章整理{% endnote %}


<!--more-->


#### 關於JVM
```
-Xms = 初始值，預設是實體記憶體的1/64
-Xmx = 最大值，預設是實體記憶體的1/4
-Xmn = 最小值
預設空餘堆記憶體小於40%時，JVM 就會增大堆直到-Xmx 的最大限制。
```

- [一图解千愁，jvm内存从来没有这么简单过！](https://juejin.im/post/5ed49e7c51882543012f9e6c "一图解千愁，jvm内存从来没有这么简单过！")
- 該文建議使用操作系统的2/3作为堆空间，是比较合理的。这是一个经验值。比如6GB的内存，你分配给JVM的，最好不要超过4GB。
- [淺談 JVM PermGen space 的解決方法](https://ithelp.ithome.com.tw/articles/10211000)

#### 調整JVM
可以透過以下的參數來修改它，不過應該不要刻意去加大給它的分配記憶體，因為遇到需要大量的請求不多，
怕造成記憶體的浪費，應該是從程式面下手修正程式效能(又是一課題了Orz)。
- 開發時 IDE 設定

```
IDE JAVA_OPTS="-Xmx900m -Xms900m"

```
- 修改jvm.cfg
[調整JVM虛擬機器記憶體大小](https://www.itread01.com/content/1546694105.html "調整JVM虛擬機器記憶體大小")
- 執行jar包的時候參數調整
```bash
java -Xmx900m -Xms900m jar app.jar
```


- tomcat/Resin/weblogic 等設定
[完美解決java.lang.OutOfMemoryError處理錯誤的問題](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/313033/ "完美解決java.lang.OutOfMemoryError處理錯誤的問題")

#### 調整JVM參數說明
- [深入理解JVM內幕之JVM簡單調優參數](https://kknews.cc/zh-tw/code/lxjr3bb.html "深入理解JVM內幕之JVM簡單調優參數")
	- Xmx和Xms設置一樣大，MaxPermSize和MinPermSize設置一樣大


#### 關於OutOfMemoryError追查
[專案出現記憶體溢位的原因及解決方案](https://www.itread01.com/content/1546849805.html "專案出現記憶體溢位的原因及解決方案")
重點:
1. 修改JVM啟動引數，直接增加記憶體。(-Xms，-Xmx引數一定不要忘記加。)
2.檢查錯誤日誌，檢視“OutOfMemory”錯誤前是否有其它異常或錯誤。
3.對程式碼進行走查和分析，找出可能發生記憶體溢位的位置。
4.使用記憶體檢視工具動態檢視記憶體使用情況
	1. Eclipse開啟Show Heap Status
	1. IntelliJ IDEA 可開啟Memory Indicator & debugger Memory頁籤
	(可參考下方檢測工具@IDEA標題)


------------
#### 程式面與錯誤訊息範例

-  關於集合物件未清除的範例
[List、MAP等集合对象是否有使用完后,未清除造成内存溢出](https://bbs.csdn.net/topics/391865237 "List、MAP等集合对象是否有使用完后,未清除造成内存溢出")
- Map &Java heap space 無限迴圈
[Java記憶體溢位(OOM)異常排查指南](https://www.itread01.com/content/1548835928.html "Java記憶體溢位(OOM)異常排查指南")
	- 內含更多錯誤示例解說
OutOfMemoryError: Java heap space
OutOfMemoryError: GC overhead limit exceeded
OutOfMemoryError:Permgen space
OutOfMemoryError:Metaspace
OutOfMemoryError:Unable to create new native thread
OutOfMemoryError:Out of swap space?
OutOfMemoryError:Requested array size exceeds VM limit
Out of memory:Kill process or sacrifice child

------------
#### 檢測工具@IDEA
IntelliJ IDEA 可開啟Memory Indicator & debugger Memory頁籤
	(可參考說明開啟:
	[show-heap-memory-size-in-intellij](https://stackoverflow.com/questions/36691118/is-it-possible-to-show-heap-memory-size-in-intellij-ide-android-studio "show-heap-memory-size-in-intellij")
		[Analyze objects in the JVM heap](https://www.jetbrains.com/help/idea/analyze-objects-in-the-jvm-heap.html "Analyze objects in the JVM heap"))
		
- 關於IDEA如何设置JVM参数
[IDEA如何设置JVM参数](https://blog.csdn.net/shuiCSDN/article/details/104144009 "IDEA如何设置JVM参数")
[菜鸟学习IntelliJ IDEA之如何设置JVM运行参数](https://blog.csdn.net/Gaomb_1990/article/details/80645056 "菜鸟学习IntelliJ IDEA之如何设置JVM运行参数")

-  關於IDEA debugger Memory頁籤
用來查看目前堆中類的個數的情况，右邊的diff會顯示跳轉類的變化
> 過去看來是透過plugin去安裝JVM Debugger Memory View，但我在plugin 已找不到這個，且官網支援的版本也沒有了，但在IEDA 2020.1 debugg時多出的Memory tab，似乎與這功能一模一樣。
說明網站:
[神兵利器－内存调试插件](https://www.jianshu.com/p/709fdc76d420 "神兵利器－内存调试插件")
[IDEA中很有用的內存調試插件](https://kknews.cc/zh-hk/code/2q4qpvz.html "IDEA中很有用的內存調試插件")
[使用多年的go pprof检查内存泄漏的方法居然是错的?!](https://colobu.com/2019/08/20/use-pprof-to-compare-go-memory-usage/ "使用多年的go pprof检查内存泄漏的方法居然是错的?!")

------------

#### 使用jvm監控工具命令
一般用於檢視服務執行時狀態的主要命令包括：jstat、jmap、top、jstack
- 基本工具介紹 [Java內存泄露監控工具](https://kknews.cc/code/pl6kmv2.html "Java內存泄露監控工具：JVM監控工具介紹  原文網址：https://kknews.cc/code/pl6kmv2.html")