# Composer Installation of Packages

Composer is required to install DotKernel `frontend`. You can install Composer starting [here](https://getcomposer.org/).

## Install dependencies

```shell
composer install
```

The setup script prompts for some configuration settings, for example the lines below:

```shell
Please select which config file you wish to inject 'Laminas\Diactoros\ConfigProvider' into:
  [0] Do not inject
  [1] config/config.php
  Make your selection (default is 1):
```

Simply select `[0] Do not inject`, because DotKernel includes its own configProvider which already contains the prompted configurations.

If you choose `[1] config/config.php` Laminas's `ConfigProvider` from `session` will be injected.

The next question is:

`Remember this option for other packages of the same type? (y/N)`

Type `y` here, and hit `enter`

## Development mode

If you're installing the project for development, make sure you have development mode enabled, by running:

```shell
composer development-enable
```

You can disable development mode by running:

```shell
composer development-disable
```

You can check if you have development mode enabled by running:

```shell
composer development-status
```
