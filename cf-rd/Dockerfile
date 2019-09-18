FROM ubuntu:18.04

RUN apt-get update && apt-get install -y \
    openjdk-8-jdk-headless \
    maven \
    git

RUN git clone https://github.com/eclipse/californium --branch 2.0.x
RUN git clone https://github.com/pokgak/californium.tools --branch cf-rd-dtls

WORKDIR /californium
RUN mvn install -DskipTests

WORKDIR /californium.tools
RUN mvn -f cf-rd/pom.xml install

EXPOSE 5683/udp
EXPOSE 5684/udp

CMD ["/usr/bin/java", "-jar", "cf-rd/target/cf-rd-2.0.0-SNAPSHOT.jar", "PSK"]