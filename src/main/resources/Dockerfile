# @dockerfile.Template@
FROM @dockerfile.registry@/openjdk/15-jdk-slim
MAINTAINER @project.maintainer@

COPY @artifactId@-@version@.jar /opt/@artifactId@/@artifactId@.jar

CMD ["java", "-Xmx256m", "-jar","/opt/@artifactId@/@artifactId@.jar"]

EXPOSE @exposed.ports@

WORKDIR /opt/@artifactId@
