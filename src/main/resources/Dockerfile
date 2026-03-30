FROM ghcr.io/valitydev/temurin-jemalloc:sha-402a042

RUN useradd -s /bin/false -U -u 20000 vality

COPY --chown=vality:vality maven-shared-archive-resources/opentelemetry-javaagent.jar /opt/${artifactId}/opentelemetry-javaagent.jar
COPY --chown=vality:vality ${artifactId}-${version}.jar /opt/${artifactId}/${artifactId}.jar

USER vality:vality

CMD ["java", "-javaagent:/opt/${artifactId}/opentelemetry-javaagent.jar", "-jar","/opt/${artifactId}/${artifactId}.jar"]

EXPOSE ${exposed.ports}

WORKDIR /opt/${artifactId}
