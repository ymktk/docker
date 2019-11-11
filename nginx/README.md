

# Sample 1

http://localhost:7777/

```bash
# service (type: LoadBalancer) -> deployment -> replicaset -> pod

# Apply (Create)
kubectl apply -f k8s-sample1.yaml

# Apply
kubectl delete -f k8s-sample1.yaml

```

# Sample 2


```bash
# service (type: ClusterIP) -> deployment -> replicaset -> pod

$ kubectl get svc
NAME            TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)    AGE
nginx-service   ClusterIP   10.97.5.194   <none>        7000/TCP   10s

# Can't reach -> http://localhost:7000/

# Can reach from a pod in the same cluster
kubectl run -it --rm --image centos:centos7.6.1810 --restart=Never testpod -- curl -s http://nginx-service:7000

```

