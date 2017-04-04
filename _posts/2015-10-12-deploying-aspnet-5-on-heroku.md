---
title: Deploying asp.net 5 on heroku
tags: []
redirect_from: /post/131004166948
---
# Deprecated

New version: [Deploying ASP.NET Core on heroku](https://jincod.tumblr.com/post/152290263970/deploying-aspnet-core-on-heroku)

<hr>
[jincod/dotnet-buildpack](https://github.com/jincod/dotnet-buildpack) forked from: [heroku/dotnet-buildpack](https://github.com/heroku/dotnet-buildpack)

```bash
heroku buildpacks:set https://github.com/jincod/dotnet-buildpack
```

[AspNet5 Demo App](https://github.com/jincod/AspNet5DemoApp)

```bash
git clone https://github.com/jincod/AspNet5DemoApp.git
git push origin master
```

### Deploy to Heroku

Click the button below to set up this sample app on Heroku:

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/jincod/AspNet5DemoApp)
