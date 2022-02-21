# @dockerfile.Template@
FROM openjdk:15-jdk-slim

RUN useradd -s /bin/false -U -u 20000 vality

COPY --chown=vality:vality @artifactId@-@version@.jar /opt/@artifactId@/@artifactId@.jar

USER vality:vality

CMD ["java", "-Xmx256m", "-jar","/opt/@artifactId@/@artifactId@.jar"]

# hadolint ignore=DL3006,DL3011
EXPOSE @exposed.ports@

WORKDIR /opt/@artifactId@
