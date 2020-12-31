FROM yvlasenko/corretto

ARG KAFKA_VERSION=2.7.0
ARG SCALA_VERSION=2.13

SHELL ["/bin/sh", "-e", "-u", "-x", "-c"]

RUN wget "https://archive.apache.org/dist/kafka/${KAFKA_VERSION}/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz" \
        -O "/tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz" \
    && echo $(wget -qO- "https://www.apache.org/dist/kafka/${KAFKA_VERSION}/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz.sha512" | sed 's/^.*://g' | tr -d '[:space:]') "/tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz" | sha512sum -c - \
    && tar xf "/tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz" -C /opt \
    && ln -s "/opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION}" /opt/kafka \
    && rm -rf /tmp/*

ENV KAFKA_HOME=/opt/kafka
ENV PATH="${KAFKA_HOME}/bin:${PATH}"
