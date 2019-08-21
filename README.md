# kubernetes-practice

* Running on ubuntu 18.04 Server 

* 練習 HA 的 kubernetes cluster 的建置 - stacked control plane and etcd nodes

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

[參考文件](https://medium.com/@saurabh6790/generate-wildcard-ssl-certificate-using-lets-encrypt-certbot-273e432794d7)

[參考文件](https://linuxize.com/post/how-to-install-and-use-docker-compose-on-ubuntu-18-04/)

----
# 關於 Helm - Kubernetes 的套件管理工具

* Helm 基礎觀念 - 一個 Helm 有兩個重要的基本組件(Tiller server 和 helm client)
* 採用官方提供的 "從腳本安裝(From Script)"
* 可以使用 `curl -L https://git.io/get_helm.sh | bash` 指令

[參考文件](https://helm.sh/docs/using_helm/#from-script)

----

# 關於 Ingress - Kubernetes 管理外部訪問的物件

#### 前置說明

* 基本認識 pod , service , ingress-controller 物件在 kubernetes 叢集內的角色和功能

* 對於 Helm 有基礎認識

* 初步掌握 kubectl 指令工具的使用

* ingress 的其他細節說明，例如：安裝，配置設定...等，請參考 ingrees 目錄下的 [README.md](https://github.com/OwenYangGit/kubernetes-practice/blob/master/ingress/README.md)

* 實作小小實驗室前，請初步了解 DNS 運作原理

----

# RBAC - Role based access control

#### 前置說明

* 了解 Service account

* 了解 Role and ClusterRole

* 了解 Rolebinding and ClusterRolebinding
