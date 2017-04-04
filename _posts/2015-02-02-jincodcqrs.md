---
title: Jincod.CQRS
tags: [Jincod.CQRS, CQRS]
redirect_from: /post/109872929635
---
Interfaces for for develop app using CQRS principle

### Installation

Available on [NuGet](https://www.nuget.org/packages/Jincod.CQRS)

```powershell
PM>Install-Package Jincod.CQRS
```
### Query

QueryContext

```csharp
public class SimpleQueryContext : IQueryContext<SimpleEntity>
{
}
```

Query

```csharp
public class SimpleQuery : IQuery<SimpleQueryContext, SimpleEntity>
{
    public SimpleEntity Execute(SimpleQueryContext queryContext)
    {
        return new SimpleEntity {Name = "Simpl1"};
    }
}
```

QueryProcessor

```csharp
var queryProcessor = container.Resolve<IQueryProcessor>();
var context = new SimpleQueryContext();
SimpleEntity simpleEntity = queryProcessor.Process<SimpleEntity, SimpleQueryContext>(context);
```

### Commands

Command

```csharp
public class SimpleCommand : ICommand
{
}
```

CommandHandler

```csharp
public class SimpleCommandHandler : ICommandHandler<SimpleCommand>
{
    public void Handle(SimpleCommand command)
    {
        // do something
    }
}
```

CommandProcessor

```csharp
var commandProcessor = container.Resolve<ICommandProcessor>();
var simpleCommand = new SimpleCommand();
commandProcessor.Process(simpleCommand);
```

### Source code available on github

[Jincod.CQRS](https://github.com/jincod/Jincod.CQRS)