# Fixtures

## Summary

This page lists and runs the Doctrine data fixtures that seed the database, either all at once or one class at a time.

## Details

> Fixtures are used to seed the database with initial values and should only be executed ONCE each, after migrating the database.

Seeding the database is done with the help of our custom package `dotkernel/dot-data-fixtures` built on top of `doctrine/data-fixtures`.
See below on how to use our CLI command for listing and executing Doctrine data fixtures.

## Working with fixtures

You can find an example of a fixtures class in `data/doctrine/fixtures/RoleLoader.php`.

To list all the available fixtures by order of execution run:

```shell
php bin/doctrine fixtures:list
```

To execute all fixtures run:

```shell
php bin/doctrine fixtures:execute
```

To execute a specific fixture, use its class name, like in this example:

```shell
php bin/doctrine fixtures:execute --class=RoleLoader
```

Fixtures can and should be ordered to ensure database consistency.
More on ordering fixtures can be found here :
https://www.doctrine-project.org/projects/doctrine-data-fixtures/en/latest/how-to/fixture-ordering.html#fixture-ordering

## FAQ

### **Q: Where do fixture classes go?**

A: In `data/doctrine/fixtures`, the path set by `doctrine` => `fixtures` in `config/autoload/doctrine.global.php`.

### **Q: What value does `--class` take?**

A: The class's short name, which must match its file name without `.php`, for example `--class=RoleLoader` for `RoleLoader.php`.

### **Q: Why should each fixture run only once?**

A: `fixtures:execute` appends to the existing data instead of purging it.
Running a fixture twice inserts its rows again, which fails on unique columns such as `user_role.name`.
