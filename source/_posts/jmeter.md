---
title: jmeter 測試工具初體驗
tags:
  - test
  - jmeter
  - qa
categories:
  - Tech.
  - back-end
  - test
date: 2022-07-01 21:32:36
---

# 什麼是 JMeter 
>The **Apache JMeter™** application is open source software, a 100% pure Java application designed to load test functional behavior and measure performance. It was originally designed for testing Web Applications but has since expanded to other test functions.g 

# 使用時機

當需要對API做整合測試並驗證回覆時使用．

# 本文將會知道：
  1. 使用測試工具JMeter做一連串API測試
  2. 解析回覆json與驗證
  3. `（未完待續）` 壓力測試

<!--more-->





## 啟動

在windows下使用

* 下載並開啟時執行黨 (jmeter="5.2.1")
* 如果需要解析json，需自行放入lib,xxx.jar

## 範例：

### Get APIs

以下這個範例是根據詢問一個Http \[list]，再根據回覆去一個個問另一支API．

* 請依序新增對應設定，可以右鍵disable/enable該群組
* 按下執行就可以從檢視結果樹看到結果

測試計畫

> * 使用者自訂變數;
>* 執行緒群組
>  *   簡易控制器: 簡易命名
>
>      * HTTP 標頭管理員 Authorization:Bearer ${token}
>      * HTTP 要求 arrays
        * BeanShell PostProcessor
>      * JSON Extractor disabled
>      * ForEach 控制器
        * HTTP 要求 by id
          * 驗證回覆
>      * Debug Sampler
>      * 檢視結果樹




* 這個測試檔案：[sample.jmx](https://github.com/minilabmemo/working-helper-record/blob/main/sample.jmx)

## 更多細節：

### 自訂變數/引用變數

當自訂toekn=xxx時就可以用${token}拿到變數．

### HTTP 要求 arrays
這是一個API 會直接回覆 arrays 如下：

```
[
[
   {
      "id":"1",
      "name":"123"
   },
   {
      "id":"2",
      "name":"233"
   }
]
```

### BeanShell PostProcessor

- (java語法)處理json資料，並透過vars.put（key,value）設定資料給下一步使用
- 這邊會需要debug比較麻煩，可以另外從上方視窗叫出log來查看問題出在哪裡
```java
import org.json.JSONObject;
import org.json.JSONArray;

try{
	
String response = "";
response = prev.getResponseDataAsString();
log.info("responsessss：" + response);
JSONArray jsonArray = new JSONArray(response);

for (int i=0; i < jsonArray.length(); i++) {
   JSONObject o= jsonArray.getJSONObject(i);
   String name = o.getString("name");
    String id = o.getString("id");
   log.info("name：" + name);
   vars.put("data_"+i,id);
}


catch (Throwable ex) {
log.error("Error in Beanshell", ex);
throw ex;
}
```

### ForEach 控制器

在使用之前必須有資料是\[data\_1:xxx,data\_2:xxx....]&#x20;

* 變數前置字串為data，start index:-1，輸出變數名稱，d&#x20;
* 這時下一層的HTTP 要求 by id就可以引用${d}

### 驗證回覆

可以驗證回復，如果要驗證的是500，可以勾選Ignore status。

### Debug Sampler&#x20;

可以查看過程中變數內容




###  網路參考文章
>note warning %} <span style="font-size: 9px;">
學習路上感謝網路大神們，如果你發現了我，可以查看以下參考文章了解更多概念👇👇👇</span>
* [Jmeter断言中判断请求失败的响应代码问题](https://www.cnblogs.com/fengsiyi/p/6904041.html) 找不到斷言，但有驗證回復
* [Meter - JSON variable in a ForEach Controller](https://www.codeproject.com/Tips/5323656/JMeter-JSON-variable-in-a-ForEach-Controller)
