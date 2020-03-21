FROM centos:centos7.7.1908
LABEL maintainer="takahiro.yamaki@example.com"

RUN set -x \
    && yum update  -y \
    && yum install \
            python36 \
            python36-pip \
            python36-devel \
            openssh-clients \
            sudo -y \
    && yum clean all \
    && useradd -m ansible \
    && pip3 install ansible

WORKDIR /etc
RUN ln -nfs ../usr/share/zoneinfo/Asia/Singapore localtime

USER ansible
WORKDIR /home/ansible

RUN set -x \
    && id  \
    && ssh-keygen -t rsa -b 4096 -N "" -f "/home/ansible/.ssh/id_rsa"

# Version info
RUN cat /etc/redhat-release \
    && ansible --version
