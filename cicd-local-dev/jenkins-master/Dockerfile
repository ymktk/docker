FROM  centos:centos7.8.2003
LABEL maintainer="takahiro.yamaki@example.com"

RUN set -x \
    && yum install -y \
            curl \
            libselinux-python \
            initscripts \
            git \
            openssh-clients \
            openssh-server-sysvinit.x86_64 \
            openssh.x86_64 \
            openssh-server.x86_64 \
            initscripts.x86_64 \
            java-11-openjdk-devel \
    && mkdir /var/run/sshd \
    && echo 'root:password' | chpasswd \
    && ssh-keygen -t rsa -b 1024 -N "" -f "/root/.ssh/id_rsa" \
    && cp /root/.ssh/id_rsa.pub /root/.ssh/authorized_keys \
    && chmod 600 /root/.ssh/authorized_keys \
    && groupadd -g 500 tomcat \
    && useradd  -g 500 -u 500 -m tomcat \
    && groupadd -g 510 jenkins \
    && useradd  -g 510 -u 510 -m jenkins -G tomcat

WORKDIR /etc
RUN ln -nfs ../usr/share/zoneinfo/Asia/Singapore localtime

#USER jenkins
#WORKDIR /home/jenkins
#RUN  ssh-keygen -t rsa -b 1024 -N "" -f "/home/jenkins/.ssh/id_rsa"

EXPOSE 22
EXPOSE 8080

# CMD ["/etc/init.d/sshd", "start"]
