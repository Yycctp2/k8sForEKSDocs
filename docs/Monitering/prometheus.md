# Get control plane metrics used Prometheus

## get raw metrics

```kubectl get --raw /metrics ```
```
workqueue_work_duration_seconds_bucket{name="crd_autoregistration_controller",le="1"} 64
workqueue_work_duration_seconds_bucket{name="crd_autoregistration_controller",le="10"} 64
workqueue_work_duration_seconds_bucket{name="crd_autoregistration_controller",le="+Inf"} 64
workqueue_work_duration_seconds_sum{name="crd_autoregistration_controller"} 0.001053377
workqueue_work_duration_seconds_count{name="crd_autoregistration_controller"} 64
workqueue_work_duration_seconds_bucket{name="crd_finalizer",le="1e-08"} 0
workqueue_work_duration_seconds_bucket{name="crd_finalizer",le="1e-07"} 0
workqueue_work_duration_seconds_bucket{name="crd_finalizer",le="1e-06"} 0
workqueue_work_duration_seconds_bucket{name="crd_finalizer",le="9.999999999999999e-06"} 0
workqueue_work_duration_seconds_bucket{name="crd_finalizer",le="9.999999999999999e-05"} 0
workqueue_work_duration_seconds_bucket{name="crd_finalizer",le="0.001"} 0
workqueue_work_duration_seconds_bucket{name="crd_finalizer",le="0.01"} 0
workqueue_work_duration_seconds_bucket{name="crd_finalizer",le="0.1"} 0
workqueue_work_duration_seconds_bucket{name="crd_finalizer",le="1"} 0
workqueue_work_duration_seconds_bucket{name="crd_finalizer",le="10"} 0
workqueue_work_duration_seconds_bucket{name="crd_finalizer",le="+Inf"} 0
workqueue_work_duration_seconds_sum{name="crd_finalizer"} 0
workqueue_work_duration_seconds_count{name="crd_finalizer"} 0
workqueue_work_duration_seconds_bucket{name="crd_naming_condition_controller",le="1e-08"} 0
...
```

## Deploy Prometheus

deploy prometheus use to helm

* create prometheus namespace    

        kubectl create namespace prometheus

* add prometheus-community chart repo
    
        helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

* deploy prometheus
    
        helm upgrade -i prometheus prometheus-community/prometheus \
            --namespace prometheus \
            --set alertmanager.persistentVolume.storageClass="gp2",server.persistentVolume.storageClass="gp2"

* port-forward Control-plane prometheus to localhost:9090

        kubectl --namespace=prometheus port-forward deploy/prometheus-server 9090 --address='0.0.0.0'

    now you can access to prometheus ```Control_plane-ip-address:9090```