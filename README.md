# Schranz Template Renderer Integration for Latte

Integrate the templating [Latte Adapter](https://github.com/schranz-templating/latte-adapter) 
into the Symfony Framework.

Part of the [Schranz Templating Project](https://github.com/schranz-templating/templating).

## Installation

Install this package via Composer:

```bash
composer require schranz-templating/symfony-latte-integration
```

Register the Bundle class in your `config/bundles.php` or Kernel file:

```php
return [
    // ...
    Schranz\Templating\Integration\Symfony\Latte\SchranzTemplatingLatteBundle::class => ['all' => true],
];
```

## Configuration

The Latte Integration has the following configuration available:

```yaml
schranz_templating_latte:
    default_path: '%kernel.project_dir%/templates'
    cache: '%kernel.cache_dir%/latte'
```

None of the configuration is required.

### default_path

**type:** `string` **default:** `'%kernel.project_dir%/templates'`

The path to the directory where Symfony will look for the application Latte templates by default.

### cache

**type:** `string` **default:** `'%kernel.cache_dir%/latte'`

Before using the Latte templates to render some contents, they are compiled into regular PHP code. Compilation is a costly process, so the result is cached in the directory defined by this configuration option.

## Extensions

To extend Latte functionality you can create a new service extending from `Latte\Extension`
which when `autoconfigure` is enabled automatically be tagged with `latte.extension` and added
as a Latte Extension. If not you need to tag the service yourself:

```yaml
services:
    App\Latte\MyExtension:
        tags:
            - { name: latte.extension }
```

Read more about Latte Extensions in the [Latte documentation](https://latte.nette.org/en/creating-extension).
