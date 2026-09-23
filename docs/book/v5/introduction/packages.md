# Packages

## Summary

This page lists the Composer packages that Dotkernel Frontend requires directly, with a one-line description of what each one provides.

## Details

* `dotkernel/dot-authorization` - Authorization base package defining interfaces for authorization services to be used with Dotkernel applications
* `dotkernel/dot-cache` - Cache adapters used by Doctrine for metadata, query, result and hydration caching
* `dotkernel/dot-controller` - Provides base classes for action based controllers similar to Laminas controller component
* `dotkernel/dot-data-fixtures` - Provides a CLI interface for listing & executing doctrine data fixtures
* `dotkernel/dot-dependency-injection` - Dependency injection component using class attributes
* `dotkernel/dot-errorhandler` - Logging Error Handler for Middleware Applications
* `dotkernel/dot-flashmessenger` - Provides session messages between redirects
* `dotkernel/dot-mail` - Mail component based on laminas-mail
* `dotkernel/dot-navigation` - Allows you to easily define and parse menus inside templates, configuration based approach
* `dotkernel/dot-rbac-guard` - Defines authorization guards that authorize users for accessing certain parts of an application based on various criteria
* `dotkernel/dot-response-header` - Middleware for setting custom response headers
* `dotkernel/dot-session` - Dotkernel session component extending and customizing laminas-session
* `dotkernel/dot-twigrenderer` - Dotkernel component providing twig extensions and customizations
* `friendsofphp/proxy-manager-lts` - Fork of ocramius/proxy-manager
* `laminas/laminas-component-installer` - Composer plugin for injecting modules and configuration providers into application configuration
* `laminas/laminas-config-aggregator` - Lightweight library for collecting and merging configuration from different sources
* `laminas/laminas-form` - Bridge between your domain models and the View Layer
* `laminas/laminas-i18n` - Complete translation suite
* `mezzio/mezzio` - PSR-15 Middleware Microframework
* `mezzio/mezzio-authorization-rbac` - mezzio authorization rbac adapter for laminas/laminas-permissions-rbac
* `mezzio/mezzio-cors` - CORS component for Mezzio and other PSR-15 middleware runners
* `mezzio/mezzio-fastroute` - FastRoute integration for Mezzio
* `ramsey/uuid-doctrine` - Use ramsey/uuid as a Doctrine field type
* `roave/psr-container-doctrine` - Doctrine Factories for PSR-11 Containers

## FAQ

### **Q: Where is the authoritative list of dependencies?**

A: In the `require` section of `composer.json`.
Development tools such as PHPUnit, PHPStan, the Laminas coding standard, Twig CS Fixer, Whoops and laminas-development-mode are in `require-dev`.

### **Q: Which package handles routing?**

A: `mezzio/mezzio-fastroute`, the FastRoute integration for Mezzio.

### **Q: Which templating engine does Frontend use?**

A: Twig, through `mezzio/mezzio-twigrenderer`, with Dotkernel's extensions from `dotkernel/dot-twigrenderer`.

### **Q: Which packages control access to pages?**

A: `dotkernel/dot-rbac-guard` applies the guards, and `dotkernel/dot-authorization` and `mezzio/mezzio-authorization-rbac` provide the role and permission model.
See [Authorization Guards](../how-to/authorization.md).
