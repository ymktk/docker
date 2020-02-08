# Docker for Ansible operations
This docker is having
- Python 3.6.8
- Ansible 2.9.4


# Usage

```bash
docker-compose up -d

docker exec -it ansible bash

docker-compose down
```

As ansible user
```bash
cd ~

source ansible-py3/bin/activate

ansible --version

```

# References

- [[Ansible] CentOS 8 に Ansible をインストールする（Python 3 + venv + pip）](https://tekunabe.hatenablog.jp/entry/2019/10/06/ansible_centos8_python3_pip)
