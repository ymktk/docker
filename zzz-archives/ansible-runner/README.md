# Ansible Runner

## Sample 1

    docker pull ansible/ansible-runner:1.4.4

    # Run this demo playbook
    # https://github.com/ansible/ansible-runner/blob/master/demo/project/test.yml
    docker run --rm -e RUNNER_PLAYBOOK=test.yml ansible/ansible-runner:1.4.4

    # Run this demo role
    # https://github.com/ansible/ansible-runner/tree/master/demo/project/roles/testrole
    docker run --rm -e RUNNER_ROLE=testrole ansible/ansible-runner:1.4.4


## Sample 2

If you want to run your own role...


## Reference

- [Github code](https://github.com/ansible/ansible-runner)
- [Document by Reahat](https://ansible-runner.readthedocs.io/_/downloads/en/latest/pdf/)
- [Ansible Runner demo](https://github.com/ansible/ansible-runner/tree/master/demo)
- [Docker HUB > ansible > ansible-runner](https://hub.docker.com/r/ansible/ansible-runner)

