# Kubernetes

## kubectl commands

    # Confirm current context
    kubectl config get-contexts

    # Change to docker-for-desktop
    kubectl config use-context docker-for-desktop

    # master(Docker for windowsが起動しているPC)が1台起動している
    kubectl get nodes

    #
    kubectl get po --all-namespaces

    # Deploy Dashboard -> https://github.com/kubernetes/dashboard
    # e.g.
    kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml

    kubectl get deployment --namespace=kubernetes-dashboard

    # Get token (https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md)
    kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')

    # ref https://www.skyarch.net/blog/?p=16378

    kubectl proxy

    http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/


    # Confirm current info
    kubectl get all -n=kube-system


# Helm

## Installing Helm

- https://helm.sh/docs/intro/install/
- https://github.com/helm/helm/releases/tag/v3.2.0


    # get tar.gz
    wget https://get.helm.sh/helm-v3.2.0-linux-amd64.tar.gz

    tar -zxvf helm-v3.2.0-linux-amd64.tar.gz

    cd /path/to/linux-amd64/

    sudo mv helm /usr/local/bin/helm

    helm version


## Add charts repository

    helm repo add stable https://kubernetes-charts.storage.googleapis.com/

    helm search repo stable


## Helm commands

    # リリース系

    # チャートからリリースを作成する
    helm install <リリース名> <nginxチャート名>

    # チャート更新があったら、作成済みリリースに更新を適用する
    helm upgrade

    # リリースを削除する
    helm delete

    # リリースをリストアップする
    helm list

    # リリースの情報を表示する
    helm get [values, manifest]


    # チャート系

    # チャートのレポジトリ 一覧、追加、削除、更新
    helm repo list
    helm repo add
    helm repo delete
    helm repo update

    # 自作チャートのひな型を作成する
    helm create

    # チャート内の依存関係を解決する
    helm dependency

    # チャートを検索する
    helm search
