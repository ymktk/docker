FROM gradle:6.6.0-jdk11

WORKDIR /etc
RUN ln -nfs ../usr/share/zoneinfo/Singapore localtime \
    && addgroup --gid 510 jenkins \
    && adduser  --gid 510 --uid 510 jenkins --disabled-password

USER jenkins
WORKDIR /home/jenkins
