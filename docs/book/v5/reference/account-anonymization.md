# Account anonymization

## Summary

This page explains why Dotkernel Frontend anonymizes user accounts instead of deleting them, which personal data it stores, and exactly what the anonymization process replaces.

## Premise

According to the GDPR, companies that record personal data from EU citizens must delete said data if its owner requests its deletion.
An alternative is to anonymize the data, according to [this article](https://commission.europa.eu/law/law-topic/data-protection/reform/rules-business-and-organisations/dealing-citizens/do-we-always-have-delete-personal-data-if-person-asks_en).

## Definition

### What is Personally identifiable information?

According to [this article](https://commission.europa.eu/law/law-topic/data-protection/reform/what-personal-data_en), Personally identifiable information (PII) is:

- A name and surname.
- A home address.
- An email address such as name.surname@company.com.
- An identification card number.
- Location data (for example the location data function on a mobile phone).
- An Internet Protocol (IP) address.
- A cookie ID.
- The advertising identifier of your phone.
- A phone number.
- Data held by a hospital or doctor, which could be a symbol that uniquely identifies a person.

Out of the box, Dotkernel Frontend saves the user's name (firstname and lastname) and email (identity).
This personal data is used for emails related to password reset and account activation.

> Other tables can also hold personal data: `contact_message` stores the name and email of each contact form sender, `user_remember_me` stores the browser user agent, and `user_avatar` references an uploaded image.
> Anonymization does not change `contact_message` or `user_remember_me` records.

## Process

### Anonymization

Anonymization runs when a logged-in user deletes their account (`/account/delete-account`), and when a pending account is unregistered through the link in the activation email (`/account/unregister/{hash}`).
The user record is kept, its status is set to `deleted`, and the process makes these replacements:

- The firstname and lastname are replaced with `anonymous` concatenated with the current date and time in `dmYHis` format, e.g. `anonymous23092026155300`.
- The email is replaced with the same value concatenated with the value in `userAnonymizeAppend`, e.g. `anonymous23092026155300@example.com`.
- On account deletion, the avatar image, its upload folder and its database record are deleted.

The `userAnonymizeAppend` key can be set in `config/autoload/local.php` or left empty.

> Using an email domain for `userAnonymizeAppend` would work as a catch-all email, if your email service provider has this option enabled.

## FAQ

### **Q: Is the user record deleted?**

A: No. The record is kept, its status is set to `deleted`, and the name and email are replaced.

### **Q: Can an anonymized user log in again?**

A: No. Login accepts only accounts whose status is `active`, as set in `config/autoload/authentication.global.php`.

### **Q: What happens if `userAnonymizeAppend` is empty?**

A: The email is replaced by the placeholder alone, for example `anonymous23092026155300`, which is not a valid email address.

### **Q: Are contact form messages anonymized as well?**

A: No. Rows in `contact_message` keep the sender's name and email.

### **Q: Can two anonymized accounts clash?**

A: Yes, if both are anonymized in the same second.
The placeholder only has one-second resolution and `user.identity` is unique, so the second account fails to save.
