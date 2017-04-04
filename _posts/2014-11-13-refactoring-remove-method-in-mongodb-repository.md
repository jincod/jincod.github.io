---
title: Refactoring Remove method in MongoDb Repository
tags: [mongodb, csharp]
redirect_from: /post/102518998710
---
### First method

```csharp
public void RemoveById(Guid id)
{
  _collection.Remove(Query.EQ("_id", id));
}
```

Using:

```csharp
_repository.RemoveById(id);
```

Disadvantages:

- Grownup Repository class with `RemoveSomething()` methods
- Depends on string constants ("_id")

### Second method

```csharp
public void RemoveByQuery(IMongoQuery query)
{
  _collection.Remove(query);
}
```

Using:

```csharp
_repository.RemoveByQuery(Query.EQ("_id", id));
```

Disadvantages:

- Business logic depends on MongoDb Driver Queries (`Query.EQ("_id", id)`)
- Depends on string constants ("_id")

### Third method

```csharp
public void Remove<TValue>(Expression<Func<TEntity, TValue>> expression, TValue value)
{
  _collection.Remove(Query<TEntity>.EQ(expression, value));
}
```

Using:

```csharp
_repository.Remove(x => x.Id, id);
```

Disadvantages:

- Only eqaul condition (`Query.EQ`)

Advantages:

- Can use a lambda expression instead of string constants
- Clear Repository class

### Fourth method

```csharp
public void Remove(Expression<Func<TEntity, bool>> whereExpression)
{
  _collection.Remove(Query<TEntity>.Where(whereExpression));
}
```

Using:

```csharp
_repository.Remove(x => x.Id == id);
```

Advantages:

- Can use a lambda expression instead of string constants
- Clear Repository class
- Can use **any lambda** expression (`x => x.Id == id`)