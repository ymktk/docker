# Useful Docker Commands

```bash
# Delete old instances
docker ps -a -q | xargs docker rm
docker container prune

# Delete old images which don't have TAG
docker images --filter "dangling=true" -q | xargs docker rmi
docker image prune

# Delete snapshots
sudo docker images | awk '/^.*snapshot.*/ {print $3}'                        | xargs docker rmi

# Delete more than 7 days
sudo docker images | grep rwasp-docker | grep 'weeks ago' | awk '{print $3}' | xargs docker rmi
```


# Basic Commands

```bash
# docker build -t ${new image name} ${Docker file directory}
docker image build -t hoge .
docker image build -t test/dockerdesu:v1 ./Docker/study/

```
