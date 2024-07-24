# Development mode

Run this command to enable dev mode by turning debug flag to `true` and turning configuration caching to `off`. It will also make sure that any existing config cache is cleared.

```shell
composer development-enable
```

- If not already done, remove the `.dist` extension from `config/autoload/development.global.php.dist`.

# Using DebugBar

DotKernel comes with its own DebugBar already installed and configured. It is enabled when you clone the config file `config/autoload/debugbar.local.php.dist` as `config/autoload/debugbar.local.php`. You can disable the tool by going into its config file `config/autoload/debugbar.local.php` and changing

```
'enabled' => true
```

to

```
'enabled' => false
```
