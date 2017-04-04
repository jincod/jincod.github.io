---
title: Run Psake tasks on TeamCity
tags: [teamcity, psake, powershell, nuget]
redirect_from: /post/83628878065
---
### File tree:

```
.
├── build.cmd
└── Scripts
    ├── default.ps1
    └── NuGet.exe
```

### build.cmd

{% gist jincod/11222592 %}

### Using:

```
build.cmd taskName
```