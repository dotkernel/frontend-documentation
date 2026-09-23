# Frequently Asked Questions

## Summary

This page solves the most common first-run errors, which come from the web server not being able to write to the `data`, `public/uploads` and `log` folders.

## How do I fix common permission issues?

If running your project you encounter some permission issues, follow the below steps.

### Errors

> PHP Fatal error:  Uncaught InvalidArgumentException: The directory "/var/www/_example.local_/html/data" is not writable...

> PHP Fatal error:  Uncaught InvalidArgumentException: The directory "/var/www/_example.local_/html/data/cache" is not writable...

> PHP Fatal error:  Uncaught InvalidArgumentException: The directory "/var/www/_example.local_/html/data/cache/doctrine" is not writable...

**Fix:**

```shell
chmod -R 777 data
```

### Error

> PHP Fatal error:  Uncaught InvalidArgumentException: The directory "/var/www/_example.local_/html/public/uploads" is not writable...

**Fix:**

```shell
chmod -R 777 public/uploads
```

### Error

> PHP Fatal error:  Uncaught ErrorException: fopen(/var/www/_example.local_/config/autoload/../../log/error-log-_yyyy-mm-dd.log_): Failed to open stream: Permission denied...

**Fix:**

```shell
chmod -R 777 log
```

## FAQ

### **Q: Is `chmod -R 777` safe on a production server?**

A: No. It lets every user on the server write to these folders.
In production, give ownership of `data`, `public/uploads` and `log` to the web server user and grant write access only to that user.

### **Q: Where are the error logs?**

A: In `log/error-log-{Y}-{m}-{d}.log`, one JSON-formatted file per day, as set in `config/autoload/error-handling.global.php`.

### **Q: The application reports missing services after a configuration change. What should I do?**

A: Remove the cached configuration with `php bin/clear-config-cache.php` (or `composer clear-config-cache`).
While `data/cache/config-cache.php` exists, it is loaded instead of your configuration files.
