# How to start

```bash

cd ~

source ansible-py3/bin/activate

ansible --version


# Syntax check
ansible-playbook -i inventory playbook.yml --syntax-check

# Task list
ansible-playbook -i inventory playbook.yml --list-tasks

# Run
# -vvv 詳細情報の表示及び、実行結果をJSONで返す
ansible-playbook -i inventory playbook.yml -vvv

```
