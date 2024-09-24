# Doctrine ORM

This step saves the database connection credentials in a Frontend configuration file.
We do not cover the creation steps of the database itself.

## Setup database

Create a new MySQL database and set its collation to `utf8mb4_general_ci`.

Fill out the database credentials in `config/autoload/local.php` under `$databases['default']`.
Below is the item you need to focus on.

> `my_database`, `my_user`, `my_password` are provided only as an example.

```php
$databases = [
    'default' => [
        'host'     => 'localhost',
        'dbname'   => 'my_database',
        'user'     => 'my_user',
        'password' => 'my_password',
        'port'     => 3306,
        'driver'   => 'pdo_mysql',
        'charset'  => 'utf8mb4',
        'collate'  => 'utf8mb4_general_ci',
    ],
    // you can add more database connections into this array
];
```

## Migrations

Running the migrations is done with this command

```shell
php vendor/bin/doctrine-migrations migrate
```

Note: If you have already run the migrations, you may get this message.
You should double-check to make sure the new migrations are ok to run.

```shell
WARNING! You have x previously executed migrations in the database that are not registered migrations.
  {migration list}
Are you sure you wish to continue? (y/n)
```

When using an empty database, you will get this confirmation message instead.

```shell
WARNING! You are about to execute a database migration that could result in schema changes and data loss. Are you sure you wish to continue? (y/n)
```

Again, submit `y` to run all the migrations in chronological order.
Each migration will be logged in the `migrations` table to prevent running the same migration more than once, which is often not desirable.

If everything ran correctly, you will get this confirmation.

```shell
[OK] Successfully migrated to version: Frontend\Migrations\Version20240806123413
```

> The migration name `Version20240806123413` may differ in future Frontend updates.

## Fixtures

Run this command to populate the `user_role` table with the default values:

```shell
php bin/doctrine fixtures:execute
```

You should see our galloping horse in the command line.

```shell
Executing Frontend\Fixtures\RoleLoader
Fixtures have been loaded.
                .''
      ._.-.___.' (`\
     //(        ( `'
    '/ )\ ).__. )
    ' <' `\ ._/'\
       `   \     \
```
