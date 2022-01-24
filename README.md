Данный репозиторий содержит файлы, которые повторяются от проекта к проекту и могут быть шаблонизированы.

Для этого в pom нужно добавить:

```
<properties>
    <server.port>8022</server.port>
    <dockerfile.base.service.tag>f26fcc19d1941ab74f1c72dd8a408be17a769333</dockerfile.base.service.tag>
    <damsel.version>1.151-4018c41</damsel.version>
    <shared.resources.version>1.0.0</shared.resources.version>
...

<dependency>
    <groupId>dev.vality</groupId>
    <artifactId>shared-resources</artifactId>
    <version>${shared.resources.version}</version>
</dependency>

...    

<resources>
    <resource>
        <directory>${project.build.directory}/maven-shared-archive-resources</directory>
        <targetPath>${project.build.directory}</targetPath>
        <includes>
            <include>Dockerfile</include>
        </includes>
        <filtering>true</filtering>
    </resource>
    <resource>
        <directory>${project.build.directory}/maven-shared-archive-resources</directory>
        <filtering>true</filtering>
        <excludes>
            <exclude>Dockerfile</exclude>
        </excludes>
    </resource>
    <resource>
        <directory>src/main/resources</directory>
        <filtering>true</filtering>
    </resource>
</resources>

<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-remote-resources-plugin</artifactId>
    <version>1.7.0</version>
    <dependencies>
        <dependency>
            <groupId>org.apache.maven.shared</groupId>
            <artifactId>maven-filtering</artifactId>
            <version>3.2.0</version>
        </dependency>
    </dependencies>
    <configuration>
        <resourceBundles>
            <resourceBundle>dev.vality:shared-resources:${shared.resources.version}</resourceBundle>
        </resourceBundles>
        <attachToMain>false</attachToMain>
        <attachToTest>false</attachToTest>
    </configuration>
    <executions>
        <execution>
            <goals>
                <goal>process</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

после этого можно удалить локальные файлы: 
1. Dockerfile
1. git.properties
1. logback-spring.xml
