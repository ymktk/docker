FROM openjdk:11-jdk-buster

COPY gradle-6.6-bin.zip /opt/

WORKDIR /etc
RUN ln -nfs ../usr/share/zoneinfo/Singapore localtime \
    && addgroup --gid 1000 jenkins \
    && adduser  --gid 1000 --uid 1000 jenkins --disabled-password

WORKDIR /opt
RUN unzip gradle-6.6-bin.zip \
    && rm gradle-6.6-bin.zip

ENV GRADLE_HOME=/opt/gradle-6.6
ENV PATH=${GRADLE_HOME}/bin:${PATH}

USER jenkins
WORKDIR /home/jenkins
