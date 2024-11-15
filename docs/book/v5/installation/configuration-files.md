# Configuration Files

This step involves changing the names of or duplicating some of the `.dist` files in the project and editing their content to suit your project's requirements.

## Prepare config files

- Duplicate `config/autoload/debugbar.local.php.dist` as `config/autoload/debugbar.local.php`
- Duplicate `config/autoload/development.local.php.dist` as `config/autoload/development.local.php`
- Duplicate `config/autoload/local.php.dist` as `config/autoload/local.php`
- Duplicate `config/autoload/mail.local.php.dist` as `config/autoload/mail.local.php`
- Edit `config/autoload/local.php` according to your dev machine and fill in the `database` configuration.

> If you intend to send emails from your Frontend, make sure to fill in SMTP connection params.
> This will be covered in the next section.

> **Optional**: in order to run/create tests, duplicate `config/autoload/local.test.php.dist` as `config/autoload/local.test.php`.
> This creates a new in-memory database that your tests will run on.

## Mail

If you want your application to send mails on registration, contact etc. add valid credentials to the following keys in `config/autoload/mail.local.php`

Under `message_options` key:

- `from` - email address that will send emails (required)
- `from_name` - organization name for signing sent emails (optional)

Under `smtp_options` key:

- `host` - hostname or IP address of the mail server (required)
- `connection_config` - add the `username` and `password` keys (required)

In `config/autoload/local.php` edit the key `contact` => `message_receivers` => `to` with *string* values for emails that should receive contact messages.

> **Please add at least 1 email address in order for contact message to reach someone**

Also feel free to add as many CCs as you require under the `contact` => `message_receivers` => `cc` key.

## reCAPTCHA

reCAPTCHA is used to prevent abusive activities on your website.
Dotkernel frontend uses the Google reCAPTCHA for its `contact us` form.

- Generate a `siteKey` and `secretKey` in your Google account: [Google reCAPTCHA](https://www.google.com/recaptcha/admin)

- Update the `recaptcha` array in `config/autoload/local.php` with the `siteKey` and `secretKey` from Google reCAPTCHA.

> You need to whitelist `localhost` in the reCAPTCHA settings page during development.

>**When in production do not forget to either remove `localhost` from the reCAPTCHA whitelist, or have a separate reCAPTCHA**
