# Make payment webhooks idempotent

Stripe and most payment providers retry webhooks, so the same event can arrive more than once. If your handler isn't idempotent, a customer can be credited twice.

Store each event ID with a unique index and skip anything you've already seen:

```php
// migration
$table->string('event_id')->unique();

// webhook controller
$created = ProcessedWebhook::firstOrCreate(['event_id' => $event->id]);

if (! $created->wasRecentlyCreated) {
    return response()->noContent(); // already handled
}

// ...handle the event
```

Return a 2xx quickly and move slow work onto a queued job, so the provider doesn't time out and retry.
