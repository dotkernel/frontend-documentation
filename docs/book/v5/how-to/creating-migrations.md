# Creating migrations

## Summary

This page generates a new Doctrine migration file and shows how to write its `up` and `down` methods.

## Details

Migrations are used to create and/or edit the database structure.
To generate a new migration file, use this command:

```shell
php vendor/bin/doctrine-migrations migrations:generate
```

It creates a PHP file like this one `/data/doctrine/migrations/Version20220606131835.php` that can then be edited in the IDE.
You can add new queries in:

- `public function up` - these are executed when the migration is run.
- `public function down` - these are optional queries that undo the above changes.

## Example

This example creates a new column named `test`.
Add this in `public function up`:

```php
$this->addSql('ALTER TABLE user ADD test VARCHAR(255) NOT NULL');
```

And its opposite in `public function down`:

```php
$this->addSql('ALTER TABLE user DROP test');
```

## FAQ

### **Q: Where are new migrations saved?**

A: In `data/doctrine/migrations`, in the `Frontend\Migrations` namespace, as set in `config/migrations.php`.

### **Q: How do I undo the last migration?**

A: Run `php vendor/bin/doctrine-migrations migrate prev`, which runs the `down` method of the latest executed migration.

### **Q: Can Doctrine write the migration for me?**

A: Yes. After changing your entities, run `php vendor/bin/doctrine-migrations diff`, which generates a migration from the difference between the entity mapping and the database.
Review the generated SQL before you run it.

### **Q: Is a failed migration rolled back?**

A: `config/migrations.php` enables `transactional` and `all_or_nothing`.
MySQL and MariaDB commit schema changes implicitly, so a failed `ALTER TABLE` may still leave earlier statements applied.
