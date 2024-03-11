---
tags: csharp, async
---

# CPU-bound operations

An example of CPU-bound code is such as performing an expensive calculation.

For CPU-bound code, you await an operation that is started on a background thread with the Task.Run method.

For example, you can use

```cs
var damageResult = await Task.Run(() => CalculateDamageDone());
```

If the work you have is CPU-bound and you care about responsiveness, use async and await, but spawn off the work on another thread with Task.Run.

If the work is appropriate for concurrency and parallelism, also consider using the Task Parallel Library.
