FROM python:3.6.8-alpine3.10
LABEL maintainer="takahiro.yamaki@example.com"

RUN set -x \
    && apk add --no-cache \
        openssh-client \
        gcc \
        musl-dev \
        libffi-dev \
        openssl-dev \
    && adduser -D ansible

USER ansible
WORKDIR /home/ansible

RUN set -x \
    && id  \
    && ssh-keygen -t rsa -b 4096 -N "" -f "/home/ansible/.ssh/id_rsa" \
    && pip3 install --user ansible

ENV PATH $PATH:/home/ansible/.local/bin

# Version info
RUN ansible --version
