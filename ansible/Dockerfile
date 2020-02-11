FROM centos:centos7.7.1908
LABEL maintainer="takahiro.yamaki@example.com"

RUN set -x \
    && yum update  -y \
    && yum install python3-pip -y \
    && useradd -m ansible

USER ansible
WORKDIR /home/ansible

RUN set -x \
    && id  \
    && pip3 install --user ansible

ENV PATH $PATH:/home/ansible/.local/bin

# Version info
RUN cat /etc/redhat-release \
    && ansible --version
