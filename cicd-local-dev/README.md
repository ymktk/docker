# How to use for local CI/CD development

## 1. Prepare docker images

### 1-1. Jenkins Master test machine blank image

```bash
cd /path/to/docker-k8s/cicd-local-dev/jenkins-master/
DOCKER_BUILDKIT=1 docker build -t jenkins-master:base .

### Get private key of Jenkins
$ export TMPDWL=/c/Users/Public/Downloads
docker run --rm jenkins-master:blank cat /root/.ssh/id_rsa > $TMPDWL/jenkins-id_rsa
# $ kubectl exec -it $(kubectl get pods -l app=jenkins-pod -o jsonpath='{.items[*].metadata.name}') -- cat /root/.ssh/id_rsa > $TMPDWL/jenkins-id_rsa

$ ls -l $TMPDWL/jenkins-id_rsa
$ cat   $TMPDWL/jenkins-id_rsa
```

### 1-2. Ansible Controller

```bash
cd /path/to/docker-k8s/cicd-local-dev/ansible_controller/centos7/
DOCKER_BUILDKIT=1 docker build -t ansible_controller .
```

### 1-3. Builder (OpenJDK11 + Gradle)

```bash
cd /path/to/docker-k8s/cicd-local-dev/builder/gradle/
DOCKER_BUILDKIT=1 docker build -t builder_gradle .

docker run -it --rm -v /c/Users/Public/repos:/home/jenkins/repos builder_gradle bash
```


## 2. Apply to local k8s cluster

```bash
$ cd /path/to/docker-k8s/cicd-local-dev/k8s/

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

### 3. Start Ansible container

```bash
### FYI SSH access from external
###   jenkins-master-nodeport > nodePort
# $ ssh -p 30022 root@host.docker.internal
### password -> /path/to/docker-k8s/cicd-local-dev/jenkins-master/Dockerfile

### FYI SSH access from WSL2 terminal
# $ ssh -p 30022 root@localhost

$ docker run -it --rm \
          -v /c/Users/Public/Downloads:/tmp/downloads \
          -v /c/Users/Public/repos:/home/ansible/repos \
          ansible_controller:latest bash

### Connection test
$ cd ~/repos/ansible/roles/
$ ssh -p 30022 -i /tmp/downloads/jenkins-id_rsa root@host.docker.internal
$ ansible -i inventory jenkins -m ping -u root -vvv
```

### Setup Jenkins Master

```bash
# tomcat 9, Unarchive tomcat.tar.gz + Setup tomcat (common)
$ cd ~/repos/ansible/roles/
$ ansible-playbook -i inventory playbook-build-tomcat.yml --list-tasks
$ ansible-playbook -i inventory playbook-build-tomcat.yml -vv


# Jenkins, Install Master wo plugins
$ cd ~/repos/ansible/roles/
$ ansible-playbook -i inventory playbook-build-jenkins.yml --list-tasks
$ ansible-playbook -i inventory playbook-build-jenkins.yml -vv


# Start jenkins @ jenkins-pod
$ kubectl exec -it $(kubectl get pods -l app=jenkins-pod -o jsonpath='{.items[*].metadata.name}') -- /bin/bash
$ su - jenkins
$ /app/var/lib/tomcats/jenkins2/bin/instance.sh start

http://localhost:30088/jenkins/

$ cat /app/var/lib/jenkins_home/secrets/initialAdminPassword

# Use this ID & PW
# ->  /path/to/ansible/roles/jenkins/defaults/main.yml
# --> jenkins_admin_username
# --> jenkins_admin_password

# Jenkins, Install Jenkins plugins
# 多すぎてタイムアウトしだしたら、少しずつにして、インストール & Jenkins再起動を繰り返す
$ cd ~/repos/ansible/roles/
$ ansible-playbook -i inventory playbook-build-jenkins.yml --tags "plugins" --list-tasks
$ ansible-playbook -i inventory playbook-build-jenkins.yml --tags "plugins" -vv

```


### Setup Artifactory

- TODO inject config file?

// http://localhost:30881/
http://localhost:30882/ui/

Initial_ID: admin/password
e.g. password123

### References

+ [Installing Artifactory with Docker](https://www.jfrog.com/confluence/display/RTF6X/Installing+with+Docker)
+ [kubectlチートシート](https://kubernetes.io/ja/docs/reference/kubectl/cheatsheet/)
+ [実行中のコンテナへのシェルを取得する](https://kubernetes.io/ja/docs/tasks/debug-application-cluster/get-shell-running-container/)
  + [Get a Shell to a Running Container](https://kubernetes.io/docs/tasks/debug-application-cluster/get-shell-running-container/)
+ ストレージ
  + [ストレージにボリュームを使用するPodを構成する](https://kubernetes.io/ja/docs/tasks/configure-pod-container/configure-volume-storage/)

