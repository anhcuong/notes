# SQL Query Optimization

### IN vs OR

``` sql
WHERE foo IN ('a', 'b', 'c')
WHERE foo = 'a' OR foo = 'b' OR foo = 'c'
```

Readability: IN

Speed: IN

> PostgreSQL executes the query with the IN operator much faster than the same query that uses a list of OR operators. (http://www.postgresqltutorial.com/postgresql-in/)

> MYSQL (http://stackoverflow.com/questions/782915/mysql-or-vs-in-performance)

### BETWEEN vs AND

``` sql
SELECT * FROM table WHERE someColumn BETWEEN 1 AND 100
SELECT * FROM table WHERE someColumn >= 1 AND someColumn <= 100
```

Readability: BETWEEN

Speed: Tie since BETWEEN query gonna be translated into AND query.

> No benefit, just a syntax sugar. By using the BETWEEN version, you can avoid function reevaluation in some cases. (http://stackoverflow.com/questions/2692593/between-operator-vs-and-is-there-a-performance-difference)

### BETWEEN vs IN

``` sql
WHERE `id` BETWEEN n AND nk;
WHERE `id` IN (n, ... nk); 
```

Readability: BETWEEN if the range is large and vice-versa.

Speed: BETWEEN if the range is large or scanning column is not indexed.

Depend on the indexed column, some situations IN might outperform BETWEEN in term of speed.

> This is performance comparision between unique scan (IN) and range scan (BETWEEN)