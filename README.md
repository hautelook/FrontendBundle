Hautelook Frontend
==================

This bundle holds the general style guide that should be used at HauteLook for all
backend (admin) applications. It uses less to compile the CSS files. It also includes
a base `layout.html.twig` file that should be extended by the application.

Installation
------------

Require the package with composer (this will install all the dependencies such as Twitter
Bootstrap, Font-Awesome, etc.):

```bash
$ composer require "hautelook/frontend-bundle"
```

You then need to make sure that the Assetic Bundle is in the Kernel:

```php
// app/AppKernel.php

$bundles = array(
    new Symfony\Bundle\AsseticBundle\AsseticBundle(),
    new Hautelook\FrontendBundle\HautelookFrontendBundle(),
);
```

and include the `assetic.yml` config file in the bundle:

```yaml
# app/config/config.yml

imports:
- { resource: ../../vendor/hautelook/frontend-bundle/Hautelook/FrontendBundle/Resources/config/assetic.yml }
```

You should now be able to

```bash
$ app/console assets:install
$ app/console assetic:dump
```

Usage
-----

You should create your own application/bundle specific `layout.html.twig` file that extends
from the layout bundle's one. That way you can set the application specific settings such as
the Navigation bar (application title, as well as the menu), as well as the title.

Example:

```html
{% extends 'HautelookFrontendBundle::layout.html.twig' %}

{% block application_title %} &mdash; Hautelook Application{% endblock application_title %}

{% block header %}
    <nav class="navbar navbar-inverse navbar-static-top" role="navigation">
        <div class="container">
            <div class="navbar-header">
                <a href="/" class="navbar-brand">
                    <i class="fa fa-lock"></i>
                    Hautelook Application
                    <span class="hl-theme-color"></span>
                </a>
            </div>
        </div>
    </nav>
{% endblock header %}
```

ToDo
----

There are still quite a few todos.

- Get rid of the jQuery vendor files in `Resources/public/js`
- Add the right hand Navbar with login information (requires Gravatar bundle)
- Add tests (Run Assetic:dump, Twig lint)
- Figure out if there is a better way to manage the assetic configuration in a way that does not store
  the whole assetic config file in the bundle (inflexible), but also does not suck.

