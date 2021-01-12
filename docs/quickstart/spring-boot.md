# Spring Boot

Liquigraph provides a [Spring Boot](https://spring.io/projects/spring-boot) starter.

It is a good fit if your Spring Boot application owns (well-identified parts of) the data in Neo4j.

## Prerequisites

Make sure a JDK is set up on the machine running the CLI.

For Neo4j 3.x, the minimal JDK version is 8.

For Neo4j 4.x, the minimal JDK version is 11.

## Download

For this particular example, a simple Spring Boot application with a Maven build is assumed.

!!! info
    You can bootstrap a project in a few clicks with [Spring Initializr](https://start.spring.io/), the ["second best place on the Internet"](https://www.youtube.com/watch?v=YVF08E7Xd_Y).
    You do not need to add any dependencies.

{!includes/_quickstart_beginning.md!}

### Configuration

Add the following dependencies to your POM file:

=== "Liquigraph 4.x"

    ```xml
    <dependency>
        <groupId>org.liquigraph</groupId>
        <artifactId>liquigraph-spring-boot-starter</artifactId>
        <version>4.0.3</version>
    </dependency>
    <dependency>
        <groupId>org.neo4j</groupId>
        <!-- change this to neo4j-jdbc-http for HTTP connections to Neo4j -->
        <artifactId>neo4j-jdbc-bolt</artifactId>
        <version>4.0.1</version>
        <scope>runtime</scope>
    </dependency>
    ```

=== "Liquigraph 3.x"

    ```xml
    <dependency>
        <groupId>org.liquigraph</groupId>
        <artifactId>liquigraph-spring-boot-starter</artifactId>
        <version>3.1.2</version>
    </dependency>
    <dependency>
        <groupId>org.neo4j</groupId>
        <!-- change this to neo4j-jdbc-http for HTTP connections to Neo4j -->
        <artifactId>neo4j-jdbc-bolt</artifactId>
        <version>3.5.2</version>
        <scope>runtime</scope>
    </dependency>
    ```
You also need to configure your application with the Neo4j connection settings required by Liquigraph (in `src/main/resources/application.properties` for instance):

```properties
spring.datasource.url=jdbc:neo4j:bolt://localhost
spring.datasource.driver-class-name=org.neo4j.jdbc.bolt.BoltDriver
spring.datasource.username=neo4j
spring.datasource.password=changeme
```

### Run

!!! caution
    The "dry run" mode is currently not supported by the Spring Boot starter, contrary to the [CLI](./cli.md) and [Maven plugin](./maven.md).

!!! note
    `CHANGELOG_FILE` should be stored in `src/main/resources/db/liquigraph/changelog.xml` for the example to work.

You just need to run:

```shell
mvn spring-boot:run
```

{!includes/_quickstart_end.md!}

{!includes/_abbreviations.md!}
