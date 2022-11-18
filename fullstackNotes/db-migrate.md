## [db-migrate](https://github.com/db-migrate/node-db-migrate#readme)
Migrations will set up our database schema 

For each migration we will run the `db migrate create` command. At the first run it will create:
- a `migrations` directory in our project root directory
- an `sqls` directory under migrations
- migrations will run in order of their creation, so have to be created in logical order (to run without error category table migration has to be run before product table migration)
- in case categories are introduced later and the order of migration has to be changed one can change the date in the name of the migration files (if the up and down migration file names are, their names have to be updated *within* the automatically generated `.js` migration file)


At each run it will create:
- a generated `.js` file that should not be modified under `migrations`
- two `.sql` files under the `sqls` directory with for the up and down migrations
  - into the `up` migration file you will enter the `sql` command that  will setup your table
  - the `down` migration file will hold the `sql` command to the migration you just did in the `up` migration
  
>IMPORTANT: when creating tables DO NOT use camelCase, the result from the database comes back all lower case even if the migration table was set up with camelCase and than the property names of the User from the database doesn't match the property names of the User type.
For each migration we will run the `db migrate create` command. At the first run it will create:
