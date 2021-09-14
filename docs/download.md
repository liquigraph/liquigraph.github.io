# Download Liquigraph

## CLI

### For Homebrew users (Mac OS)

Liquigraph is part of the standard recipes of [Homebrew](https://brew.sh/).
You just have to run:

```shell
brew install liquigraph
```

### Regular download (Unix & Windows)

=== "Liquigraph 4.x"
    - [liquigraph-cli.zip](https://search.maven.org/remotecontent?filepath=org/liquigraph/liquigraph-cli/{{ versions.latest_4x }}/liquigraph-cli-{{ versions.latest_4x }}-bin.zip)
    - [liquigraph-cli.tar.gz](https://search.maven.org/remotecontent?filepath=org/liquigraph/liquigraph-cli/{{ versions.latest_4x }}/liquigraph-cli-{{ versions.latest_4x }}-bin.tar.gz)
    - [liquigraph-cli.tar.bz2](https://search.maven.org/remotecontent?filepath=org/liquigraph/liquigraph-cli/{{ versions.latest_4x }}/liquigraph-cli-{{ versions.latest_4x }}-bin.tar.bz2)

=== "Liquigraph 3.x"
    - [liquigraph-cli.zip](https://search.maven.org/remotecontent?filepath=org/liquigraph/liquigraph-cli/{{ versions.latest_3x }}/liquigraph-cli-{{ versions.latest_3x }}-bin.zip)
    - [liquigraph-cli.tar.gz](https://search.maven.org/remotecontent?filepath=org/liquigraph/liquigraph-cli/{{ versions.latest_3x }}/liquigraph-cli-{{ versions.latest_3x }}-bin.tar.gz)
    - [liquigraph-cli.tar.bz2](https://search.maven.org/remotecontent?filepath=org/liquigraph/liquigraph-cli/{{ versions.latest_3x }}/liquigraph-cli-{{ versions.latest_3x }}-bin.tar.bz2)

These archives contain two scripts:

 - `liquigraph-cli.sh` for Unix users
 - `liquigraph-cli.bat` for Windows users

## JVM

The following artefacts are available through Maven Central.

!!! info
    If you want to try a development version (a.k.a. a [SNAPSHOT](https://maven.apache.org/guides/getting-started/index.html#What_is_a_SNAPSHOT_version) version), you do not need to build from sources.
    You can configure your build with a custom repository:
    ```xml
    <repositories>
      <repository>
          <id>ossrh</id>
          <name>Sonatype Snapshots</name>
          <url>https://oss.sonatype.org/content/repositories/snapshots</url>
          <snapshots>
              <enabled>true</enabled>
          </snapshots>
          <releases>
              <enabled>false</enabled>
          </releases>
      </repository>
    </repositories>
    ```

### Maven plugin

=== "Liquigraph 4.x"

    ```xml
    <plugin>
        <groupId>org.liquigraph</groupId>
        <artifactId>liquigraph-maven-plugin</artifactId>
        <version>{{ versions.latest_4x }}</version>
        <configuration>
            <changelog>changelog.xml</changelog><!-- classpath location -->
            <jdbcUri>jdbc:neo4j:bolt://localhost</jdbcUri>
        </configuration>
        <executions>
            <execution>
              <id>run-migrations</id>
              <goals>
                <goal>dry-run</goal>
                <goal>run</goal>
              </goals>
            </execution>
        </executions>
    </plugin>
    ```

=== "Liquigraph 3.x"

    ```xml
    <plugin>
        <groupId>org.liquigraph</groupId>
        <artifactId>liquigraph-maven-plugin</artifactId>
        <version>{{ versions.latest_3x }}</version>
        <configuration>
            <changelog>changelog.xml</changelog><!-- classpath location -->
            <jdbcUri>jdbc:neo4j:bolt://localhost</jdbcUri>
        </configuration>
        <executions>
            <execution>
              <id>run-migrations</id>
              <goals>
                <goal>dry-run</goal>
                <goal>run</goal>
              </goals>
            </execution>
        </executions>
    </plugin>
    ```

### Spring Boot starter

=== "Liquigraph 4.x"

    ```xml
    <dependency>
        <groupId>org.liquigraph</groupId>
        <artifactId>liquigraph-spring-boot-starter</artifactId>
        <version>{{ versions.latest_4x }}</version>
    </dependency>
    ```

=== "Liquigraph 3.x"

    ```xml
    <dependency>
        <groupId>org.liquigraph</groupId>
        <artifactId>liquigraph-spring-boot-starter</artifactId>
        <version>{{ versions.latest_3x }}</version>
    </dependency>
    ```

### Liquigraph Core

!!! caution
    Liquigraph is better used through the CLI, Maven plugin or Spring Boot starter.
    If you want to build an integration, [please file an issue](https://github.com/liquibase/liquigraph/issues/new) and let's discuss!

=== "Liquigraph 4.x"

    ```xml
    <dependency>
        <groupId>org.liquigraph</groupId>
        <artifactId>liquigraph-core</artifactId>
        <version>{{ versions.latest_4x }}</version>
    </dependency>
    ```

=== "Liquigraph 3.x"

    ```xml
    <dependency>
        <groupId>org.liquigraph</groupId>
        <artifactId>liquigraph-core</artifactId>
        <version>{{ versions.latest_3x }}</version>
    </dependency>
    ```

{!includes/_abbreviations.md!}


