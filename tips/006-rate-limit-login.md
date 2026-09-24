# Rate limit your login form per email and IP

Without a limit, anyone can try thousands of passwords against one account. Define a named limiter that keys on both the email and the IP:

```php
// app/Providers/AppServiceProvider.php
use Illuminate\Cache\RateLimiting\Limit;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\RateLimiter;

public function boot(): void
{
    RateLimiter::for('login', function (Request $request) {
        return Limit::perMinute(5)->by($request->input('email').'|'.$request->ip());
    });
}
```

Then apply it to the route:

```php
Route::post('/login', LoginController::class)->middleware('throttle:login');
```
