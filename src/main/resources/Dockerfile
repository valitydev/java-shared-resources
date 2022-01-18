# @dockerfile.Template@
FROM @dockerfile.registry@/openjdk/15-jdk-slim:@dockerfile.base.service.tag@
MAINTAINER @project.maintainer@

COPY @artifactId@-@version@.jar /opt/@artifactId@/@artifactId@.jar

CMD ["java", "-Xmx256m", "-jar","/opt/@artifactId@/@artifactId@.jar"]

EXPOSE @exposed.ports@

LABEL dev.vality.@artifactId@.parent=service-java \
    dev.vality.@artifactId@.parent_tag=@dockerfile.base.service.tag@ \
    dev.vality.@artifactId@.commit_id=@git.commit.id@ \
    dev.vality.@artifactId@.branch=@git.branch@

WORKDIR /opt/@artifactId@
