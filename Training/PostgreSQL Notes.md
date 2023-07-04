
### Schema
Postgres is working with schema which is like "namespace".
If you want to connect to a URL you need to give the right schema:
1. In the terminal
```
[11:07:10] michael-ab | () | /$ psql -h localhost -U postgres
psql (9.2.24)
Type "help" for help.

postgres=# select current_schema();
 current_schema
----------------
 public
(1 row)

```
2. The current schema is public:
```java
private final String url = "jdbc:postgresql://localhost/michael" +
            "?currentSchema=public";
```