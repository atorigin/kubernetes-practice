# kubernetes-practice

* 練習 HA 的 kubernetes cluster 的建置

* 本 repo 採用 kubeadm v1.14 , kubelet v1.14 , kubectl v1.14

### 初始化第一台 control-plane node -> master node
` kubeadm init --config=kubeadm-config.yaml --experimental-upload-certs `

output like:
```
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:
... 
...
...
You can now join any number of the control-plane node running the following command on each as root:

  kubeadm join myk8s.helloyuan.site:6443 --token 8c
    --discovery-token-ca-cert-hash sha256:901
    --experimental-control-plane --certificate-key f42d

Please note that the certificate-key gives access to cluster sensitive data, keep it secret!
As a safeguard, uploaded-certs will be deleted in two hours; If necessary, you can use
"kubeadm init phase upload-certs --experimental-upload-certs" to reload certs afterward.

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join myk8s.helloyuan.site:6443 --token 8c
    --discovery-token-ca-cert-hash sha256:901
```

### proxy-docker-compose.yaml (獨立一台機器)
1. 製作 nginx load balancer，依照真實環境修改 nginx.conf
2. nginx.conf 設定 upstream server

### 利用 kubeadm 創建高可用集群的使用教學
1. 利用 proxy-docker-compose 創建 loadbalancer
2. 利用 prerequisite 腳本 "安裝 kubernetes 叢集" 的前置條件和環境
3. 設定 kubeadm 初始化 kubernetes 集群的 master node 
