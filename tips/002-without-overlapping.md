# Stop scheduled jobs from piling up

If a scheduled command can take longer than its interval, a second copy will start before the first one finishes. Add `withoutOverlapping()`:

```php
// routes/console.php
use Illuminate\Support\Facades\Schedule;

Schedule::command('passes:sync')
    ->everyFiveMinutes()
    ->withoutOverlapping();
```

On multi-server setups, add `->onOneServer()` too (requires a shared cache driver like Redis or database).
