FROM  centos:centos7.8.2003
LABEL maintainer="takahiro.yamaki@example.com"

COPY ./kubernetes.repo /etc/yum.repos.d/

RUN set -x \
    && yum update  -y \
    && yum install -y \
            python36  \
            python36-pip \
            python36-devel  \
            openssh-clients \
            which \
            wget \
            telnet \
            traceroute \
            openssl \
            kubectl \
    && yum clean all \
    && pip3 install ansible

WORKDIR /tmp
RUN wget https://github.com/moby/buildkit/releases/download/v0.7.2/buildkit-v0.7.2.linux-amd64.tar.gz \
    && tar xzf buildkit-v0.7.2.linux-amd64.tar.gz \
    && rm  -f  buildkit-v0.7.2.linux-amd64.tar.gz \
    && mv     ./bin/* /usr/local/bin/ \
    && rm -rf ./bin

WORKDIR /etc
RUN ln -nfs ../usr/share/zoneinfo/Asia/Singapore localtime \
    && groupadd --gid 500 ansible \
    && groupadd --gid 501 tomcat \
    && groupadd --gid 502 jenkins \
    && useradd  --uid 500 --gid 500 --create-home ansible \
    && useradd  --uid 501 --gid 501 --create-home tomcat  \
    && useradd  --uid 502 --gid 502 --create-home jenkins

USER ansible
WORKDIR /home/ansible

# RUN set -x \
#     && id  \
#     && ssh-keygen -t rsa -b 4096 -N "" -f "/home/ansible/.ssh/id_rsa"

# Version info
RUN cat /etc/redhat-release \
    && ansible  --version \
    && buildctl --version \
    && kubectl version --client
