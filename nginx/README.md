

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

# Sample 5 (Ingress, path routing)

```bash
kubectl get all
NAME                                     READY   STATUS    RESTARTS   AGE
pod/nginx-deployment1-59d475f4c4-pmmfd   1/1     Running   0          6m45s
pod/nginx-deployment2-6bb5d9d8f6-8h5zc   1/1     Running   0          6m45s

NAME                 TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/kubernetes   ClusterIP   10.96.0.1       <none>        443/TCP          2d15h
service/nginx1-svc   NodePort    10.99.10.136    <none>        7030:31631/TCP   6m45s
service/nginx2-svc   NodePort    10.107.214.92   <none>        7040:32682/TCP   6m45s

NAME                                READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/nginx-deployment1   1/1     1            1           6m45s
deployment.apps/nginx-deployment2   1/1     1            1           6m45s

NAME                                           DESIRED   CURRENT   READY   AGE
replicaset.apps/nginx-deployment1-59d475f4c4   1         1         1       6m45s
replicaset.apps/nginx-deployment2-6bb5d9d8f6   1         1         1       6m45s

 $ kubectl exec -it nginx-deployment1-59d475f4c4-pmmfd -- mkdir /usr/share/nginx/html/path1
 $ kubectl exec -it nginx-deployment1-59d475f4c4-pmmfd -- cp /etc/hostname /usr/share/nginx/html/path1/index.html
 $ kubectl exec -it nginx-deployment2-6bb5d9d8f6-8h5zc -- mkdir /usr/share/nginx/html/path2
 $ kubectl exec -it nginx-deployment2-6bb5d9d8f6-8h5zc -- cp /etc/hostname /usr/share/nginx/html/path2/index.html

```

http://localhost/path1/
http://localhost/path2/
http://localhost/


# Sample 6 (Nginx proxy)