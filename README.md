# Useful Docker Commands

```bash
# Delete old instances
docker ps -a -q | xargs docker rm

# Delete old images which don't have TAG
docker images --filter "dangling=true" -q | xargs          docker rmi

# Delete snapshots
sudo docker images | awk '/^.*snapshot.*/ {print $3}'                        | xargs docker rmi

# Delete more than 7 days
sudo docker images | grep rwasp-docker | grep 'weeks ago' | awk '{print $3}' | xargs docker rmi
```
