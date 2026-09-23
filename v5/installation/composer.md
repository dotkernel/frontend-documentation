# Composer Installation of Packages

## Summary

This page installs the PHP dependencies with `composer install` and explains how to answer the configuration prompts it shows.

## Details

Composer is required to install Dotkernel Frontend. You can install Composer from the [official site](https://getcomposer.org/).

> First make sure that you have navigated your command prompt to the folder where you copied the files in the previous step.

## Install dependencies

> The installation requires the PHP extension `intl`, which may not be enabled by default.
> If Composer reports `laminas/laminas-i18n ... requires ext-intl * -> the requested PHP extension intl is missing from your system.`, enable `extension=intl` in your `php.ini`.

Run this command in the command prompt.

> Use the **CLI** in order to ensure interactivity for proper configuration.

```shell
composer install
```

You should see this text below, along with a long list of packages to be installed instead of the `[...]`.
In this example there are 158 packages, though the number can change in future updates.
You will find the packages in the `vendor` folder.

```shell
No composer.lock file present. Updating dependencies to latest instead of installing from lock file. See https://getcomposer.org/install for more information.
Loading composer repositories with package information
Updating dependencies
Lock file operations: 158 installs, 0 updates, 0 removals
[...]
Writing lock file
Installing dependencies from lock file (including require-dev)
Package operations: 158 installs, 0 updates, 0 removals
[...]
```

The setup script prompts for some configuration settings, for example the lines below:

```shell
Please select which config file you wish to inject 'Laminas\Diactoros\ConfigProvider' into:
  [0] Do not inject
  [1] config/config.php
  Make your selection (default is 1):
```

Type `0` to select `[0] Do not inject`.

> We choose `0` because Dotkernel includes its own ConfigProvider which already contains the prompted configurations.
> If you choose `[1] config/config.php`, an extra `ConfigProvider` will be injected.

The next question is:

`Remember this option for other packages of the same type? (y/N)`

Type `y` here, and hit `enter` to complete this stage.

After the packages are installed, `bin/composer-post-install-script.php` creates `config/autoload/local.php` (from `local.php.dist`) and `config/autoload/mail.global.php` (from dot-mail's `mail.global.php.dist`) if they are missing.

## Development mode

Development mode is covered in [Development Mode](development-mode.md).

## FAQ

### **Q: Why should I choose `[0] Do not inject` at the prompt?**

A: `config/config.php` already registers the ConfigProviders that the installer offers to inject.
Choosing `[1]` adds them a second time.

### **Q: The install fails because `ext-intl` is missing. What should I do?**

A: Enable `extension=intl` in your `php.ini` and run `composer install` again; `laminas/laminas-i18n` requires it.

### **Q: Which files does `composer install` create?**

A: `bin/composer-post-install-script.php` creates `config/autoload/local.php` and `config/autoload/mail.global.php` if they are missing.
It creates `config/autoload/local.test.php` only when development mode is already enabled.

### **Q: Where are the packages installed?**

A: In the `vendor` folder.
