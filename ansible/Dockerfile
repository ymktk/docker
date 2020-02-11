FROM centos:centos7.7.1908
LABEL maintainer="takahiro.yamaki@example.com"

RUN set -x \
    && bash \
    && yum update  -y \
    && yum install python3-pip -y \
    && useradd -m ansible

USER ansible
WORKDIR /tmp

RUN set -x \
    && id  \
    && pip3 install --user ansible

ENV PATH $PATH:/home/ansible/.local/bin

# Version info
RUN cat /etc/redhat-release \
    && ansible --version
