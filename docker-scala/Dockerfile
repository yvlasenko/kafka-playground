FROM yvlasenko/corretto

ARG SCALA_VERSION=2.13.4

SHELL ["/bin/sh", "-e", "-u", "-x", "-c"]

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        curl \
    && curl "https://downloads.lightbend.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.deb" \
        -o "scala-${SCALA_VERSION}.deb" \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false curl
