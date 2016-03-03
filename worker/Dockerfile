FROM java:7

ENV http_proxy=http://proxy.houston.hpecorp.net:8080/
ENV https_proxy=http://proxy.houston.hpecorp.net:8080/
ENV no_proxy=localhost,127.0.0.1,hpecorp.net

RUN apt-get update -qq && apt-get install -y maven && apt-get clean

WORKDIR /code

ADD pom.xml /code/pom.xml
RUN ["mvn", "dependency:resolve"]
RUN ["mvn", "verify"]

# Adding source, compile and package into a fat jar
ADD src /code/src
RUN ["mvn", "package"]

CMD ["/usr/lib/jvm/java-7-openjdk-amd64/bin/java", "-jar", "target/worker-jar-with-dependencies.jar"]
