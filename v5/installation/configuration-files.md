# Configuration Files

## Summary

This page prepares the local configuration files and fills in the database, mail, contact recipients and reCAPTCHA settings that Dotkernel Frontend needs.

## Details

This step involves changing the names of or duplicating some of the `.dist` files in the project and editing their content to suit your project's requirements.

## Prepare config files

- `config/autoload/development.local.php` is created from its `.dist` file when you run `composer development-enable`; do not duplicate it manually.
- `composer install` creates `config/autoload/mail.global.php` from `vendor/dotkernel/dot-mail/config/mail.global.php.dist`; duplicate it as `config/autoload/mail.local.php` for your credentials, because `*.local.php` files are ignored by git and override `*.global.php`.
- Edit `config/autoload/local.php` (created from `local.php.dist` by `composer install`) according to your dev machine and fill in the `database` configuration.

> If you intend to send emails from your Frontend, make sure to fill in SMTP connection params.
> This is covered in the [Mail](#mail) section below.

> **Optional**: in order to run/create tests, duplicate `config/autoload/local.test.php.dist` as `config/autoload/local.test.php`.
> This creates a new in-memory database that your tests will run on.

## Mail

If you want your application to send mails on registration, contact etc. add valid credentials to the following keys under `dot_mail` => `default` in `config/autoload/mail.local.php`

Under `message_options` key:

- `from` - email address that will send emails (required)
- `from_name` - organization name for signing sent emails (optional)

To send through SMTP, set `transport` to `esmtp` (the default is `sendmail`).

Under `smtp_options` key:

- `host` - hostname or IP address of the mail server (required)
- `connection_config` - add the `username` and `password` keys (required)

In `config/autoload/local.php` edit the key `contact` => `message_recipients` => `to` with an array of email addresses that should receive contact messages.

> **Please add at least 1 email address in order for contact message to reach someone**

Also feel free to add as many CCs and BCCs as you require under the `contact` => `message_recipients` => `cc` and `bcc` keys.
The optional `contact` => `message_sender` => `from_email` and `from_name` keys override the sender set in the `dot_mail` configuration.

## reCAPTCHA

reCAPTCHA is used to prevent abusive activities on your website.
Dotkernel frontend uses the Google reCAPTCHA for its `contact us` form.

- Generate a `siteKey` and `secretKey` in your Google account: [Google reCAPTCHA](https://www.google.com/recaptcha/admin)

- Update the `recaptcha` array in `config/autoload/local.php` with the `siteKey` and `secretKey` from Google reCAPTCHA.

> The contact page throws an `Invalid siteKey provided.` exception until both keys are filled in.

- Adjust `scoreThreshold` if needed (a float between `0.0` and `1.0`, default `0.5`); a submission passes only when Google's response `score` is higher than this value.

> You need to whitelist `localhost` in the reCAPTCHA settings page during development.

>**When in production do not forget to either remove `localhost` from the reCAPTCHA whitelist, or have a separate reCAPTCHA**

## FAQ

### **Q: Which configuration files are safe for credentials?**

A: `config/autoload/local.php` and any `config/autoload/*.local.php` file, which git ignores.
`mail.global.php` is not ignored, so put SMTP credentials in a `mail.local.php`.

### **Q: Do I have to configure mail?**

A: Only if the application should send the registration, activation, password reset and contact emails.
The default transport is `sendmail`; set `transport` to `esmtp` to send through an SMTP server.

### **Q: Who receives the messages sent from the contact form?**

A: The addresses under `contact` => `message_recipients` in `config/autoload/local.php`: `to`, plus optional `cc` and `bcc`.

### **Q: Why does the contact page fail with "Invalid `siteKey` provided."?**

A: The reCAPTCHA `siteKey` or `secretKey` in `config/autoload/local.php` is empty.
The contact page needs both keys before it can render.

### **Q: What is `local.test.php` for?**

A: It points Doctrine at an in-memory SQLite database, but only while the tests have enabled test mode, so your development database is never touched.
