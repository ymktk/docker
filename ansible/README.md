# Docker for Ansible operations
This docker is having
- Ansible 2.9.5


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
```

# References

- [[Ansible] CentOS 8 に Ansible をインストールする（Python 3 + venv + pip）](https://tekunabe.hatenablog.jp/entry/2019/10/06/ansible_centos8_python3_pip)
- [AnsibleをPython2.xからPython3.xに対応させる手順とトラブルシューティング](https://qiita.com/comefigo/items/766d42100356bdea8ff8)
