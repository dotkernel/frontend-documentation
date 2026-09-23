# Server Requirements

## Summary

This page lists what a server needs to run Dotkernel Frontend: a web server (Apache or Nginx), PHP with its required settings and extensions, and a MariaDB or MySQL database.
It also lists the extensions that are recommended for common tasks and for running the tests.

## Details

For production, we highly recommend a *nix based system.

## Webserver

### Apache >= 2.2

* mod_rewrite
* .htaccess support `(AllowOverride All)`

> The repository includes a default `.htaccess` file in the `public` folder.

### Nginx

You need to convert the provided Apache related `.htaccess` file into Nginx configuration instructions.

## PHP 8.2 or 8.3

Both mod_php and FCGI (FPM) are supported.

## Required Settings and Modules & Extensions

* memory_limit >= 128M
* upload_max_filesize and post_max_size >= 100M (depending on your data)
* curl (used by the contact form's reCAPTCHA verification)
* gettext
* intl (required by `laminas/laminas-i18n`)
* json
* mbstring
* CLI SAPI (for Cron Jobs)
* Composer (added to $PATH)

## RDBMS

* Tested with MariaDB 10.11 LTS and MariaDB 11.4 LTS
* Tested with MySQL 8.4 LTS

> For MySQL 8.4 LTS be sure you have the below line in my.cnf

```text
mysql_native_password=ON
```

## Recommended extensions

* opcache
* pdo_mysql (the driver configured in `config/autoload/local.php.dist` for MySQL or MariaDB)
* dom - if working with markup files structure (html, xml etc.)
* simplexml - working with xml files
* gd, exif - if working with images
* zlib, zip, bz2 - if compressing files
* sqlite3 - for tests

## FAQ

### **Q: Which PHP versions are supported?**

A: PHP 8.2 and 8.3; `composer.json` requires `~8.2.0 || ~8.3.0`.

### **Q: Can I use Nginx instead of Apache?**

A: Yes.
Convert the rewrite rules in `public/.htaccess` into Nginx configuration so that every request for a file that does not exist is sent to `public/index.php`.

### **Q: Can I use PostgreSQL?**

A: Not out of the box.
`config/autoload/local.php.dist` configures the `pdo_mysql` driver, and the shipped migration uses MySQL/MariaDB syntax such as `ENUM` columns.

### **Q: Why is `sqlite3` needed for tests?**

A: The test configuration in `config/autoload/local.test.php.dist` connects Doctrine to an in-memory SQLite database (`sqlite3:///:memory:`).
