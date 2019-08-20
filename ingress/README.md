# Ingress 說明

* An API object that manages external access to the services in a cluster, typically HTTP.

* Ingress exposes HTTP and HTTPS routes from outside the cluster to services within the cluster.

## 前提

* You must have an ingress controller to satisfy an Ingress.

* You can choose from a number of [Ingress controllers](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/).

## 安裝方式

* 透過 kubectl 安裝相關工具在 kubernetes cluster 中 - 以 nginx 為例
[參考文件](https://kubernetes.github.io/ingress-nginx/deploy/)

* 透過 kubenetes 的套件管理工具 Helm 安裝
[參考文件](https://github.com/helm/charts/tree/master/stable/nginx-ingress)

## 安裝指令

```
helm install stable/nginx-ingress --name my-ingress -f values.yaml
```
