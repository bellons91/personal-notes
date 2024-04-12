---
tags: architecture
---

# Sidecar pattern

Sidecar pattern is an architectural design where you add a service that runs in the background and performs some operations, removing the computational weight from the main application.

Examples of sidecar containers include:

- An agent that reads logs from the primary app container on a shared volume and forwards them to a logging service.
-A background process that refreshes a cache used by the primary app container in a shared volume.
