---
title: Deploy to surge.sh from appveyor
tags: [surge, appveyor]
redirect_from: /post/146117898810
---

Appveyor.yml

```yaml
environment:
  SURGE_LOGIN: login
  SURGE_TOKEN:
    secure: secure-string
install:
  - ps: Install-Product node 0
  - npm install -g npm
  - npm install
build: off
build_script:
  - npm run build
deploy_script:
  - npm run deploy
```

Scripts section in package.json

```json
"scripts": {
  "build": "webpack --config webpack.config.js",
  "deploy": "surge --project ./dist --domain domain.surge.sh"
}
```