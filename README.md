# JP's AWS Load Balancer Controller Lab

### You can run this lab either from your local computer or for AWS Cloud9. If you opt for AWS Cloud9, please follow the link bellow to create, connect to your Cloud9 environment, and open a terminal to get started.

Instructions: https://docs.aws.amazon.com/cloud9/latest/user-guide/environments.html

### Clone this repo
```bash
git clone https://github.com/jpbueno/lb-controller.git
```

### Install eksctl
```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
```

### Create an EKS cluster with a managed node group having 3 On-Demand t3.medium nodes and a label called lifecycle=OnDemand

```bash
eksctl create cluster --version=1.18 --name=eks-spot-lab --node-private-networking --managed --nodes=3 --alb-ingress-access --region=us-east-1 --node-type t3.medium --node-labels="lifecycle=OnDemand" --asg-access
```
### kube-ops-view

***Install kube-ops-view***

```bash
cd kube-ops-view
kubectl create ns kube-ops-view-ns
kubectl apply -k deploy -n kube-ops-view-ns
```

***Open kube-ops-view***

```bash
kubectl port-forward service/kube-ops-view 8080:80
```