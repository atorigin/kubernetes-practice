# kubernetes-practice

* Running on ubuntu 18.04 Server 

* 練習 HA 的 kubernetes cluster 的建置

* 本 repo 採用 kubeadm v1.14 , kubelet v1.14 , kubectl v1.14

* 使用 sh prerequisite_env.sh 來進行

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
if you lost the command , you can use:
```
kubeadm token create --ttl 10m --print-join-command # to print join command and set expired time in 10 min

kubeadm init phase upload-certs --experimental-upload-certs # with join control-plane node , you should get the certificate-key
```


### proxy-docker-compose.yaml (獨立一台機器) -> 也可以用 Cloud LoadBalacer (GCP LB or AWS ELB...)
1. 製作 nginx load balancer，依照真實環境修改 nginx.conf
2. nginx.conf 設定 upstream server

### 利用 kubeadm 創建高可用集群的使用教學
1. 利用 proxy-docker-compose 創建 loadbalancer
2. 利用 prerequisite 腳本 "安裝 kubernetes 叢集" 的前置條件和環境
3. 設定 kubeadm 初始化 kubernetes 集群的 master node 

----
# Certbot with https

#### 使用 certbot + nginx 簽發一張 Wildcard certificate

1. 啟用 docker-compose
2. 進入 container 容器後，安裝簽發所需環境
3. 使用 certbot 簽發 Wildcard 憑證

#### 參考
[參考文件](https://medium.com/@saurabh6790/generate-wildcard-ssl-certificate-using-lets-encrypt-certbot-273e432794d7)

[參考文件](https://linuxize.com/post/how-to-install-and-use-docker-compose-on-ubuntu-18-04/)
