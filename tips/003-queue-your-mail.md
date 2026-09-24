# Never send email inside the request

Sending mail synchronously adds the mail provider's latency to your user's page load, and a provider outage becomes a 500 error. Queue it:

```php
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Mail\Mailable;

class WelcomeMail extends Mailable implements ShouldQueue
{
    // ...
}
```

Now `Mail::to($user)->send(new WelcomeMail)` is pushed onto the queue automatically.
