# Maven plugin

Liquigraph provides a Maven plugin.
This plugin is a good fit for:

 - standalone executions of Liquigraph in environments where JVM tooling is already in place (like CI/CD pipelines e.g.). You might want to have a look at the [Liquigraph CLI](./cli.md) otherwise
 - the automation of migrations before some other Maven plugin executes (such as [Maven Failsafe Plugin](https://maven.apache.org/surefire/maven-failsafe-plugin/) for integration tests)

## Prerequisites

Make sure a JDK is set up on the machine running the Maven build.

For Neo4j 3.x, the minimal JDK version is 8.

For Neo4j 4.x, the minimal JDK version is 11.

You will also need to install a recent version of [Apache Maven](https://maven.apache.org/).

As a simple sanity check, `javac --version`, `java --version` and `mvn --version` should display the same JDK version.

{!includes/_quickstart_beginning.md!}

## A minimal POM file

For simplicity's sake, a standalone Maven build will be assumed.
If that's not the case, simply copy the relevant sections of the following file:

=== "Liquigraph 4.x"

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>
    
        <groupId>com.example</groupId>
        <artifactId>liquigraph-maven-example</artifactId>
        <version>0.0.1-SNAPSHOT</version>
        <packaging>jar</packaging>
    
        <name>liquigraph-maven-example</name>
    
        <properties>
            <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
            <project.reporting.outputEncoding>${project.build.sourceEncoding}</project.reporting.outputEncoding>
            <maven.compiler.release>11</maven.compiler.release>
        </properties>
    
        <build>
            <plugins>
                <plugin>
                    <groupId>org.liquigraph</groupId>
                    <artifactId>liquigraph-maven-plugin</artifactId>
                    <version>{{ versions.latest_4x }}</version>
                    <configuration>
                        <changelog>changelog.xml</changelog>
                        <jdbcUri>jdbc:neo4j:bolt://localhost</jdbcUri>
                        <username>neo4j</username>
                        <password>changeme</password>
                    </configuration>
                </plugin>
            </plugins>
        </build>
    </project>
    ```

=== "Liquigraph 3.x"

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>
    
        <groupId>com.example</groupId>
        <artifactId>liquigraph-maven-example</artifactId>
        <version>0.0.1-SNAPSHOT</version>
        <packaging>jar</packaging>
    
        <name>liquigraph-maven-example</name>
    
        <properties>
            <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
            <project.reporting.outputEncoding>${project.build.sourceEncoding}</project.reporting.outputEncoding>
            <maven.compiler.source>8</maven.compiler.source>
            <maven.compiler.target>${maven.compiler.source}</maven.compiler.target>
        </properties>
    
        <build>
            <plugins>
                <plugin>
                    <groupId>org.liquigraph</groupId>
                    <artifactId>liquigraph-maven-plugin</artifactId>
                    <version>{{ versions.latest_3x }}</version>
                    <configuration>
                        <changelog>changelog.xml</changelog>
                        <jdbcUri>jdbc:neo4j:bolt://localhost</jdbcUri>
                        <username>neo4j</username>
                        <password>changeme</password>
                    </configuration>
                </plugin>
            </plugins>
        </build>
    </project>
    ```

!!! info
    Please refer to the [download section](../download.md#jvm) to learn how to retrieve a Liquigraph [SNAPSHOT](https://maven.apache.org/guides/getting-started/index.html#What_is_a_SNAPSHOT_version) version.

!!! note
    `CHANGELOG_FILE` should be stored in `src/main/resources/changelog.xml` for the example to work.

The following executions assumes that the current directory is the folder where `pom.xml`.

## Dry run

{!includes/_dry-run-beginning.md!}

Since the configuration is defined in the POM file, the execution is simply as follows:

```shell
mvn compile liquigraph:dry-run
```

This should result in a successful execution with a file named `output.cypher` in the generated `target` folder:

```shell
less target/output.cypher
//Liquigraph changeset[author: florent-biville, id: sentence-initialization]
//Liquigraph changeset[executionContexts: none declared]
CREATE (n:Sentence {text:"Hello monde!"}) RETURN n
//Liquigraph changeset[author: florent-biville, id: sentence-correction]
//Liquigraph changeset[executionContexts: none declared]
MATCH (n:Sentence {text:"Hello monde!"}) SET n.text="Hello world!" RETURN n
```

!!! note
    - Contrary to Liquibase, Liquigraph only includes the queries of the matching change sets.
    Cypher queries executed for Liquigraph internal purposes are not included.
    - Printing to the standard output is also currently unsupported.

## Run

Once the dry run is successful, you can finally execute the migrations.

The invocation is very similar, only the plugin target goal changes:

```shell
mvn compile liquigraph:run
```

{!includes/_quickstart_end.md!}

{!includes/_abbreviations.md!}
