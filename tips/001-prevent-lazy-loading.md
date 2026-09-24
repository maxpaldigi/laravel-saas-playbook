# Catch N+1 queries before they reach production

Turn lazy loading into an exception in local and staging, so N+1 queries fail loudly while you develop.

```php
// app/Providers/AppServiceProvider.php
use Illuminate\Database\Eloquent\Model;

public function boot(): void
{
    Model::preventLazyLoading(! app()->isProduction());
}
```

In production it stays silent, so a missed `with()` never breaks a customer's page.
