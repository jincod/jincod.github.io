---
title: Using private connectionString in Web.config
tags: [aspnetmvc]
redirect_from: /post/103641036910
---
Web.config:

```xml
<connectionStrings configSource="connectionStrings.config"/>
```

connectionStrings.config:

```xml
<connectionStrings>
  <add name="Main" connectionString="localhost" />
</connectionStrings>`
```

.gitignore:

```
connectionStrings.config
```