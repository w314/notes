# [psql ENUM data type](https://www.postgresql.org/docs/14/datatype-enum.html)

```sql
CREATE TYPE usertype AS ENUM ('admin', 'regular');
CREATE TABLE users (
    username VARCHAR(100),
    firstname VARCHAR(100), 
    lastname VARCHAR(100), 
    password_digest VARCHAR, 
    id SERIAL PRIMARY KEY
    user_type usertype
);
```

Enum types are stored in `pg_enum` table