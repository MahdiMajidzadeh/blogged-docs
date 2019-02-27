# Configurations

With the installation of Blogged package you will find a new configuration file located at `config/blogged.php`.
In this file, you can find various options to change the configuration of your blog.

```php
.
└─ config
   └─ blogged.php
```

---

- [Routing](#routing)
- [Settings](#settings)
- [Appearance](#ui)
- [Social](#social)
- [Forum](#forum)
- [Authentication](#authentication)
- [Middlewares](#middlewares)

<a name="routing"></a>
## Routing

The default routes for the blog and the dashboard are `/blog` and `/blog/sashboard`.

> {info} Since Blogged doesn't force you to use custom login page, instead you can use your own login page by providing the login path to be used by Blogged in order to authenticate them.

```php
return [
    'docs'          => [
        'blog'      => 'blog',
        'dashboard' => 'blog/dashboard',
        'login'     => 'login',
    ]
];
```

However, if you don't have login page ready, you can run the auth command to make it for you.

```shell
php artisan make:auth
```

<a name="settings"></a>
## Settings

Blogged doesn't use any additional `users` table. By default, the author of the articles will be pointed to App\User class and the storage to the `local` disk. The Pagination number will relfect how many articles per page in both of blog and its dashboard.

```php
return [
    'settings'       => [
        'dashboard'  => true,
        'user'       => App\User::class,
        'storage'    => env('BLOGGED_STORAGE', 'local'),
        'ga_id'      => env('BLOGGED_GA', ''),
        'pagination' => 10,
    ]
];
```

<a name="ui"></a>
## Appearance

Here you can add configure the appearance of your blog. For example, you can change the default logo, control the visibility of the back-to-top button and many more. However, you can add your own CSS and JS files if you like.

> {primary} Currently Supported Themes: `light`, `dark`

```php
return [
    'ui'                   => [
        'show_app_name'    => true,
        'logo'             => '',   // e.g.: /logo.svg
        'fav'              => '',   // e.g.: /fav.png
        'columns'          => 1,    // 2, 3, 4
        'sidebar'          => true,
        'primary_color'    => '#ab3f61',
        'code'             => 'dark',
        'additional_css'   => [
            //'css/custom.css',
        ],
        'additional_js'    => [
            //'js/custom.js',
        ],
    ]
];
```

<a name="social"></a>
## Social

Blogged comes with handy little feature enables your readers to share your articles on thier social media accounts. Feel free to enable or disable any of the social media that you want.

```php
return [
    'social'        => [
        'twitter'   => true,
        'facebook'  => true,
        'linkedin'  => true,
        'pinterest' => true,
        'tumblr'    => false,
        'email'     => false,
        'telegram'  => false,
    ]
];
```

<a name="forum"></a>
## Forum

Giving a chance to your users to post their questions or feedback directly on your blog, is pretty nice way to engage them more. However, you can also disable the forum's visibility if you don't like the idea. Supported Services: `disqus`

> {info} [`Disqus`](https://disqus.com/) is a great way to setup forum inside your website/docs in few steps. Create a site and paste its name in the `site_name` to activate the disqus forum.

```php
return [
    'forum'                 => [
        'enabled'           => false,
        'default'           => 'disqus',
        'services'          => [
            'disqus'        => [
                'site_name' => '', // yoursite.disqus.com
            ]
        ]
    ]
];
```

<a name="authentication"></a>
## Authentication

This configuration option defines the authentication guard that will be used to protect your Blog routes. This option should match one of the authentication guards defined in the "auth" config file.

```php
return [
    'guard' => env('BLOGGED_GUARD', null),
];
```

<a name="middleware"></a>
## Middlewares

These middleware will be assigned to every Dashboard route, giving you the chance to add your own middleware to this stack or override any of the existing middleware. Or, you can just stick with this stack.

```php
use BinaryTorch\Blogged\Http\Middleware\Authorize;
use BinaryTorch\Blogged\Http\Middleware\Authenticate;

return [
    'middleware' => [
        'web',
        Authenticate::class,
        Authorize::class,
    ]
];
```