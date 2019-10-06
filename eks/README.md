# Reference
- [About eksctl create cluster template yaml](https://github.com/weaveworks/eksctl/tree/master/examples)
- [Introduce eksctl command usage and command example document](https://eksctl.io/usage/managing-nodegroups/)
- [aws-eks-cloudformation-template](https://github.com/aws-quickstart/quickstart-amazon-eks/blob/master/templates/amazon-eks.template.yaml)

# Using eksctl create a simple default cluster
#### Following step
1. Install docker
2. Pull eksctl docker image from weaveworks , command is ` docker pull weaveworks/eksctl `
3. Use ` docker run -it weaveworks/eksctl sh ` command to operate eksctl command ( as you can run ./eksctl-run-docker.sh )
4. aws configure. setup aws environment !! ( If not setup , you will create cluster failed with eksctl )
5. eksctl create cluster --name myeks --node 2 --region ap-northeast-1

## Note - the step5 can use yaml define to create your customize cluster
#### command like : ` eksctl create cluster -f cluster.yaml `

#### :star: More details please go to reference
