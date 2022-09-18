# 기본 설정

***

## kubectl 설치하기

    curl -o kubectl https://s3.us-west-2.amazonaws.com/amazon-eks/1.23.7/2022-06-29/bin/linux/amd64/kubectl
    chmod +x ./kubectl
    mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$PATH:$HOME/bin

## ekctl 설치하기

    curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
    sudo mv /tmp/eksctl /usr/local/bin  

## eksctl 설정하기


먼저 클러스터의 생성 IAM으로 권한을 설정해야 합니다. 아래 명령어를 통해 확인할 수 있습니다.


    aws sts get-caller-identity


그리고 다음 명령어를 통해 클러스터에 kubectl과 eksctl을 설정해줍니다.

    aws eks update-kubeconfig --name $(eks-cluster-name) --region $(cluster-region)
