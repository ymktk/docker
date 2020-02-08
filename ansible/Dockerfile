FROM centos:centos8.1.1911
LABEL maintainer="takahiro.yamaki@example.com"

RUN set -x \
    && dnf update  -y \
    && dnf install python3 -y \
    && useradd -m ansible

USER ansible

RUN set -x \
    && id \
    && python3 -m venv ~/ansible-py3 \
    && source ~/ansible-py3/bin/activate \
    && pip3 install --upgrade pip \
    && pip3 install ansible

# Version info
RUN cat /etc/redhat-release \
    && python3 --version

WORKDIR /home/ansible/
