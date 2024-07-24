# Configuration Files

## Prepare config files

* duplicate `config/autoload/debugbar.local.php.dist` as `config/autoload/debugbar.local.php`

* duplicate `config/autoload/development.local.php.dist` as `config/autoload/development.local.php`

### Note

* duplicate `config/autoload/local.php.dist` as `config/autoload/local.php`

* duplicate `config/autoload/mail.local.php.dist` as `config/autoload/mail.local.php`

### Note

> If you intend to send emails from your Frontend, make sure to fill in SMTP connection params. This will be covered in the next section.

* **optional**: in order to run/create tests, duplicate `config/autoload/local.test.php.dist` as `config/autoload/local.test.php`

### Note

> this creates a new in-memory database that your tests will run on.

## Configuration - Mail

If you want your application to send mails on registration, contact etc. add valid credentials to the following keys in `config/autoload/mail.local.php`

Under `message_options` key:

- `from` - email address that will send emails (required)
- `from_name` - organization name for signing sent emails (optional)

Under `smtp_options` key:

- `host` - hostname or IP address of the mail server (required)
- `connection_config` - add the `username` and `password` keys (required)

In `config/autoload/local.php` edit the key `contact` => `message_receivers` => `to` with *string* values for emails that should receive contact messages.

Note: **Please add at least 1 email address in order for contact message to reach someone**

Also feel free to add as many CCs as you want under the `contact` => `message_receivers` => `cc` key.

## Configuration - reCAPTCHA

reCAPTCHA is used to prevent abusive activities on your website. DotKernel frontend uses the Google reCAPTCHA for its contact us form.
You must first generate a `siteKey` and `secretKey` in your Google account - [Google reCAPTCHA](https://www.google.com/recaptcha/admin)

Update the `recaptcha` array in `config/autoload/local.php` with the `siteKey` and `secretKey` from Google reCAPTCHA.

Note: you need to whitelist `localhost` in the reCAPTCHA settings page during development.
**When in production do not forget to either remove `localhost` from the reCAPTCHA whitelist, or have a separate reCAPTCHA**
