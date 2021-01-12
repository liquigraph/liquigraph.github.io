## Basic concepts

Liquigraph requires a single entry point, also known as a **change log** file.
This file can include other **change log** files and/or define **change set**s.

Every **change set** is executed in a separate transaction.
They define at least 1 [Cypher](https://neo4j.com/developer/cypher/) query.
These Cypher queries define the data (or [indices/constraints](https://neo4j.com/docs/getting-started/current/cypher-intro/schema/)) that will be created, modified or deleted from the target database.

!!! caution
    Neo4j disallows mixing index/constraint with regular "data" operations within the same transaction. 
    Such a transaction will always fail.
    As a consequence, index/constraint operations must be defined in separate Liquigraph change sets.

Change sets are uniquely identified by their ID and author name.
By default, they also are:

 - incremental: they are allowed to run only once.
 - immutable: their queries are not allowed to change.

Learn how to change these defaults, and more, in the [reference documentation](../reference.md).

## First migrations

### Change log creation

Save the following change log file:

```xml linenums="1"
<?xml version="1.0" encoding="UTF-8"?>
<changelog xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:noNamespaceSchemaLocation="https://www.liquigraph.org/schema/1.0/liquigraph.xsd">
    <changeset id="sentence-initialization" author="florent-biville">
        <query>CREATE (n:Sentence {text:"Hello monde!"}) RETURN n</query>
    </changeset>
    <changeset id="sentence-correction" author="florent-biville">
        <query>MATCH (n:Sentence {text:"Hello monde!"}) SET n.text="Hello world!" RETURN n</query>
    </changeset>
</changelog>
```

The change log defines two change sets, which are executed in order, in separate transactions:

 1. The first change set defines a single query, which creates a node, with a `Sentence` label and a simple textual property called `text`.
 1. The second change set defines a single Cypher query as well, which finds the node pattern and updates the `text` property accordingly.

If the Cypher syntax looks unfamiliar, feel free to follow [this official tutorial](https://neo4j.com/developer/cypher/guide-cypher-basics/).

!!! info
    The location of this file will be called `CHANGELOG_FILE` throughout the rest of the tutorial.

!!! note
    Contrary to Liquibase, Liquigraph only supports XML for defining change logs.

### Connection URI

To keep things simple, we will assume a standalone Neo4j server is running on your machine, 
via [Neo4j Desktop](https://neo4j.com/download/) or [Docker](https://hub.docker.com/_/neo4j) for instance.

The connection URI will be `jdbc:neo4j:bolt://localhost`, username `neo4j` and the password `changeme`.

Depending on Neo4j versions, Neo4j server typology and Liquigraph client, connection URI can vary greatly.
The configuration is covered in much greater details in the [reference documentation](../reference.md).
