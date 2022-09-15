# Setting

***

## Install kubectl

    curl -o kubectl https://s3.us-west-2.amazonaws.com/amazon-eks/1.23.7/2022-06-29/bin/linux/amd64/kubectl
    chmod +x ./kubectl
    mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$PATH:$HOME/bin

## Install eksctl

    curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
    sudo mv /tmp/eksctl /usr/local/bin  

## Configuration eksctl
first config aws credential. cluster ownerd credential  
eksctl&kubectl connecting to EKS Cluster

    aws eks update-kubeconfig --name $(eks-cluster-name) --region $(cluster-region)
