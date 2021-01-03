FROM amazoncorretto:11

ARG SCALA_VERSION=2.13.4
ARG CC_BRANCH=migrate_to_kafka_2_5

SHELL ["/bin/sh", "-e", "-u", "-x", "-c"]

RUN curl -L "https://downloads.lightbend.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.rpm" \
        --output "/tmp/scala-${SCALA_VERSION}.rpm" \
    && rpm -i "/tmp/scala-${SCALA_VERSION}.rpm"\
    && rm "/tmp/scala-${SCALA_VERSION}.rpm"

RUN yum install -y git \
    && git clone --branch "${CC_BRANCH}" https://github.com/linkedin/cruise-control.git /tmp/cruise-control \
    && cd /tmp/cruise-control \
    && ./gradlew jar \
    && ./gradlew jar copyDependantLibs \
    && mkdir -p /tmp/ccout \
    && CC_JAR="$(find /tmp/cruise-control/cruise-control/build/libs/ -maxdepth 1 -type f -name 'cruise-control-*.jar')" \
    && CC_METRICS_JAR="$(find /tmp/cruise-control/cruise-control/build/dependant-libs/ -maxdepth 1 -type f -name 'cruise-control-metrics-reporter-*.jar')" \
    && cp -a "${CC_JAR}" /tmp/ccout/ \
    && cp -a "${CC_METRICS_JAR}" /tmp/ccout/ \
    && ln -s "$(basename ${CC_JAR})" /tmp/ccout/cruise-control.jar \
    && ln -s "$(basename ${CC_METRICS_JAR})" /tmp/ccout/cruise-control-metrics-reporter.jar

FROM yvlasenko/corretto

COPY --from=0 /tmp/ccout/ /opt/cruise-control/
