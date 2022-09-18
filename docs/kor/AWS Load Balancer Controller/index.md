# Introduce 

The AWS load balancer can be used as a k8s ingress & service via the ALB controller.


* Service Component is convert to NLB(Network Load Balancer)
* Ingress component is convert to ALB(Application Load Balancer)

ALB Controller is convert annotations to AWS Resource. like this

__```ingress.yaml```__


    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
    name: "ingress-example"
    namespace: default
    annotations:
        kubernetes.io/ingress.class: alb 
        alb.ingress.kubernetes.io/scheme: internet-facing
        alb.ingress.kubernetes.io/target-type: ip
    spec:
    rules:
    - http:
            paths:
            - path: /$(access_path)
                pathType: Prefix
                backend:
                service:
                    name: $(Service_Name)
                    port:
                    number: $(Service_Port)

