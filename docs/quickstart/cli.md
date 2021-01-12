# CLI

Liquigraph provides a CLI. 
It is a good fit for users working on non-JVM applications or with a standalone Neo4j deployment directly.

## Prerequisites

Make sure a JRE is set up on the machine running the CLI.

For Neo4j 3.x, the minimal JRE version is 8.

For Neo4j 4.x, the minimal JRE version is 11.

## CLI download

Please refer to the [download section](../download.md) to download the CLI first.

The rest of the tutorial assumes a Unix OS and will therefore show examples with `liquigraph-cli.sh`.


!!! info
    - Homebrew (Mac OS) users need to replace `liquigraph-cli.sh` with `liquigraph`.
    - Windows users need to replace `liquigraph-cli.sh` with `liquigraph-cli.bat`.

Let's now make sure the CLI runs without any issue:

```shell
./liquigraph-cli.sh --help
Usage: liquigraph [options]
  Options:
  * --changelog, -c
      Master Liquigraph changelog location.
	 Prefix with 'classpath:' if
      location is in classpath
// [...] omitted for brevity
    --help, -h
      Get this help
    --password, -p
      Graph DB password (remote only)
    --username, -u
      Graph DB username (remote only)
    --version, -v
      Show the version
```

{!includes/_quickstart_beginning.md!}

## Dry run

{!includes/_dry-run-beginning.md!}

Besides the connection and change log settings, a temporary directory needs to be specified via the option `--dry-run-output-directory` 
(short version: `-d`).
In dry-run mode, Liquigraph generates a Cypher file into this directory.
The Cypher file contains the queries of the change set that would be executed against the configured Neo4j database.

```shell
./liquigraph.sh --username neo4j \
                --password changeme \
                --graph-db-uri jdbc:neo4j:bolt://localhost \
                --changelog CHANGELOG_FILE \
                --dry-run-output-directory /path/to/directory
```

!!! tip
    - You can leave the password value out, and a secure prompt will appear.
    - You can also read the password from a file with `./liquigraph.sh [...] --password < password.txt`.

This should result in a successful execution with a file named `output.cypher` in `/path/to/directory`:

```shell
less /path/to/directory/output.cypher
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
The CLI invocation remains almost the same, only the dry run directory parameter needs to go away:

```shell
./liquigraph.sh --username neo4j \
                --password changeme \
                --graph-db-uri jdbc:neo4j:bolt://localhost \
                --changelog CHANGELOG_FILE
```

{!includes/_quickstart_end.md!}

{!includes/_abbreviations.md!}
