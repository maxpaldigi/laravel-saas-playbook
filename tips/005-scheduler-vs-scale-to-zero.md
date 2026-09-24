# Your scheduler can keep a serverless database awake

Serverless databases that scale to zero only save money when nothing talks to them. A task scheduled `everyMinute()` that touches the database wakes it up every minute, so it never sleeps and you pay for it around the clock.

- Ask whether each task really needs to run that often. Hourly or daily is usually enough.
- Group small jobs into one command instead of many frequent ones.
- Check your database's idle or compute graph after deploying scheduler changes.
