---
title: Jenkins integration with Jest
tags: [tests, jenkins]
---

We will use [Jest-junit](https://github.com/palmerj3/jest-junit) test reporter to integrate jest results with Jenkins.

## Installation

```bash
npm install -D jest jest-junit
```

## Configuration

Add to `package.json`:

```json
"scripts": {
  ...
  "test": "jest"
}
```

Add to `Jenkinsfile`:

```groovy
stage ('tests') {
  withEnv(["JEST_JUNIT_OUTPUT=./jest-test-results.xml"]) {
    sh 'npm test -- --ci --testResultsProcessor="jest-junit"'
  }
  junit 'jest-test-results.xml'
}
```
