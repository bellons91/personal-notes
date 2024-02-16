---
tags: csharp, async
---

# IO-bound operations

If you have any I/O-bound needs (such as requesting data from a network, accessing a database, or reading and writing to a file system), you'll want to utilize asynchronous programming.

For I/O-bound code, you await an operation that returns a `Task` or `Task<T>` inside of an async method.

If the work you have is I/O-bound, use async and await without Task.Run. You should **not** use the Task Parallel Library.