---
title: Ensure https for ASP.NET Core apps on Heroku
tags: [aspnetcore, heroku]
---

Update `ConfigureServices` method with:

{% gist jincod/5d1cec864da231f60611daf20a9ac75f StartupConfigureService.cs %}

Update `Configure` method with:

{% gist jincod/5d1cec864da231f60611daf20a9ac75f StartupConfigure.cs %}

More info

- [Docs](https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/proxy-load-balancer)
- [Heroku Routing](https://devcenter.heroku.com/articles/http-routing)
