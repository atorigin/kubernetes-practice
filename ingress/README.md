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
vim values.yaml # 修改 service type -> 這邊示範使用 NodePort，預設原本是 Loadbalance
helm install stable/nginx-ingress --name my-ingress --namespace nginx-ingress -f values.yaml
```

### output like:
```
NAME:   my-ingress
LAST DEPLOYED: Tue Aug 20 06:29:19 2019
NAMESPACE: nginx-ingress
STATUS: DEPLOYED

RESOURCES:
==> v1/Pod(related)
NAME                                                       READY  STATUS             RESTARTS  AGE
my-ingress-nginx-ingress-controller-6c46bc87db-zhbpv       0/1    ContainerCreating  0         0s
my-ingress-nginx-ingress-default-backend-78c8b449f9-tn8qt  0/1    ContainerCreating  0         0s

==> v1/Service
NAME                                      TYPE          CLUSTER-IP    EXTERNAL-IP  PORT(S)                     AGE
my-ingress-nginx-ingress-controller       LoadBalancer  10.96.71.252  <pending>    80:31775/TCP,443:30848/TCP  0s
my-ingress-nginx-ingress-default-backend  ClusterIP     10.106.17.2   <none>       80/TCP                      0s

==> v1/ServiceAccount
NAME                      SECRETS  AGE
my-ingress-nginx-ingress  1        0s

==> v1beta1/ClusterRole
NAME                      AGE
my-ingress-nginx-ingress  0s

==> v1beta1/ClusterRoleBinding
NAME                      AGE
my-ingress-nginx-ingress  0s

==> v1beta1/Deployment
NAME                                      READY  UP-TO-DATE  AVAILABLE  AGE
my-ingress-nginx-ingress-controller       0/1    1           0          0s
my-ingress-nginx-ingress-default-backend  0/1    1           0          0s

==> v1beta1/Role
NAME                      AGE
my-ingress-nginx-ingress  0s

==> v1beta1/RoleBinding
NAME                      AGE
my-ingress-nginx-ingress  0s


NOTES:
The nginx-ingress controller has been installed.
It may take a few minutes for the LoadBalancer IP to be available.
You can watch the status by running 'kubectl --namespace nginx-ingress get services -o wide -w my-ingress-nginx-ingress-controller'

An example Ingress that makes use of the controller:

  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    annotations:
      kubernetes.io/ingress.class: nginx
    name: example
    namespace: foo
  spec:
    rules:
      - host: www.example.com
        http:
          paths:
            - backend:
                serviceName: exampleService
                servicePort: 80
              path: /
    # This section is only required if TLS is to be enabled for the Ingress
    tls:
        - hosts:
            - www.example.com
          secretName: example-tls

If TLS is enabled for the Ingress, a Secret containing the certificate and key must also be provided:

  apiVersion: v1
  kind: Secret
  metadata:
    name: example-tls
    namespace: foo
  data:
    tls.crt: <base64 encoded cert>
    tls.key: <base64 encoded key>
  type: kubernetes.io/tls
```

----

#### 小小實驗室

* 驗證 ingress 是否可以有效轉發

* 小技巧：設定 dns 解析可以修改 /etc/hosts 檔案來進行測試驗證 -> 僅針對本機的解析(正規流程需要透過 dns 服務供應商設定對應的 dns 與 ip)

* 實驗室步驟
  * 創建 web 的 deployment -> web 服務
  * 創建 web 的 service -> 讓 web 可被外部訪問
  * 創建 web 的 ingress -> 透過 ingress 控制外部如何訪問到 service

```
kubectl apply -f web-deployment.yaml -n default
kubectl apply -f web-service.yaml -n default
kubectl apply -f web-ingress.yaml -n default
```

#### :star2: 補充說明 - dns 須依環境配置正確，只要是 NodePort 的 service type，當訪問 cluster 內的所有 public ip 都可以找到 ingress controller 幫忙轉發到對應的 service
```
# dns record sample
cluster-instance1-public-ip blue.yourdomain.com
cluster-instance2-public-ip purple.yourdomain.com
```
