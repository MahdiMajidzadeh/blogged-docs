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

Blogged provides an easy way to activate the authorization feature using Laravel policy. Please have a look at the [official documnetation](https://laravel.com/docs/5.7/authorization) if you're not familiar with.

Create two new files called `BloggedArticlePolicy.php` and `BloggedCategoryPolicy.php` inside `app/Policies` directory. Then, copy and paste the code below to the respective file:


> {success} BloggedArticlePolicy.php

```php
<?php

namespace App\Policies;

use App\User;
use BinaryTorch\Blogged\Models\Article;
use Illuminate\Auth\Access\HandlesAuthorization;

class BloggedArticlePolicy
{
    use HandlesAuthorization;

    /**
     * Determine whether the user can view the article.
     *
     * @param  \App\User  $user
     * @param  Article  $article
     * @return mixed
     */
    public function view(User $user, Article $article)
    {
        return true;
    }

    /**
     * Determine whether the user can create articles.
     *
     * @param  \App\User  $user
     * @return mixed
     */
    public function create(User $user)
    {
        return true;
    }

    /**
     * Determine whether the user can update the article.
     *
     * @param  \App\User  $user
     * @param  Article  $article
     * @return mixed
     */
    public function update(User $user, Article $article)
    {
        return true;
    }

    /**
     * Determine whether the user can delete the article.
     *
     * @param  \App\User  $user
     * @param  Article  $article
     * @return mixed
     */
    public function delete(User $user, Article $article)
    {
        return true;
    }
}
```

> {success} BloggedCategoryPolicy.php


```php
<?php

namespace App\Policies;

use App\User;
use BinaryTorch\Blogged\Models\Category;
use Illuminate\Auth\Access\HandlesAuthorization;

class BloggedCategoryPolicy
{
    use HandlesAuthorization;

    /**
     * Determine whether the user can create categories.
     *
     * @param  \App\User  $user
     * @return mixed
     */
    public function create(User $user)
    {
        return true;
    }

    /**
     * Determine whether the user can update the category.
     *
     * @param  \App\User  $user
     * @param  Category  $category
     * @return mixed
     */
    public function update(User $user, Category $category)
    {
        return true;
    }

    /**
     * Determine whether the user can delete the category.
     *
     * @param  \App\User  $user
     * @param  Category  $category
     * @return mixed
     */
    public function delete(User $user, Category $category)
    {
        return true;
    }
}
```


Finally, once you prepared the policies you want, don't forget to add them in your `AuthServiceProvider` in the `policies` array:

```php
    /**
     * The policy mappings for the application.
     *
     * @var array
     */
    protected $policies = [
        //..
        \BinaryTorch\Blogged\Models\Article::class => \App\Policies\BloggedArticlePolicy::class,
        \BinaryTorch\Blogged\Models\Category::class => \App\Policies\BloggedCategoryPolicy::class,
    ];
```