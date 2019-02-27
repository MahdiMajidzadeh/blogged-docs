# Integrating with Laravel Nova

You have Nova dashboard already? no issues!

---

- [Overview](#overview)

<a name="overview"></a>
## Overview

If you already have Laravel [Nova](https://nova.laravel.com) and you want to use it as a dashboard for Blogged you can do so by following this simple steps:

1. Deavtivate Blogged dashboard (optional)
2. Write Nova resources for each of `Category` and `Article` models

---

> {primary} Deavtivate Blogged dashboard (optional)

In order to deactivate blogged dashboard, change the default settings of dashboard inside `config/blogged.php`:


```php
return [
    'settings'       => [
        'dashboard'  => true, //change to false
    ]
];
```

> {primary} Write Nova resources for each of `Category` and `Article` models

Run the following two commands to generate nova resources:

```bash
php artisan nova:resource Article
php artisan nova:resource Category
```

> {success} Copy the following code to `app/Nova/Article` file:

```php
<?php

namespace App\Nova;

use Laravel\Nova\Fields\ID;
use Illuminate\Http\Request;
use Laravel\Nova\Fields\Text;
use Laravel\Nova\Fields\File;
use Laravel\Nova\Fields\Date;
use Laravel\Nova\Fields\Boolean;
use Laravel\Nova\Fields\Markdown;
use Laravel\Nova\Fields\BelongsTo;
use Laravel\Nova\Http\Requests\NovaRequest;

class Article extends Resource
{
    /**
     * The model the resource corresponds to.
     *
     * @var string
     */
    public static $model = 'BinaryTorch\Blogged\Models\Article';

    /**
     * The single value that should be used to represent the resource when being displayed.
     *
     * @var string
     */
    public static $title = 'title';

    /**
     * The columns that should be searched.
     *
     * @var array
     */
    public static $search = [
        'id', 'title', 'status'
    ];

    /**
     * Get the fields displayed by the resource.
     *
     * @param  \Illuminate\Http\Request  $request
     * @return array
     */
    public function fields(Request $request)
    {
        return [
            ID::make()->sortable(),
            
            BelongsTo::make('User', 'author'),

            BelongsTo::make('Category', 'category'),

            Text::make('Title')
                ->sortable()
                ->rules('required', 'max:255'),

            Text::make('URL', 'slug')
                ->hideFromIndex()
                ->rules('required', 'max:255'),

            File::make('image')
                ->disk('public')
                ->hideFromIndex(),


            Text::make('Excerpt')
                ->hideFromIndex()
                ->rules('required', 'max:255'),

            Markdown::make('Body')
                ->hideFromIndex()
                ->rules('required'),

            Date::make('Publish Date', 'publish_date'),

            Boolean::make('Featured')
                ->hideFromIndex(),

            Boolean::make('Published'),
        ];
    }
}
```

> {success} Copy the following code to `app/Nova/Category` file:

```php
<?php

namespace App\Nova;

use Laravel\Nova\Fields\ID;
use Illuminate\Http\Request;
use Laravel\Nova\Fields\Text;
use Laravel\Nova\Fields\HasMany;
use Laravel\Nova\Http\Requests\NovaRequest;

class Category extends Resource
{
    /**
     * The model the resource corresponds to.
     *
     * @var string
     */
    public static $model = 'BinaryTorch\Blogged\Models\Category';

    /**
     * The single value that should be used to represent the resource when being displayed.
     *
     * @var string
     */
    public static $title = 'title';

    /**
     * The columns that should be searched.
     *
     * @var array
     */
    public static $search = [
        'id', 'title',
    ];

    /**
     * Get the fields displayed by the resource.
     *
     * @param  \Illuminate\Http\Request  $request
     * @return array
     */
    public function fields(Request $request)
    {
        return [
            ID::make()->sortable(),
            
            Text::make('Title')
                ->sortable()
                ->rules('required', 'max:255'),

            Text::make('URL', 'slug')
                ->hideFromIndex()
                ->rules('required', 'max:255'),

            HasMany::make('articles')
        ];
    }
}
```