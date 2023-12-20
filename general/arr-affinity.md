---
type: basic-note
foam_template:
  filepath: './general/arr-affinity.md'
tags: 
---

# ARR Affinity

Application Request Routing (ARR) for IIS 7 and above is a proxy-based routing module that forwards HTTP requests to application servers based on HTTP headers, server variables, and load balance algorithms.

ARR cleverly identifies the user by assigning them a special cookie (known as an *affinity cookie*), which allows the service to choose the right instance the user was using to serve subsequent requests made by that user. This means, a client establishes a session with an instance and it will keep talking to the same instance until his session has expired.

[Configure ARRAffinity cookie when accessing Azure App Service behind Azure Application Gateway](https://techcommunity.microsoft.com/t5/apps-on-azure-blog/configure-arraffinity-cookie-when-accessing-azure-app-service/ba-p/3842511)

[Disable Session affinity cookie (ARR cookie) for Azure web apps](https://azure.github.io/AppService/2016/05/16/Disable-Session-affinity-cookie-(ARR-cookie)-for-Azure-web-apps.html)

[Application Request Routing Version 2 Overview](https://learn.microsoft.com/en-us/iis/extensions/planning-for-arr/application-request-routing-version-2-overview)
