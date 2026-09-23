# Authorization Guards

## Summary

This page explains how Dotkernel Frontend restricts access: roles and their permissions are defined in `authorization.global.php`, and `authorization-guards.global.php` requires those permissions for specific routes and controller actions.

## Details

The packages responsible for restricting access to certain parts of the application are [dot-rbac-guard](https://github.com/dotkernel/dot-rbac-guard) and [dot-rbac](https://github.com/dotkernel/dot-rbac).
These packages work together to create an infrastructure that is customizable and diversified to manage user access to the platform by specifying the type of role the user has.

The `authorization.global.php` file provides multiple configurations specifying multiple roles as well as the types of permissions to which these roles have access.

```php
// config/autoload/authorization.global.php - flat RBAC model shipped with Frontend
'dot_authorization' => [
    'guest_role'    => 'guest',
    'role_provider' => [
        'type'    => 'InMemory',
        'options' => [
            'roles' => [
                'user'  => [
                    'permissions' => [
                        'authenticated',
                        'premium',
                    ],
                ],
                'guest' => [
                    'permissions' => [
                        'unauthenticated',
                    ],
                ],
            ],
        ],
    ],
],
```

The `authorization-guards.global.php` file provides configuration to restrict access to certain actions based on the permissions defined in `authorization.global.php` so basically we have to add the permissions in the dot-rbac configuration file first to specify the action restriction permissions.

```php
// config/autoload/authorization-guards.global.php - ControllerPermission guard shipped with Frontend
'type'    => 'ControllerPermission',
'options' => [
    'rules' => [
        [
            'route'       => 'account',
            'actions'     => [ // list of actions to apply, or empty array for all actions
                'avatar',
                'details',
                'changePassword',
                'deleteAccount',
            ],
            'permissions' => ['authenticated'],
        ],
        [
            'route'       => 'page',
            'actions'     => [
                'premium-content',
            ],
            'permissions' => ['premium'], // list of permissions required
        ],
    ],
],
```

> The default `protection_policy` is `GuardInterface::POLICY_ALLOW`: routes and actions without a rule are accessible to everyone.

## FAQ

### **Q: What happens to routes and actions that have no rule?**

A: They are open to everyone.
The shipped `protection_policy` is `GuardInterface::POLICY_ALLOW`.

### **Q: Which role does a visitor who is not logged in have?**

A: `guest`, as set by `guest_role` in `authorization.global.php`.
It has only the `unauthenticated` permission.

### **Q: How do I protect every action of a route?**

A: Add a rule for the route with an empty `actions` array.

### **Q: What is the `premium` permission for?**

A: It protects the `premium-content` action of the `page` route (`/page/premium-content`).
The shipped `user` role has it, so any logged-in user can open the page.

### **Q: Where are a user's roles stored?**

A: In the `user_role` table, linked to users through `user_roles`.
The default roles are created by the `RoleLoader` fixture.
