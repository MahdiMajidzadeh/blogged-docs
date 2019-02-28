# Authorization

In addition to providing authentication feature out of the box, LaRecipe also provides a simple way to authorize user access against a specific action.

---

- [Why?](#why)
- [How?](#how)

<a name="why">
## Why?

Let's say you have a team of users that you want to give them access to the dashboard but with limited permission. For instance, only admins can delete and update articles and categories where others they can only write articles and so on..

<a name="how">
## How?

Blogged provides an easy way to activate the authorization feature using Laravel policy. Please have a look at the [official documentation](https://laravel.com/docs/5.7/authorization) if you're not familiar with.

```bash
php artisan blogged:policies
```

This command will create:

- `app/Policies/BloggedArticlePolicy`
- `app/Policies/BloggedCategoryPolicy.php`

If you have changed your app namespace, it will be correctly set up.


> {info} These policies are automatically loaded by Blogged Service Provider.

By default, these policies allow everything. It's up to you to edit the authorizations to fit your needs.
