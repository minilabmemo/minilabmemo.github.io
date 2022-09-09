---
title: "[監控]使用Prometheus+Grafana監控效能"
tags:
  - Prometheus
  - Grafana
  - monitor
categories:
  - Tech.
  - back-end
  - monitor
date: 2021-04-28 20:20:29
---

{% note info %} 使用Prometheus+Grafana監控效能 {% endnote %}




## 介紹

### Prometheus
> 普羅米修斯是開源的免費應用程序。可以很容易建立不同維度的 metrics及資訊視覺化圖表的監控與查詢，也有告警設定，Kubernetes的核心組件也可以找到它的身影，許多知名公司如：Uber也有導入。

### Grafana
> Grafana是一個跨平台、開源的資料視覺化網路應用程式平台。使用者組態連接的資料來源之後，Grafana可以在網路瀏覽器里顯示資料圖表和警告。該軟體的企業版本提供更多的擴充功能。擴充功能通過外掛程式的形式提供，終端使用者可以自訂自己的資料面板介面以及資料請求方式。Grafana被廣泛使用，包括維基百科專案。


<!--more-->

## 必備安裝與設定

### 下載Prometheus

下載網址https://prometheus.io/download/

個人是用windows 所以下載的是zip檔，
內含prometheus.exe執行程式與prometheus.yml設定檔。
點擊prometheus.exe 啟動預設9090port，即可查看http://localhost:9090/已運作。
如欲更改port
```
//start.bat 
prometheus.exe  --web.listen-address=:9999
cmd
```
但這時並未監控任何程式，待後面範例會用到，可先關閉。

### 下載grafana

下載網址 https://grafana.com/grafana/download
個人是docker啟動
```
docker run -d --name=grafana -p 3000:3000 grafana/grafana
```
即可開啟http://localhost:3000/ 預設帳號密碼：admin

#### 設定 grafana連結prometheus
進入後尋找data sources->設定連接prometheus
新增Url:http://localhost:9999 Access:Browser，Save & Test確認連接
目前還沒有設定圖表，僅先設定待用。

--- 

## 監控windows電腦CPU/Network/Memory

### 1.windows_exporter 用來監控windows
下載地址： https://github.com/martinlindhe/wmi_exporter/releases
下載MSI，下載後在需要監控的目標主機上雙擊執行安裝，安裝完成後會以服務的形式自動執行，預設監聽9182埠。

如須關閉可以在電腦中服務找到windows_exporter關閉之。

其他[Node Exporter Full by Instance ID](https://grafana.com/grafana/dashboards/10204)

### 2.修改prometheus.yml
```
  - job_name: 'windows_exporter'
    static_configs:
    - targets: ['localhost:9182']
      labels:
        instance: Windows
```

### 3.於grafana 新增圖表
於[grafana的網站上搜尋做好的圖表](https://grafana.com/grafana/dashboards)，這邊有找到兩種：
- [windows_exporter for Prometheus Dashboard](https://grafana.com/grafana/dashboards/13466/)
- [Windows Node (fixed for v0.13.0+)](https://grafana.com/grafana/dashboards/12422)
就可以監控了

<img src="/images/post/grafanaWin.png" width="500px"/>

---

## 監控Go程式效能
### 1.在Go程式代碼中加入監控代碼

ex: [GIN的prometheus用法]( https://stackoverflow.com/questions/65608610/how-to-use-gin-as-a-server-to-write-prometheus-exporter-metrics)
```diff
import (
	"log"
	"net/http"
	"github.com/gin-gonic/gin"
+	"github.com/prometheus/client_golang/prometheus/promhttp"
)
func main() {
+	StartMonitoring("0.0.0.0:8000")
	select {}
}
func StartMonitoring(port string) {
	var p string
	if port == "" {
		p = ":8080"
	} else {
		p = port
	}
	go func() {
		log.Println("Listening on", p)
+	http.Handle("/metrics", promhttp.Handler())
		log.Fatal(http.ListenAndServe(p, nil))
	}()
}
+ func prometheusHandler() gin.HandlerFunc {
	h := promhttp.Handler()

	return func(c *gin.Context) {
		h.ServeHTTP(c.Writer, c.Request)
	}
}
```
已開啟一個listen 8000的程式


### 2. 編輯prometheus.yml，
把監控的web服務localhost:8000加入，這邊可以編輯多組。
```yaml
  - job_name: 'prometheus'

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
    - targets: ['localhost:8000','localhost:8011']
    
```

### 3. 啟動

這時可以打開localhost:9999就可以看到Prometheus的簡易歷史圖表記錄了。
metrics available for this monitor [prometheus-go](https://docs.signalfx.com/en/latest/integrations/agent/monitors/prometheus-go.html)




### 4. import Go Metrics 圖表
於[grafana的網站上搜尋做好的圖表](https://grafana.com/grafana/dashboards)
- 例如可以套入這個[Go Metrics](https://grafana.com/grafana/dashboards/10826) 範例



-------------------


##  網路參考文章
{% note warning %} <span style="font-size: 9px;">
學習路上感謝網路大神們，如果你發現了我，可以查看以下參考文章了解更多概念👇👇👇</span>{% endnote %}
- [Prometheus（二）：Prometheus 監控Windows機器](https://www.mdeditor.tw/pl/pghx/zh-tw)
- [Promethus叢集部署筆記：（四）安裝並配置windows_exporter
](https://www.mdeditor.tw/pl/gmMw/zh-tw)
- [使用 Prometheus 和 Grafana 打造 Flask Web App 監控預警系統](https://blog.techbridge.cc/2019/08/26/how-to-use-prometheus-grafana-in-flask-app/)
[Grafana | 將資料視覺化？簡易的介紹與操作！](https://ab20803.medium.com/grafana-%E5%B0%87%E8%B3%87%E6%96%99%E8%A6%96%E8%A6%BA%E5%8C%96-%E7%B0%A1%E6%98%93%E7%9A%84%E4%BB%8B%E7%B4%B9%E8%88%87%E6%93%8D%E4%BD%9C-4af05a0f4d8c)
