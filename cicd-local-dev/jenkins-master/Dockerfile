FROM  centos/systemd
LABEL maintainer="takahiro.yamaki@example.com"

COPY authorized_keys.txt /root/.ssh/authorized_keys

RUN set -x \
    && yum update  -y \
    && yum install \
            openssh-server -y \
    && chmod 700 /root/.ssh \
    && chmod 600 /root/.ssh/authorized_keys \
    && useradd -m jenkins \
    && useradd -m tomcat  \
    && systemctl enable sshd.service

#USER jenkins
#WORKDIR /home/jenkins
#RUN  ssh-keygen -t rsa -b 4096 -N "" -f "/home/jenkins/.ssh/id_rsa"

#USER tomcat
#WORKDIR /home/tomcat
#RUN ssh-keygen -N "" -f "/home/tomcat/.ssh/id_rsa"

#USER root

#EXPOSE 80
#EXPOSE 8081
#EXPOSE 8082
#EXPOSE 8083

CMD ["/usr/sbin/init"]
