FROM openjdk:11-jdk-buster

COPY gradle-6.6-bin.zip /opt/

WORKDIR /etc
RUN ln -nfs ../usr/share/zoneinfo/Singapore localtime

WORKDIR /opt
RUN unzip gradle-6.6-bin.zip \
    && rm gradle-6.6-bin.zip

ENV GRADLE_HOME=/opt/gradle-6.6
ENV PATH=${GRADLE_HOME}/bin:${PATH}
