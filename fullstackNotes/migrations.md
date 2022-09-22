## [db-migrate](https://github.com/db-migrate/node-db-migrate#readme)

For each migration we will run the `db migrate create` command. At the first run it will create:
- a `migrations` directory in our project root directory
- an `sqls` directory under migrations
- migrations will run in order of their creation, so have to be created in logical order (to run without error category table migration has to be run before product table migration)
- in case categories are introduced later and the order of migration has to be changed one can change the date in the name of the migration files (if the up and down migration file names are, their names have to be updated *within* the automatically generated `.js` migration file)

