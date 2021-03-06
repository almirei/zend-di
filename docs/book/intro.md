# Introduction

## Dependency Injection

_Dependency Injection_ (here-in called DI) refers to the act of providing
dependencies for an object during instantiation or via a method call. A basic
example looks like this:

```php
$b = new MovieLister(new MovieFinder());
```

Above, `MovieFinder` is a dependency of `MovieLister`, and `MovieFinder` was
injected into `MovieLister`.

There are several forms of dependency injection:

- Constructor injection
- Setter injection
- Property (or field) injection

While previous versions of zend-di attempted to handle all three types, starting
in version 3, the component focuses only on the first, constructor injection.
This decision was made for several reasons:

- It simplified the implementation dramatically.
- The simplified implementation had performance benefits.
- It enforces the order of object initialization, which both helps to prevent
  circular dependencies, and ensures the completeness of the instantiated object.

> ### Further reading
>
> If you are not familiar with the concept of DI, here are several great reads:
>
> - [Matthew Weier O'Phinney's Analogy](http://weierophinney.net/matthew/archives/260-Dependency-Injection-An-analogy.html)
> - [Ralph Schindler's Learning DI](http://ralphschindler.com/2011/05/18/learning-about-dependency-injection-and-php)
> - [Fabien Potencier's Series](http://fabien.potencier.org/article/11/what-is-dependency-injection) on DI


> ### zend-servicemanager
>
> Since zend-di purely provides automatic DI (aka auto wiring), it does not
> provide code-driven [Inversion of Control](https://en.wikipedia.org/wiki/Inversion_of_control) (IoC).
>
> However, Zend Framework does ship with another IoC component as well: [zend-servicemanager](https://docs.zendframework.com/zend-servicemanager/).
> Unlike zend-di, zend-servicemanager is code-driven, meaning that you tell it
> what class to instantiate, or provide a factory for the given class. This allows
> you more fine-grained control on how your objects will be instantiated.
>
> In fact zend-di is designed to play nicely with other IoC containers that
> implement PSR-11, especially with zend-servicemanager. You can even use
> factories generated by zend-di for zend-servicemanager.

## Dependency Injection Containers

When your code is written in such a way that all your dependencies are injected
into consuming objects, you might find that the simple act of wiring an object
has gotten more complex. When this becomes the case, and you find that this
wiring is creating more boilerplate code, this makes for an excellent
opportunity to utilize a Dependency Injection Container. These containers are also
often referred to as IoC Containers.

In its simplest form, a Dependency Injection Container (here-in called a DiC
for brevity) is an object that is capable of creating objects on request and
managing the "wiring", or the injection of required dependencies, for those
requested objects. Since the patterns that developers employ in writing DI
capable code vary, DiC's are generally either in the form of smallish objects
that suit a very specific pattern, or larger DiC frameworks.

The PHP FIG defined a standard interface for such DiCs via [PSR-11
(ContainerInterface)](http://www.php-fig.org/psr/psr-11/).

zend-di is a DiC framework which provides an injector performing the wiring, and
a simple imlementation of a DiC. The injector is able to consume any PSR-11
container, such as [zend-servicemanager](https://docs.zendframework.com/zend-servicemanager/),
to obtain the instances of the dependencies.

While for the simplest use cases no configuration is needed, zend-di allows
developers to configure how to resolve dependencies for more complex use cases.

## Legacy documentation

The primary documentation covers version 3.0 and above. We also ship
documentation covering version 2 features, starting with a chapter covering
[zend-di Definition classes](v2/definitions.md).
