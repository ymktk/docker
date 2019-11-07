From centos:centos7.6.1810
LABEL maintainer="Takahiro Yamaki"

COPY google-cloud-sdk.repo /etc/yum.repos.d/

WORKDIR /tmp
    
RUN set -x \
    && yum update  -y \
    && yum install -y \
       google-cloud-sdk wget unzip \
    && wget  https://releases.hashicorp.com/terraform/0.12.13/terraform_0.12.13_linux_amd64.zip \
    && unzip ./terraform_0.12.13_linux_amd64.zip -d /usr/local/bin/
