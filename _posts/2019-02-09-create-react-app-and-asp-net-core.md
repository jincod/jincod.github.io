---
title: Using Create React App with ASP.NET Core
tags: [reactjs, aspnetcore]
---

Make sure you have already set ASP.NET Core app ([Getting Started](https://dotnet.microsoft.com/learn/web/aspnet-hello-world-tutorial/intro)) and React.js app ([Getting Started](https://facebook.github.io/create-react-app/docs/getting-started))

To use ASP.NET Core API from React.js app add option `proxy` to `package.json`

```json
...
"proxy":"http://localhost:5000"
...
```

This option allow to proxy requests starts with `/api` to your API server (ASP.NET Core app).

More info about proxy option [Proxying API Requests in Development](https://facebook.github.io/create-react-app/docs/proxying-api-requests-in-development)

Start your apps

```bash
dotnet run
npm start
```

Full example of this approach [AspNetCoreDemoApp](https://github.com/jincod/AspNetCoreDemoApp)
