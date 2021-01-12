You can then check the data has been added in Neo4j Browser with the following Cypher query:

```cypher
MATCH (sentence:Sentence) RETURN sentence.text AS text
```

The result should be "Hello world!".

You can re-run the same Liquigraph command several times and observe that the graph remains unchanged.
In other words, the following Cypher query:

```cypher
MATCH (sentence:Sentence) RETURN COUNT(sentence)
```

... should indeed always return 1.

!!! info "Good to know"
    If you ever run a less specific Cypher query such as `MATCH (n) RETURN n`, you will see that more node and relationships
    are returned.
    This is normal: Liquigraph persists the change log history in the same database.
    The change log history graph structure is covered in much more details in the [reference documentation](../reference.md). 
