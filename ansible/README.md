# Docker for Ansible operations
This docker is having
- Ansible 2.9.11
- github.com/moby/buildkit v0.7.2
- kubectl v1.18.6


# Usage

```bash

cd /path/to/ansible/

COMPOSE_DOCKER_CLI_BUILD=1 DOCKER_BUILDKIT=1 docker-compose build

docker-compose up -d

docker exec -it ansible bash

docker-compose down
```

As ansible user
```bash
python3 -V
pip3 -V
ansible --version
buildctl --version
kubectl version --client

```

# References

- [moby/buildkit releases](https://github.com/moby/buildkit/releases)
- [[Ansible] CentOS 8 に Ansible をインストールする（Python 3 + venv + pip）](https://tekunabe.hatenablog.jp/entry/2019/10/06/ansible_centos8_python3_pip)
- [AnsibleをPython2.xからPython3.xに対応させる手順とトラブルシューティング](https://qiita.com/comefigo/items/766d42100356bdea8ff8)
