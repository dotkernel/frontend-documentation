# Running the application

## Summary

This page runs Dotkernel Frontend in a virtual host on WSL.
It also covers the two local-only fixes: clearing a stale configuration cache and turning off secure session cookies.

## Details

We recommend running your applications in WSL:

- Make sure you have [WSL](https://github.com/dotkernel/development/blob/main/wsl/README.md) installed on your system.
- Currently we provide a distro implementations for [AlmaLinux 9](https://github.com/dotkernel/development/blob/alma-linux-9/README.md) and [AlmaLinux 10](https://github.com/dotkernel/development/blob/alma-linux-10/README.md)
- Install the application in a virtualhost as recommended by the chosen distro.
- Set `$baseUrl` in **config/autoload/local.php** to the address of the virtualhost.
- Run the application by opening the virtualhost address in your browser.

You should see the `Dotkernel Frontend` welcome page.

> If you are getting exceptions or errors regarding some missing services, try running the following command:

```shell
sudo php bin/clear-config-cache.php
```

> If `config-cache.php` is present that config will be loaded regardless of the `ConfigAggregator::ENABLE_CACHE` in `config/autoload/mezzio.global.php`

> **Development only**: `session.cookie_secure` does not work locally so make sure you modify your `local.php`, as per the following:

```php
# other code

return [
    # other configurations...
    'session_config' => [
        'cookie_secure' => false,
    ],
];
```

Do not change this in `local.php.dist` as well because this value should remain `true` on production.

## FAQ

### **Q: Which address does the application use?**

A: The `$baseUrl` value in `config/autoload/local.php`, which is `http://dotkernel.local` by default.
Set it to the address of your virtual host.

### **Q: Can I run Frontend without a virtual host?**

A: Yes, for a quick look. `composer serve` starts PHP's built-in server on port 8080 (`php -S 0.0.0.0:8080 -t public/`).
Set `$baseUrl` to match.

### **Q: Why am I logged out after every request on my local machine?**

A: `session_config` => `cookie_secure` is `true`, so the browser sends the session cookie only over HTTPS.
Set it to `false` in your `local.php` when you develop over plain HTTP.

### **Q: Why do my configuration changes have no effect?**

A: A configuration cache is being loaded.
Enable development mode, or run `php bin/clear-config-cache.php`.
