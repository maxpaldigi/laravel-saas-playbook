# Let models clean up after themselves

Logs, scan events and expired tokens grow forever unless you delete them. Use the `Prunable` trait:

```php
use Illuminate\Database\Eloquent\Builder;
use Illuminate\Database\Eloquent\Prunable;

class ScanEvent extends Model
{
    use Prunable;

    public function prunable(): Builder
    {
        return static::where('created_at', '<=', now()->subMonths(6));
    }
}
```

Then schedule it once a day:

```php
Schedule::command('model:prune')->daily();
```
