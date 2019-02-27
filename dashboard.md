# Blog Dashboard

Blogged comes with a beautiful looking user interface and dashboard which is highly configurable to fit your need.

---

- [Overview](#overview)
- [Screenshots](#screenshots)
- [Settings](#overview)

<a name="overview"></a>
## Overview

The dashboard section comes with all main features that needed for CRUD operations, including creating articles, uploading images and so on.

By default, normal auth users have entire access and permission to all actions in the dashboard. However, you can limit your users' access by adding custom policies. See [Authorization](/docs/{{version}}/authorization) section for more details.

<a name="screenshots"></a>
## Screenshots

This are few screenshots from the dashboard UI. You can see actual demo [here](/blog/dashboard).
1. Dashboard

![dashboard screenshot](/dashboard-screenshot.png)

2. Categories

![categories screenshot](/categories-screenshot.png)

3. New Article

![article screenshot](/article-screenshot.png)

<a name="settings"></a>
## Settings

If you have your own admin panel or dashboard and you want to disable this dashboard you can do so by changing the config settings section:

```php
return [
    'settings'       => [
        'dashboard'  => true, // change to false :)
    ]
];
```