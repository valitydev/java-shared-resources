Данный репозиторий содержит файлы которые посторяютс яот проекта к проекту и могут быть шаблонизированы.

Для этого pom нужно добавить:

```
<properties>
    <project.maintainer>Inal Arsanukaev &lt;i.arsanukaev@rbkmoney.com&gt;</project.maintainer>
    <server.port>8022</server.port>
    <dockerfile.base.service.tag>f26fcc19d1941ab74f1c72dd8a408be17a769333</dockerfile.base.service.tag>
    <damsel.version>1.151-4018c41</damsel.version>
    <shared.resources.version>0.2.1</shared.resources.version>
...

<dependency>
    <groupId>com.rbkmoney</groupId>
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
    <version>1.5</version>
    <dependencies>
        <dependency>
            <groupId>org.apache.maven.shared</groupId>
            <artifactId>maven-filtering</artifactId>
            <version>1.3</version>
        </dependency>
    </dependencies>
    <configuration>
        <resourceBundles>
            <resourceBundle>com.rbkmoney:shared-resources:${shared.resources.version}</resourceBundle>
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