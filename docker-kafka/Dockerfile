FROM ubuntu:20.04

ARG corretto_version=15.0.1.9-1

SHELL ['/bin/sh', '-e', '-u', '-x', '-c']

RUN set -eux \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        curl ca-certificates gnupg software-properties-common fontconfig java-common \
    && curl -fL https://apt.corretto.aws/corretto.key | apt-key add - \
    && add-apt-repository 'deb https://apt.corretto.aws stable main' \
    && mkdir -p /usr/share/man/man1 || true \
    && apt-get update \
    && apt-get install -y java-15-amazon-corretto-jdk=1:$version \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
        curl gnupg software-properties-common

ENV LANG C.UTF-8
ENV JAVA_HOME=/usr/lib/jvm/java-15-amazon-corretto

# RUN apt-key adv --keyserver keyserver.ubuntu.com --recv 99E82A75642AC823 \
#     && add-apt-repository -y \
#         "deb http://dl.bintray.com/sbt/debian /" \
#     && apt-get update \
#     && apt-get install -y \
#         scala \
#         git
