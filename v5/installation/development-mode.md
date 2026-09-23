# Development mode

## Summary

This page enables development mode, which turns on debugging, turns off configuration caching and clears any existing configuration cache.

## Details

Run this command to enable dev mode by turning debug flag to `true` and turning configuration caching to `off`.
It will also make sure that any existing config cache is cleared.

```shell
composer development-enable
```

You should see this in the command prompt:

```shell
> laminas-development-mode enable
You are now in development mode.
```

The command also creates `config/development.config.php` and `config/autoload/development.local.php` from their `.dist` files, so no manual copy is needed.

You can disable development mode by running:

```shell
composer development-disable
```

You can check if you have development mode enabled by running:

```shell
composer development-status
```

## FAQ

### **Q: What does development mode change?**

A: `config/development.config.php` sets `debug` to `true` and disables the configuration cache.
`config/autoload/development.local.php` registers Whoops as the error response generator, which shows the exception details and stack trace.

### **Q: How do I turn development mode off?**

A: Run `composer development-disable`; `composer development-status` shows the current state.

### **Q: Should development mode be enabled in production?**

A: No.
It exposes exception details through Whoops and disables the configuration cache.
