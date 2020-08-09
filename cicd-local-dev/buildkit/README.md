kubectl apply -f deployment.yaml

kubectl get pods

### kubectl port-forward pod/<buildkitのpod名> 1234:1234

kubectl port-forward pod/buildkitd-56c6cd7dbf-2zm7j 1234:1234

export BUILDKIT_HOST=tcp://127.0.0.1:1234


which buildctl

buildctl --version

buildctl build \
    --output type=image,name=ymktk/test:hoge,push=false \
    --frontend=dockerfile.v0 \
    --local context=. \
    --local dockerfile=/c/Users/Public/repos/docker/ansible/alpine3.10/


# Reference

- [buildkitを使ってKubernetesクラスタでDockerのコンテナイメージをビルドする方法](https://qiita.com/MasafumiTsuyuki/items/524e042b8a20475c3745)
