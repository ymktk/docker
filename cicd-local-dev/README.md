
## Prepare docker images

### 1. Jenkins Master test machine blank image

```bash
cd /path/to/docker/cicd-local-dev/jenkins-master/
docker build -t jenkins-master:blank .
```

### 2. Ansible Controller

```bash
cd /path/to/docker/cicd-local-dev/ansible_controller/centos7/
DOCKER_BUILDKIT=1 docker build -t ansible_controller:0.1 .
```


## Run local k8s cluster

```bash
$ cd /path/to/docker/cicd-local-dev/k8s/

$ kubectl apply -f  local-dev.yaml

$ kubectl exec -it $(kubectl get pods -l app=jenkins-pod -o jsonpath='{.items[*].metadata.name}') -- /bin/bash


### To see info
# $ kubectl get pods --show-labels
# $ kubectl get -f local-dev.yaml
# $ kubectl get deployment jenkins

### Confirm Jenkins Pod IP
# $ kubectl get pods -l app=jenkins-pod -o wide
# $ kubectl get pods -l app=jenkins-pod -o yaml | grep "podIP:"
# $ kubectl get pods -l app=jenkins-pod -o custom-columns="NAME:{metadata.name}, IP:{status.podIP}"

### Service info
# $ kubectl get svc jenkins-master-nodeport
# $ kubectl describe svc jenkins-master-nodeport

### FYI SSH access within cluster
# $ ssh root@jenkins-master-clusterip

### If you want to delete
# $ kubectl delete -f local-dev.yaml
```

### Start Ansible container

```bash
docker run -it --rm -v /c/Users/Public/Downloads:/tmp/downloads \
                    -v /c/Users/Public/repos:/home/ansible/repos \
                    ansible_controller:0.1 bash

### SSH access from external
###   jenkins-master-nodeport > nodePort
ssh -p 30022 root@host.docker.internal

### FYI from WSL2 terminal
# $ ssh -p 30022 root@localhost

### FYI Get private key of Jenkins
# $ kubectl exec -it $(kubectl get pods -l app=jenkins-pod -o jsonpath='{.items[*].metadata.name}') -- cat /root/.ssh/id_rsa

```

### References

+ [kubectlチートシート](https://kubernetes.io/ja/docs/reference/kubectl/cheatsheet/)
+ [実行中のコンテナへのシェルを取得する](https://kubernetes.io/ja/docs/tasks/debug-application-cluster/get-shell-running-container/)
  + [Get a Shell to a Running Container](https://kubernetes.io/docs/tasks/debug-application-cluster/get-shell-running-container/)
+ ストレージ
  + [ストレージにボリュームを使用するPodを構成する](https://kubernetes.io/ja/docs/tasks/configure-pod-container/configure-volume-storage/)

