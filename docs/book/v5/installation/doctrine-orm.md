# Doctrine ORM

## Setup database

Make sure you fill out the database credentials in `config/autoload/local.php` under `$databases['default']`.

Create a new MySQL database and set its collation to `utf8mb4_general_ci`.

## Running migrations

Running the migrations is done with this command

```shell
php vendor/bin/doctrine-migrations migrate
```

Note: if you have already run the phinx migrations, you may get this message

```shell
WARNING! You have x previously executed migrations in the database that are not registered migrations.
  {migration list}
Are you sure you wish to continue? (y/n)
```

After submitting `y`, you will get this confirmation message.

```shell
WARNING! You are about to execute a database migration that could result in schema changes and data loss. Are you sure you wish to continue? (y/n)
```

Again, submit `y` to run all the migrations in chronological order. Each migration will be logged in the `migrations` table to prevent running the same migration more than once, which is often not desirable.

## Creating migrations

To generate a new migration file, use this command:

```shell
php vendor/bin/doctrine-migrations migrations:generate
```

It creates a PHP file like this one `/data/doctrine/migrations/Version20220606131835.php` that can then be edited in the IDE. You can add new queries to be executed when the migration is run (in `public function up`) and optionally queries that undo those changes (in `public function down`).

Here is an example you can add in `public function up`

```shell
$this->addSql('ALTER TABLE users ADD test VARCHAR(255) NOT NULL');
```

and its opposite in `public function down`

```shell
$this->addSql('ALTER TABLE users DROP test');
```

## Executing fixtures

**Fixtures are used to seed the database with initial values and should only be executed ONCE, after migrating the database.**

Seeding the database is done with the help of our custom package ``dotkernel/dot-data-fixtures`` built on top of doctrine/data-fixtures. See below on how to use our CLI command for listing and executing Doctrine data fixtures.

An example of a fixtures class is ``data/doctrine/fixtures/RoleLoader.php``

To list all the available fixtures, by order of execution, run:

```shell
php bin/doctrine fixtures:list
```

To execute all fixtures, run:

```shell
php bin/doctrine fixtures:execute
```

To execute a specific fixtures, run:

```shell
php bin/doctrine fixtures:execute --class=RoleLoader
```

Fixtures can and should be ordered to ensure database consistency, more on ordering fixtures can be found here :
https://www.doctrine-project.org/projects/doctrine-data-fixtures/en/latest/how-to/fixture-ordering.html#fixture-ordering
