---
title: Docker deployment using Bitbucket Pipelines and Heroku
tags: [docker, deployment]
---

Set `HEROKU_TOKEN` and `APP_NAME` at `Settings -> Pipelines -> Environment variables`.

bitbucket-pipelines.yml

{% gist jincod/04bc7c402720d3d8472fbb094c4741bc bitbucket-pipelines.yml %}

deploy.sh

{% gist jincod/04bc7c402720d3d8472fbb094c4741bc deploy.sh %}