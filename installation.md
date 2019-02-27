# Installation

Blogged comes with custom Artisan install command which make the process like a breeze.

> {warning} Before you run the install command, make sure you setup the DB connection and run the migrations. Also, please make sure you run the auth command or you prepare you own `login` page.

---

- [Install](#install)
- [View](#view)

<a name="install"></a>
## Install

> {primary} If you are installing with Laravel v5.4 you will need to add the Service Provider manually. Otherwise, if you are on v5.5 and above this happens automatically.


Install via composer

```php
composer require binarytorch/blogged
```

Then, run the install command to publish the needed assets and configurations.

```php
php artisan blogged:install
```

<a name="view"></a>
## View

### Blog 

1. Using Laravel Valet: visit `yourdomain.test/blog`.
2. Using Laravel serve: `http://127.0.0.1:8000/blog`.

### Blog Dashboard

1. Using Laravel Valet: visit `yourdomain.test/blog/dashboard`.
2. Using Laravel serve: `http://127.0.0.1:8000/blog/dashboard`.