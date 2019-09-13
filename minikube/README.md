# Installation
- [參考文件](https://www.radishlogic.com/kubernetes/running-minikube-in-aws-ec2-ubuntu/)
- ubuntu 18.04 LTS on AWS Cloud EC2 instance

# Prerequisite

#### install kubectl
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

chmod + x ./kubectl

sudo mv ./kubectl/usr/local/bin/kubectl
```

#### install docker

```
sudo apt-get update && sudo apt-get install docker.io -y
```

#### install minikube

```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64&& chmod + x minikube && sudo mv minikube /usr/local/bin/
```

#### minikube start

```
sudo -i

minikube start --vm-driver=none
```

# Make a small lab for test

```
kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080

kubectl expose deployment hello-minikube --type=NodePort

kubectl get services

minikube status

curl ${ip}:port
```



