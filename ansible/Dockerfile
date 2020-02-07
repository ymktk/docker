FROM centos:centos8.1.1911
LABEL maintainer="takahiro.yamaki@example.com"

RUN set -x \
    && dnf update  -y \
    && dnf install sudo -y \
    && dnf install python3-pip -y \
    && useradd -m ansible \
    && echo "ansible:ansible" | chpasswd
    # && echo 'ansible ALL=(ALL) ALL' >> /etc/sudoers

USER ansible
WORKDIR /tmp

RUN set -x \
    && id \
    && pip3 install --user ansible

# Version info
RUN cat /etc/redhat-release \
    && ansible --version
