## ALB Controller example used NginX image

### Application Load Balancer used Ingress

``` deployment.yaml```
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```


```Service.yaml```
```
apiVersion: v1
kind: Service
metadata:
  name: nginx-application
  annotations:
    alb.ingress.kubernetes.io/healthcheck-path: "/"
spec:
  selector:
    app: nginx
  type: NodePort
  ports:
    - port: 80 # Service.yaml Port
      targetPort: 80 # deployments access port
      protocol: TCP
```


```Ingress.yaml```
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
    name: "backend-ingress"
    namespace: default
    annotations:
      kubernetes.io/ingress.class: alb
      alb.ingress.kubernetes.io/scheme: internet-facing  
      alb.ingress.kubernetes.io/target-type: ip
spec:
    rules:
    - http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: "nginx-application"
                port:
                  number: 80
```

### Network load Balancer used Service

``` deployment.yaml ```
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

```Service.yaml```
```
apiVersion: v1
kind: Service
metadata:
  name: Service
  annotations:
    alb.ingress.kubernetes.io/healthcheck-path: "/"
    service.beta.kubernetes.io/aws-load-balancer-type: "external"
    service.beta.kubernetes.io/aws-load-balancer-nlb-target-type: "ip"
spec:
  selector:
    app: nginx
  type: NodePort
  ports:
    - port: 80 # Service.yaml Port
      targetPort: 80 # deployments access port
      protocol: TCP
```

