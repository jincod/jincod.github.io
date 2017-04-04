---
title: Integrate ASP.NET 5 and Webpack with Hot Module Replacement plugin
tags: [aspnet5, npm, webpack, hotmodulereplacement]
redirect_from: /post/135043543538
---

Every app runs in at least two environments: production and development.

This post is about the separation of the environment configs using [Webpack](https://webpack.github.io/) and [ASP.NET 5](http://www.asp.net/vnext).

## Webpack

Add two configs:

- webpack.config.dev.js
- webpack.config.prod.js

`webpack.config.dev.js` contains [Hot Module Replacement](https://webpack.github.io/docs/hot-module-replacement.html) in plugins section:

```json
plugins: [
  new webpack.HotModuleReplacementPlugin()
]
```

In `webpack.config.prod.js` plugins section contains `ExtractTextPlugin` and `UglifyJsPlugin`:

```json
plugins: [
  ...

  new webpack.optimize.UglifyJsPlugin({
  compressor: {
    warnings: false
  }
  }),
  new ExtractTextPlugin('styles.css')
]
```

## Evironment Tag Helpers

Use [Evironment Tag Helpers](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNet.Mvc.TagHelpers/EnvironmentTagHelper.cs) to switch between development and production environment in `Layout.cshtml` add:

```html
@addTagHelper "*, Microsoft.AspNet.Mvc.TagHelpers"

...

<environment names="Production">
  <link rel="stylesheet" href="/styles.css">
</environment>

...

<environment names="Development">
  <script src="http://localhost:3000/bundle.js"></script>
</environment>
<environment names="Production">
  <script src="/bundle.js"></script>
</environment>
```html

in `project.json` add:

```json
"dependencies": {
  "Microsoft.AspNet.Mvc.TagHelpers": "6.0.0-rc1-final"
}
```

## Development

Run webpack dev server:

```bash
npm i
npm run build
```

Run ASP.NET project:

```bash
dnx --project src\AspNet5DemoApp dev
```

## Production

Add property `postrestore` project.json for install npm modules from package.json

```json
"scripts": {
  "postrestore": ["cd ../.. && npm i && cd src/AspNet5DemoApp"]
}
```

In `package.json` add property `postinstall` to `scripts` section:

```json
"scripts": {
  "build": "webpack",
  "postinstall": "if [ \"$NODE_ENV\" = production ]; then npm run build; fi"
}
```

`postinstall` command run after the package is uninstalled if environment is production (`NODE_ENV=production`).

## Links

- [Source](https://github.com/jincod/AspNet5DemoApp)
- [Demo](https://aspnet5demoapp.herokuapp.com/)
