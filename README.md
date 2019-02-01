# Socialite for WordPress

WordPress.com and Self-hosted WordPress.

## For Self-hosted WordPress
You must install WP OAuth Server plugin.

https://wordpress.org/plugins/oauth2-provider/

## Installation
```
composer require revolution/socialite-wordpress
```

### config/services.php

```php
    'wordpress' => [
        // Endpoint for WordPress.com
        // 'host'          => env('WORDPRESS_HOST', 'https://public-api.wordpress.com/oauth2'),
        // 'api_me'        => env('WORDPRESS_API_ME', 'https://public-api.wordpress.com/rest/v1.1/me'),

        // Endpoint for Self-hosted WordPress
        'host'   => env('WORDPRESS_HOST'),
        'api_me' => env('WORDPRESS_API_ME', env('WORDPRESS_HOST') . '/me/'),

        'client_id'     => env('WORDPRESS_CLIENT_ID'),
        'client_secret' => env('WORDPRESS_CLIENT_SECRET'),
        'redirect'      => env('WORDPRESS_REDIRECT'),
    ],
```

### .env
```
WORDPRESS_HOST=https://example.com/oauth
#WORDPRESS_API_ME=
WORDPRESS_CLIENT_ID=
WORDPRESS_CLIENT_SECRET=
WORDPRESS_REDIRECT=
```

## Usage

routes/web.php
```
Route::get('login', 'SocialiteController@login');
Route::get('callback', 'SocialiteController@callback');
```

SocialiteController

```php
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Socialite;

class SocialiteController extends Controller
{
    public function login()
    {
        return Socialite::driver('wordpress')->redirect();
    }

    public function callback()
    {
        $user = Socialite::driver('wordpress')->user();
        dd($user);
    }
}

```

## Demo
https://github.com/kawax/socialite-project

## LICENCE
MIT

Copyright kawax
