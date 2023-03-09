# kube-prometheus-stack 功能練習

## 使用 podMonitor 安裝 aws cni 監控 dashboard
利用 grafana import 別人寫好得 dashboard 來監控 eks network interface 使用情形   
參考文件:   
https://grafana.com/grafana/dashboards/16032-aws-cni-metrics/   

其他說明:   
在測試的時候發現安裝 kube-prometheus-stack 原本就會預設裝一個 prometheus crd 在指定的 namespace 下，因此想透過該預設的 prometheus 來 scrape 在 kube-system 下的 aws-node metrics 才可以取得 network interface 相關的 metrics，像參考文件提到的，需要建立一個 `podMonitor CRD 資源` 來獲取 data。   

### 補充
因為在配置過程 dashboard 一直抓不到資料（顯示 no data）因此要從問題根本找原因，後來發現在 prometheus crd 裡面會有定義 podMonitorSelector 字段，裡面要填入 matchLabels 的對應 key-value，因此經過修正，最後完成的 `podMonitor CRD` 就是 `aws-cni-podmonitor.yaml` 檔案。