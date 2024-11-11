# Development mode

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

- If not already done, remove the `.dist` extension from `config/autoload/development.local.php.dist`.
