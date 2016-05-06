# SQL Query Optimization

### IN vs OR

``` sql
WHERE foo IN ('a', 'b', 'c')
WHERE foo = 'a' OR foo = 'b' OR foo = 'c'
```

Readability: IN
Speed: IN

> PostgreSQL executes the query with the IN operator much faster than the same query that uses a list of OR operators. (http://www.postgresqltutorial.com/postgresql-in/)

### 