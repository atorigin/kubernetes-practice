# 安裝 Helm ( Deprecate , it is helm2 , the latest version is helm3 )

1. 先安裝 helm client 工具
```
curl -LO https://git.io/get_helm.sh
chmod 700 get_helm.sh
./get_helm.sh
```
2. 配置 tiller 所對應的 rbac 設定  
  a. 採用 service account with cluster-admin role 的方式   
  b. 參考 [官方文件](https://helm.sh/docs/using_helm/#example-service-account-with-cluster-admin-role)   
  c. cluster-admin 在 kubernetes cluster 初始化時會被自動創建，因此這個範例不需要多創建一個 cluster-admin 的 cluster role   
```
kubectl create -f rbac-config.yaml
```
3. helm init - 安裝 tiller
```
helm init --service-account tiller --history-max 200
```
4. 補充說明  
  a. 還有其他方式的可以調整 tiller rbac 設定，以應對不同的應用場景，例如：:point_down:   
  b. 參考 [官方文件](https://helm.sh/docs/using_helm/#example-deploy-tiller-in-a-namespace-restricted-to-deploying-resources-only-in-that-namespace)
