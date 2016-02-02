FROM hypriot/rpi-java

ENV http_proxy "http://10.0.4.2:3128"
ENV https_proxy "https://10.0.4.2:3128"

RUN apt-get update -qq && apt-get install -y maven && apt-get clean

WORKDIR /code

ADD pom.xml /code/pom.xml
ADD settings.xml /root/.m2/settings.xml
RUN ["mvn", "dependency:resolve"]
RUN ["mvn", "verify"]

# Adding source, compile and package into a fat jar
ADD src /code/src
RUN ["mvn", "package"]

CMD ["java", "-jar", "target/worker-jar-with-dependencies.jar"]
