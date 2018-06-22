# Coravel

Inspired by all the awesome features that are baked into the Laravel PHP framework - coravel seeks to provide additional features that .Net Core lacks like:

[x] Task Scheduling
[x] Queuing
[] Mailer
[] Command line tools integrated with coraval features
[] More???

## Sections

[Task Scheduling](https://jamesmh.github.io/coravel/Scheduling)
[Queuing](https://jamesmh.github.io/coravel/Queuing)

## Quick-Start

Add the nuget package `Coravel` to your .NET Core app. Done!

__Task Scheduling__: Tired of using cron and Windows Task Scheduler? Want to just use something easy that ties into your existing code?

In `Startup.cs`, put this in `ConfigureServices()`:

```c#
services.AddScheduler(scheduler =>
    {
        scheduler.Schedule(
            () => Console.WriteLine("Run at 1pm utc during week days.")
        )
        .DailyAt(13, 00);
        .Weekday();
    }
);
```

Easy enough? Look at the documentation to see what methods are available to you!

__Queing__: Tired of having to install other systems to get a queuing system to work? Tired of using databases to issue queued tasks?

In `Startup.cs`, put this in `ConfigureServices()`:

```c#
services.AddQueue();
```

Voila! Too hard?

To append to the queue, inject `IQueue` into your controller (or wherever injection occurs):

```c#
using Coravel.Queuing.Interfaces; // Don't forget this!

// Now inside your MVC Controller...
IQueue _queue;

public HomeController(IQueue queue) {
    this._queue = queue;
}
```

And then call:

```c#
this._queue.QueueTask(() =>
    Console.WriteLine("This was queued!")
);
```

Now you have a fully functional queue!