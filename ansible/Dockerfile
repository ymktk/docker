FROM centos:centos7.7.1908
LABEL maintainer="takahiro.yamaki@example.com"

RUN set -x \
    && yum update  -y \
    && yum install python36 python36-pip python36-devel sudo -y \
    && useradd -m ansible \
    && echo "ansible:ansible" | chpasswd \
    && echo 'ansible ALL=(ALL) ALL' >> /etc/sudoers

USER ansible
WORKDIR /home/ansible

RUN set -x \
    && id  \
    && pip3 install --user ansible

ENV PATH $PATH:/home/ansible/.local/bin

# Version info
RUN cat /etc/redhat-release \
    && ansible --version
