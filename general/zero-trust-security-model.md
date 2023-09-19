---
tags: security, authentication
---

# Zero Trust security model

Zero Trust is a security model that **assumes the worst-case scenario** and protects resources with that expectation. Zero Trust assumes breach at the outset and then verifies each request as though it originated from an uncontrolled network.

Three principles:

- **Verify explicitly**: Always authenticate and authorize based on all available data points.
- **Follow [[principle-of-least-privilege]]**: Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection.
- **Assume breach**: Minimize blast radius and segment access. Verify end-to-end encryption. Use analytics to get visibility, drive threat detection, and improve defences.

While on older approaches, a device was considered secure when it was connected to a corporate network, the Zero Trust security model grants access to a user based on authenticated requests rather than the connection type.
