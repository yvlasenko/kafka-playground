FROM ubuntu:20.04

ARG CORRETTO_VERSION=15.0.1.9-1

SHELL ["/bin/sh", "-e", "-u", "-x", "-c"]

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        ca-certificates \
        fontconfig \
        gnupg \
        java-common \
        software-properties-common \
        wget \
    && wget -qO- https://apt.corretto.aws/corretto.key | apt-key add - \
    && add-apt-repository 'deb https://apt.corretto.aws stable main' \
    && mkdir -p /usr/share/man/man1 || true \
    && apt-get update \
    && apt-get install -y java-15-amazon-corretto-jdk=1:${CORRETTO_VERSION} \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false gnupg software-properties-common

ENV LANG C.UTF-8
ENV JAVA_HOME=/usr/lib/jvm/java-15-amazon-corretto
