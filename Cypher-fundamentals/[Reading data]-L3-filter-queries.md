# Filter queries

- Get list of actor names whose movies were released in 2008 or 2009.

```sh
Match (p:Person)-[:ACTED_IN]->(m:Movie)
Where m.released=2008 OR m.released=2009
Return p,m
```

- Get list of actor names who acted in the movies 'The Matrix'.

```sh
Match (p:Person)-[:ACTED_IN]->(m:Movie)
Where m.title = 'The Matrix'
Return p.name
```
OR
```sh
Match (p)-[:ACTED_IN]->(m)
Where p:Person and m:Movie and m.title = 'The Matrix'
Return p.name
```

- Get list of actor names whose movies were released between 2000 and 2003.

```sh
Match (p:Person)-[:ACTED_IN]->(m:Movie)
Where 2000 <= m.released <= 2003
Return p.name, m.title, m.released
```

- Get details if a particular field exists.

```sh
Match (p:Person)-[:ACTED_IN]->(m:Movie)
Where p.name='Jack Nicholan' and m.tagline is not null
Return m.title, m.tagline
```

- Get details if text starts with.

```sh
Match (p:Person)-[:ACTED_IN]->()
Where p.name start with ='Jack'
Return p.name
```

- Get details if text starts with (case insensitive).

```sh
Match (p:Person)-[:ACTED_IN]->()
Where toLower(p.name) start with ='jack'
Return p.name
```

- Get details of persons who wrote the movie but did not direct the same movie.

```sh
Match (p:Person)-[:WROTE]->(m:Movie)
Where Not exists ( (p)-[:DIRECTED]->(m))
Return p.name, p.title
```

- Get details of persons based on the values in a provided list.

```sh
Match (p:Person)
Where p.born in [1965,1970,1975]
Return p.name, p.born
```

- Get details of persons based on the role.

```sh
Match (p:Person)-[r:ACTED_IN]->(m.Movie)
Where 'Neo' in r.roles and m.title='The Matrix'
Return p.name, r.roles
```


## Exercise:

1. Filtering a value in a list

Suppose you want to retrieve all movies that have a released property value that is 2000, 2002, 2004, 2006, or 2008. Here is an incomplete Cypher example to return the title property values of all movies released in these years. What keyword do you specify in the WHERE clause?

Anwser:
MATCH (m:Movie)
WHERE m.released IN [2000, 2002, 2004, 2006, 2008]
RETURN m.title

2. Finding people born in the seventies.

We want to write a MATCH clause to retrieve all Person nodes for people born in the seventies.
Select the WHERE clauses below that will filter this query properly:

MATCH (a:Person) RETURN a.name, a.born

Answer:

WHERE a.born >= 1970 AND a.born < 1980

OR

WHERE 1970 <= a.born < 1980

OR

WHERE a.born IN [1970,1971,1972,1973,1974,1975,1976,1977,1978,1979]

## Challenge:

- Finding Specific Actors

How many actors in the movie The Matrix were born after 1960?






