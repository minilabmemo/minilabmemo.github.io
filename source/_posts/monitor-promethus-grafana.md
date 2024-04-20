---
title: "[監控]使用 Prometheus+Grafana 監控電腦與程式效能"
cover: /images/grafanaWin.png
thumbnail: /images/grafanaWin.png
tags:
  - Prometheus
  - Grafana
  - monitor
	- golang
categories:
  - [技術工具，效能]
date: 2021-04-28 20:20:29
---

<article class="message is-info"><div class="message-body">
使用 Prometheus+Grafana 監控效能 
</div></article>

## 介紹

### Prometheus

> 普羅米修斯是開源的免費應用程序。可以很容易建立不同維度的 metrics 及資訊視覺化圖表的監控與查詢，也有告警設定，Kubernetes 的核心組件也可以找到它的身影，許多知名公司如：Uber 也有導入。

### Grafana

> Grafana 是一個跨平台、開源的資料視覺化網路應用程式平台。使用者組態連接的資料來源之後，Grafana 可以在網路瀏覽器里顯示資料圖表和警告。該軟體的企業版本提供更多的擴充功能。擴充功能通過外掛程式的形式提供，終端使用者可以自訂自己的資料面板介面以及資料請求方式。Grafana 被廣泛使用，包括維基百科專案。

<!--more-->

## 必備安裝與設定

### 下載 Prometheus

下載網址 https://prometheus.io/download/

個人是用 windows 所以下載的是 zip 檔，
內含 prometheus.exe 執行程式與 prometheus.yml 設定檔。
點擊 prometheus.exe 啟動預設 9090port，即可查看 http://localhost:9090/已運作。
如欲更改 port

```
//start.bat
prometheus.exe  --web.listen-address=:9999
cmd
```

但這時並未監控任何程式，待後面範例會用到，可先關閉。

### 下載 grafana

下載網址 https://grafana.com/grafana/download
個人是 docker 啟動

```
docker run -d --name=grafana -p 3000:3000 grafana/grafana
```

即可開啟 http://localhost:3000/ 預設帳號密碼：admin

#### 設定 grafana 連結 prometheus

進入後尋找 data sources->設定連接 prometheus
新增 Url:http://localhost:9999 Access:Browser，Save & Test 確認連接
目前還沒有設定圖表，僅先設定待用。

---

## 監控 windows 電腦 CPU/Network/Memory

### 1.windows_exporter 用來監控 windows

下載地址：https://github.com/martinlindhe/wmi_exporter/releases
下載 MSI，下載後在需要監控的目標主機上雙擊執行安裝，安裝完成後會以服務的形式自動執行，預設監聽 9182 埠。

如須關閉可以在電腦中服務找到 windows_exporter 關閉之。

其他[Node Exporter Full by Instance ID](https://grafana.com/grafana/dashboards/10204)

### 2.修改 prometheus.yml

```
  - job_name: 'windows_exporter'
    static_configs:
    - targets: ['localhost:9182']
      labels:
        instance: Windows
```

### 3.於 grafana 新增圖表

於[grafana 的網站上搜尋做好的圖表](https://grafana.com/grafana/dashboards)，這邊有找到兩種：

- [windows_exporter for Prometheus Dashboard](https://grafana.com/grafana/dashboards/13466/)
- [Windows Node (fixed for v0.13.0+)](https://grafana.com/grafana/dashboards/12422)
  就可以監控了

<img src="/images/grafanaWin.png" width="500px"/>

---

## 監控 Go 程式效能

### 1.在 Go 程式代碼中加入監控代碼

ex: [GIN 的 prometheus 用法](https://stackoverflow.com/questions/65608610/how-to-use-gin-as-a-server-to-write-prometheus-exporter-metrics)

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

已開啟一個 listen 8000 的程式

### 2. 編輯 prometheus.yml，

把監控的 web 服務 localhost:8000 加入，這邊可以編輯多組。

```yaml
- job_name: "prometheus"

  # metrics_path defaults to '/metrics'
  # scheme defaults to 'http'.

  static_configs:
    - targets: ["localhost:8000", "localhost:8011"]
```

### 3. 啟動

這時可以打開 localhost:9999 就可以看到 Prometheus 的簡易歷史圖表記錄了。
metrics available for this monitor [prometheus-go](https://docs.signalfx.com/en/latest/integrations/agent/monitors/prometheus-go.html)

### 4. import Go Metrics 圖表

於[grafana 的網站上搜尋做好的圖表](https://grafana.com/grafana/dashboards)

- 例如可以套入這個[Go Metrics](https://grafana.com/grafana/dashboards/10826) 範例

<img src="https://grafana.com/api/dashboards/10826/images/6819/image" width="500px"/>

---

## 網路參考文章

- [Prometheus（二）：Prometheus 監控 Windows 機器](https://www.mdeditor.tw/pl/pghx/zh-tw)
- [Promethus 叢集部署筆記：（四）安裝並配置 windows_exporter
  ](https://www.mdeditor.tw/pl/gmMw/zh-tw)
- [使用 Prometheus 和 Grafana 打造 Flask Web App 監控預警系統](https://blog.techbridge.cc/2019/08/26/how-to-use-prometheus-grafana-in-flask-app/)
  [Grafana | 將資料視覺化？簡易的介紹與操作！](https://ab20803.medium.com/grafana-%E5%B0%87%E8%B3%87%E6%96%99%E8%A6%96%E8%A6%BA%E5%8C%96-%E7%B0%A1%E6%98%93%E7%9A%84%E4%BB%8B%E7%B4%B9%E8%88%87%E6%93%8D%E4%BD%9C-4af05a0f4d8c)
