---
tags: dapr, microservice
---

# Dapr

The Distributed Application Runtime (Dapr) is a set of incrementally adoptable features that simplify the authoring of distributed, microservice-based applications.

Dapr provides capabilities for enabling application intercommunication through messaging via pub/sub or reliable and secure service-to-service calls.

Dapr is often used to implement the [[sidecar-pattern]]. The main application communicates with the sidecar via [[gRPC]] or HTTP;

Dapr exposes several APIs:

- **Service-to-service invocation**: Discover services and perform reliable, direct service-to-service calls with automatic [[mTLS]] authentication and encryption.
- **State management**: Provides state management capabilities for transactions and CRUD operations.
- **Pub/sub**: Allows publisher and subscriber container apps to intercommunicate via an intermediary message broker.
- **Bindings**: Trigger your applications based on events
- **Actors**: Dapr actors are message-driven, single-threaded, units of work designed to quickly scale. For example, in burst-heavy workload situations.
- **Observability**: Send tracing information to an Application Insights backend.
- **Secrets**: Access secrets from your application code or reference secure values in your Dapr components.

![Dapr APIs](dapr-apis.png)

Dapr uses a modular design where functionality is delivered as a component.
