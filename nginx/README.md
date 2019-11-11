

# Sample 1

http://localhost:7777/

```bash
# service (type: LoadBalancer) -> deployment -> replicaset -> pod

# Apply (Create)
kubectl apply -f k8s-sample1.yaml

# Apply
kubectl delete -f k8s-sample1.yaml

```

# Sample 2 (Internal Network, LB in a cluster)


```bash
# service (type: ClusterIP) -> deployment -> replicaset -> pod

$ kubectl get svc
NAME            TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)    AGE
nginx-service   ClusterIP   10.97.5.194   <none>        7000/TCP   10s

# Can't reach -> http://localhost:7000/

# Can reach from a pod in the same cluster
kubectl run -it --rm --image centos:centos7.6.1810 --restart=Never testpod -- curl -s http://nginx-service:7000
kubectl run -it --rm --image centos:centos7.6.1810 --restart=Never testpod -- curl -s http://nginx-service.default:7000
kubectl run -it --rm --image centos:centos7.6.1810 --restart=Never testpod -- curl -s http://nginx-service.default.svc.cluster.local:7000

```

# Sample 3 (Expose a Service)


```bash
# service (type: NodePort, k8s Node port(30000)->ClusterIP port(7010)->) -> deployment -> replicaset -> pod

$ kubectl get svc
NAME         TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
nginx-svc    NodePort    10.103.83.234   <none>        7010:30000/TCP   22s


# Can reach -> http://localhost:30000/

# Also you can reach from a pod in the same cluster
kubectl run -it --rm --image centos:centos7.6.1810 --restart=Never testpod -- curl -s http://nginx-svc.default.svc.cluster.local:7010

```

# Sample 4 (Ingress)

```bash
# ingress -> service (type: NodePort) -> deployment -> replicaset -> pod

$ kubectl get svc
NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
nginx1-svc   NodePort    10.105.242.188   <none>        7020:31975/TCP   71s

$ kubectl get ingress
NAME            HOSTS   ADDRESS   PORTS   AGE
nginx-ingress   *                 80      13s

# Can reach -> http://localhost/

# Also you can reach from a pod in the same cluster
kubectl run -it --rm --image centos:centos7.6.1810 --restart=Never testpod -- curl -s http://nginx1-svc.default.svc.cluster.local:7020

```
