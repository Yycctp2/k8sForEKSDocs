# Installation ALB Controller

***

## Create IAM Policy

    curl -o iam_policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.4.3/docs/install/iam_policy.json

## Create IAM Role

    eksctl create iamserviceaccount \
    --cluster=$(cluster-name) \
    --namespace=kube-system \
    --name=aws-load-balancer-controller \
    --role-name "AmazonEKSLoadBalancerControllerRole" \
    --attach-policy-arn=arn:aws:iam::$(iam-num):policy/AWSLoadBalancerControllerIAMPolicy \
    --approve

## install to helm chart

Find your region IAM num : [AWS container image registry](https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/add-ons-images.html) and insert to 602401143452 (default region ap-northeast-2)

    helm repo add eks https://aws.github.io/eks-charts
    helm repo update
    helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
    -n kube-system \
    --set clusterName=my-cluster \
    --set serviceAccount.create=false \
    --set serviceAccount.name=aws-load-balancer-controller 
    --set image.repository=602401143452.dkr.ecr.region-code.amazonaws.com/amazon/aws-load-balancer-controller

check that the controller is installed

    kubectl get deployment -n kube-system aws-load-balancer-controller

## install to manifest

deploy cert-manager

    kubectl apply \
    --validate=false \
    -f https://github.com/jetstack/cert-manager/releases/download/v1.5.4/cert-manager.yaml

install the controller

    curl -Lo v2_4_3_full.yaml https://github.com/kubernetes-sigs/aws-load-balancer-controller/releases/download/v2.4.3/v2_4_3_full.yaml
    kubectl apply -f v2_4_3_full.yaml
    curl -Lo v2_4_3_ingclass.yaml https://github.com/kubernetes-sigs/aws-load-balancer-controller/releases/download/v2.4.3/v2_4_3_ingclass.yaml
    kubectl apply -f v2_4_3_ingclass.yaml

check that the controller is installed

    kubectl get deployment -n kube-system aws-load-balancer-controller