FROM openjdk:8-jdk-alpine

ENV DOCKERIZE_VERSION v0.3.0

RUN apk add --no-cache curl wget git openssh

RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

ADD target/config-*.jar app.jar

ENV JAVA_OPTS=""

ENTRYPOINT dockerize -wait tcp://discovery:8080 -timeout ${TIMEOUT:-240s} && exec java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom -jar /app.jar
