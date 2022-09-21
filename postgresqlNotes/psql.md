# Set up database

1. Start Postgres is termnal
```bash
psql -U postgres
```
Enter password for postgres user. When `postgres=#` prompt appears:
2. Create user for application
```sql
CREATE USER store_app_user WITH PASSWORD 'storeSecret';
```
3. Create database for application
```sql
CREATE DATABASE store_app_db;
GRANT ALL PRIVILEGES ON DATABASE store_app_db TO store_app_user;
```
4. Test database
Connect to the database:
```bash
\c store_app_db
\dt
```
Outputs: "Did not find any relations."

