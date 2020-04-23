# Environment
- OS : ubuntu:18.04
- Need have zip tools ( sudo apt-get install zip -y )
- Base on $SHELL=BASH

## Reference
- [About eksctl create cluster template yaml](https://github.com/weaveworks/eksctl/tree/master/examples)
- [Introduce eksctl command usage and command example document](https://eksctl.io/usage/managing-nodegroups/)
- [aws-eks-cloudformation-template](https://github.com/aws-quickstart/quickstart-amazon-eks/blob/master/templates/amazon-eks.template.yaml)

#### :star: More details please go to reference

## prerequisite
- aws configure ( or AWS IAM Role )
- if you want to using ` kubectl ` tool , you need to install following step
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
kubectl version --client
echo 'source <(kubectl completion bash)' >>~/.bashrc # kubectl completeion setting
source ~/.bashrc
```

### Create eks cluster usage
- Into vpc directory using terraform command to create vpc infra setting
  - two public subnet and make auto assign public address
- Into eks directory using eksctl command create cluster and managed nodegroup
  - that allow ssh to worker nodes , so ~ ensure your public ssh key into the path ( such my yaml setting ~/.ssh/owen.pem )
  - how to create ? ` eksctl create cluster -f eks-cluster.yaml `

#### :star: For this yaml , you need to create vpc on your aws cloud , because it will using exists vpc to create eks cluster control-plane and worker-node.
