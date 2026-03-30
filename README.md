# shared-resources

Данный репозиторий содержит шаблоны ресурсов, используемых в сервисах домена.

## Переопределяемые настройки `logback`

`application.yml`:

```yaml
logback:
  appender: JSON_K8S_CONSOLE # возможные значения: DEFAULT_CONSOLE || COLOR_CONSOLE || JSON_K8S_CONSOLE
```

## Настройка `pom.xml`

Dependency:

```xml
<dependency>
    <groupId>dev.vality</groupId>
    <artifactId>shared-resources</artifactId>
    <version>${shared.resources.version}</version>
</dependency>
```

Resources:

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
            <exclude>opentelemetry-javaagent.jar</exclude>
        </excludes>
    </resource>
    <resource>
        <directory>src/main/resources</directory>
        <filtering>true</filtering>
    </resource>
</resources>
```

Plugin:

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

## Отключение OpenTelemetry Java Agent

Для отключения Java agent используйте один из вариантов:

- Переменная окружения: `OTEL_JAVAAGENT_ENABLED=false`
- JVM-параметр: `-Dotel.javaagent.enabled=false`

Документация:
[Disabling the agent entirely](https://opentelemetry.io/docs/zero-code/java/agent/disable/#disabling-the-agent-entirely)
