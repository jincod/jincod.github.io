---
title: Express.js route builder from controllers
tags: [nodejs, expressjs, routing]
redirect_from: /post/116040161750
---
App structure:

```
.
├── index.coffee
└── server
    ├── controllers
        └── api.coffee
        └── user.coffee
    └── router.coffee
    └── app.coffee
```

api.coffee:

```
express = require 'express'

router = express.Router()

test = (req, res, next) -> res.sendStatus 200
add = (req, res, next) -> res.sendStatus 200

router.get '/test', test
router.post '/add', add

module.exports = router
```

Read all route info from ```controllers``` and build app routes:

{% gist jincod/16c7bec5d8c44431a142 %}

[Example source](https://github.com/jincod/expressjs-router-example)