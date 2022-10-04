# EKS_Auth

k8s cluster is controlled by kubectl(command line tool) EKS can auth k8s RBAC(Role_Based_Access_Controll) by IAM identity. 


you can check identity as followed code
```
aws sts get-caller-identity
```

EKS is attached your AWS identity to rbac_config_file 

