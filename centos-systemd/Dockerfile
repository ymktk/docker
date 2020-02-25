FROM centos/systemd
LABEL maintainer="takahiro.yamaki@example.com"

RUN set -x \
    && yum update  -y \
    && yum install \
            openssh-server \
            sudo -y \
    && yum clean all \
    && useradd -m jenkins \
    && useradd -m tomcat  \
    && mkdir -m 700 /root/.ssh \
    && systemctl enable sshd.service

# RUN rm /var/run/nologin

RUN echo    'jenkins ALL=NOPASSWD: /bin/mkdir'     >> /etc/sudoers \
    && echo 'jenkins ALL=NOPASSWD: /bin/curl'      >> /etc/sudoers \
    && echo 'jenkins ALL=NOPASSWD: /bin/rpm'       >> /etc/sudoers \
    && echo 'jenkins ALL=NOPASSWD: /bin/yum'       >> /etc/sudoers \
    && echo 'jenkins ALL=NOPASSWD: /bin/systemctl' >> /etc/sudoers

USER jenkins
WORKDIR /home/jenkins
RUN  ssh-keygen -t rsa -b 4096 -N "" -f "/home/jenkins/.ssh/id_rsa"

USER root

EXPOSE 80
EXPOSE 8081
EXPOSE 8082

CMD ["/usr/sbin/init"]
