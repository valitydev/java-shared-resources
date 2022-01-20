# @dockerfile.Template@
FROM openjdk:15-jdk-slim

COPY @artifactId@-@version@.jar /opt/@artifactId@/@artifactId@.jar

CMD ["java", "-Xmx256m", "-jar","/opt/@artifactId@/@artifactId@.jar"]

EXPOSE @exposed.ports@

WORKDIR /opt/@artifactId@
