# Only call env() inside config files

In production you should run `php artisan config:cache`. Once the config is cached, Laravel stops loading `.env`, so any `env()` call outside `config/` returns `null`.

```php
// config/services.php
'wallet' => [
    'team_id' => env('APPLE_TEAM_ID'),
],

// anywhere else in your app
$teamId = config('services.wallet.team_id'); // not env('APPLE_TEAM_ID')
```

Add `php artisan config:cache` and `php artisan route:cache` to your deploy script to get a faster boot as well.
