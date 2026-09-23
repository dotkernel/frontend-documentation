# Dependency Injection

## Summary

This page explains how Dotkernel Frontend injects constructor dependencies with the `#[Inject]` attribute from `dot-dependency-injection`, and how to register a class with `AttributedServiceFactory` so that no factory has to be written.

## Details

Dependency injection is a design pattern used in software development to implement inversion of control.
In simpler terms, it's the act of providing dependencies for an object during instantiation.

In PHP, dependency injection can be implemented in various ways, including through constructor injection, setter injection and property injection.

Dotkernel Frontend, through its [dot-dependency-injection](https://github.com/dotkernel/dot-dependency-injection) package focuses only on constructor injection.

## Usage

**Dotkernel Frontend** comes out of the box with the [dot-dependency-injection](https://github.com/dotkernel/dot-dependency-injection) package, which provides all the functionality injecting dependencies into any object you want.

`dot-dependency-injection` determines the dependencies by looking at the `#[Inject]` attribute, added to the constructor of a class.
Each dependency is specified as a separate parameter of the `#[Inject]` attribute.

For our example we will inject `UserServiceInterface` and `config` dependencies into a `UserController`.

```php
use Dot\Controller\AbstractActionController;
use Dot\DependencyInjection\Attribute\Inject;

class UserController extends AbstractActionController
{
    #[Inject(
        UserServiceInterface::class,
        "config",
    )]
    public function __construct(
        protected UserServiceInterface $userService,
        protected array $config = [],
    ) {
    }
}
```

> If your class needs the value of a specific configuration key, you can specify the path using dot notation: `config.example`

The next step is to register the class in the `ConfigProvider` under `factories` using
`Dot\DependencyInjection\Factory\AttributedServiceFactory::class`.

```php
public function getDependencies(): array
{
    return [
        'factories' => [
            UserController::class => AttributedServiceFactory::class
        ]
    ];
}
```

That's it.
When your object is instantiated from the container, it will automatically have its dependencies resolved.

> Dependencies injection is available to any object within Dotkernel Frontend.
> For example, you can inject dependencies in a service, a controller and so on, simply by registering them in the `ConfigProvider`.

## FAQ

### **Q: Do I still need to write factories?**

A: Not for classes that use `#[Inject]`.
Register services and controllers with `AttributedServiceFactory`, and Doctrine repositories with `AttributedRepositoryFactory`, as `src/User/src/ConfigProvider.php` does.

### **Q: How do I inject a single configuration key?**

A: Use dot notation in the attribute.
For example, `RecaptchaService` uses `#[Inject("config.recaptcha")]` to receive only the `recaptcha` array.

### **Q: Does the order of the `#[Inject]` arguments matter?**

A: Yes. The dependencies are passed to the constructor in the order they are listed, so the list must match the order of the constructor parameters.

### **Q: Does the package support setter or property injection?**

A: No. `dot-dependency-injection` supports constructor injection only.
