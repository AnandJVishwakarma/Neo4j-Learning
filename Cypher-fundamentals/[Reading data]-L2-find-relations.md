# Finding Relationships

- Get list of actor names whose movies were released in 2008 or 2009.

```sh
Match (p:Person)-[:ACTED_IN]->(m:Movie)
Where m.released=2008 OR m.released=2009
Return p,m
```
