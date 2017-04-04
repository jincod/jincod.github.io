---
title: Automation deployment process using Powershell and Psake
tags: [powershell, psake, msbuild]
redirect_from: /post/113769159110
---
## Setup

```bash
git clone https://github.com/jincod/build-scripts.git
```

Change your solution name in *scripts\build-scenario.ps1*:

```powershell
properties {
  $Solution = "$ProjectDir\YourSolution.sln"
}
```

## Usage

Build all:

```bash
build.cmd
```

Only clean:

```bash
build.cmd clean
```

## Added tasks

```powershell
task Tests -depends Init {
  $tests = (Get-ChildItem $OutDir -Recurse -Include *Tests.dll)
  exec { & $nunit /noshadow /framework:"net-4.0" /xml:"$OutDir\Tests.nunit.xml" $tests }
}
```

### Call from build step TeamCity

![build-step](https://40.media.tumblr.com/35d2947618c91e087ee39a2c5b8c17fd/tumblr_nlaltxnZL31qaxpewo1_r1_1280.png)

### Github

[https://github.com/jincod/build-scripts](https://github.com/jincod/build-scripts)