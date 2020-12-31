FROM yvlasenko/corretto

ARG SCALA_VERSION=2.13.4

SHELL ["/bin/sh", "-e", "-u", "-x", "-c"]

RUN wget "https://downloads.lightbend.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.deb" \
    && dpkg -i "scala-${SCALA_VERSION}.deb" \
    && rm "scala-${SCALA_VERSION}.deb"
