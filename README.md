# kubernetes-practice
For test my k8s lab repo

* 練習 k8s 的 repo

* 本 repo 採用 kubeadm v1.14 , kubelet v1.14 , kubectl v1.14

### proxy-docker-compose.yaml (獨立一台機器)
1. 製作 nginx load balancer，依照真實環境修改 nginx.conf
2. nginx.conf 設定 upstream server

### 利用 kubeadm 創建高可用集群的使用教學
1. 利用 proxy-docker-compose 創建 loadbalancer
2. 利用 prerequisite 腳本 "安裝 kubernetes 叢集" 的前置條件和環境
3. 設定 kubeadm 初始化 kubernetes 集群的 master node 
