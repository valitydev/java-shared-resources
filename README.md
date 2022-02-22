Данный репозиторий содержит шаблоны (используемых в сервисах домена) ресурсов

#Переопределяемые настройки `logback`

`application.yml`
```yaml
spring:
  application:
    name: '@project.name@'
logback:
  appender: JSON_K8S_CONSOLE # возможные значения: DEFAULT_CONSOLE || COLOR_CONSOLE || JSON_K8S_CONSOLE
logging:
  level:
    root: info
    spring-application-root: info
    spring-application-woody: info
  pattern:
    spring-application-json-k8s-console: >-
      {
        "@timestamp": "%date{yyy-MM-dd'T'HH:mm:ss.SSSXXX, UTC}",
        "@severity": "%level",
        "thread_name": "%thread",
        "application": "${spring.application.name}",
        "logger_name": "%logger",
        "method": "%method",
        "line": "%line",
        "message": "%message",
        "customField": "${customField}"
      }
logger:
  name:
    spring-application-root: dev.vality.magista
    spring-application-woody: dev.vality.woody
```

#`pom.xml`
```xml
<dependency>
    <groupId>dev.vality</groupId>
    <artifactId>shared-resources</artifactId>
    <version>${shared.resources.version}</version>
</dependency>
```
```xml
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
```
```xml
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
