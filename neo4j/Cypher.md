
[[Neo4j]] Learning academy: [cypher-fundamentals](https://graphacademy.neo4j.com/courses/cypher-fundamentals)

## Cypher pattern

Nodes with relationship to other nodes

```
( ) --> ( )
```

Find all nodes that have a relationship to `Movie` nodes

```
( ) --> ( :Movie )
```

### Searching

Find `Person` nodes that have the `ACTED_IN` relationship to `Movie` nodes

```
( :Person)-[:ACTED_IN]->( :Movie)
```

![[person-movie.png]]


Find the names of anybody born after 1960 that acted in the movie "The Matrix".

```
MATCH (a:Person)-[:ACTED_IN]->(m:Movie)
WHERE a.born > 1960 AND toLower(m.title) = "the matrix"
RETURN a.name, a.born
```

### Creating

Nodes or relationships can be created using `CREATE` or `MERGE`. When using `MERGE`, if the node or relationship already exists (e.g. with the same label and primary key) then it won't be re-created.

Creating a movie and person. The node must have a label (e.g. `Person`) and a primary key property (e.g. `name`).

```
MERGE (p:Person {name: 'Michael Caine'})
MERGE (m:Movie {title: 'The Dark Knight'})
RETURN p, m
```


We can create an `ACTED_IN` relationship between these two nodes:

```
MATCH (p:Person {name: 'Michael Caine'})
MATCH (m:Movie {title: 'The Dark Knight'})
MERGE (p)-[:ACTED_IN]->(m)
RETURN p, m
```


You can also set properties on the relationship.

```
MERGE (p:Person {name: 'Michael Caine'})
MERGE (m:Movie {title: 'Batman Begins'})
MERGE (p)-[:ACTED_IN {roles: ['Alfred Penny']}]->(m)
RETURN p,m
```

### Updating

Additional properties can be added or updated using `SET`

```
MATCH (p:Person)-[r:ACTED_IN]->(m:Movie)
WHERE p.name = 'Michael Caine' AND m.title = 'The Dark Knight'
SET r.roles = ['Alfred Penny']
RETURN p, r, m
```
**NOTE:** `roles` is set as an array since an actor can have multiple roles in a movie.

You can also remove properties:

```
MATCH (p:Person)-[r:ACTED_IN]->(m:Movie)
WHERE p.name = 'Michael Caine' AND m.title = 'The Dark Knight'
REMOVE r.roles
RETURN p, r, m
```
You can also remove properties by setting the property to `null`

```
SET r.roles = null
```

Conditional `SET`s allow properties to be set in different conditions:
```
MERGE (m:Movie {title: 'Rocketman'})
ON MATCH SET m.matchedAt = dateTime()
ON CREATE SET m.createdAt = dateTime()
SET m.updatedAt = dateTime()
RETURN m
```

### Deleting

A node without any relationships can be easily deleted:
``
```
MATCH (p:Person)
WHERE p.name = 'Jane Doe'
DELETE p
```

A node with any relationships must be `DETACH`ed first (or any error will be thrown).

```
MATCH (p:Person {name: 'Jane Doe'})
DETACH DELETE p
```


To remove a relationship:
```
MATCH (p:Person {name: 'Jane Doe'})-[r:ACTED_IN]->(m:Movie {title: 'The Matrix'})
DELETE r
RETURN p, m
```

Delete labels:
```
MATCH (p:Person {name: 'Jane Doe'})
REMOVE p:Developer
RETURN p
```


Delete all nodes!

```
MATCH (n) DETACH DELETE n
```

