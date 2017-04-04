---
title: Using ElasticSearch witn NEST client
tags: [NEST, elasticsearch]
redirect_from: /post/109469107265
---
Using NEST for create mapping and search Products and Categories.

### Model for ElasticSearch index:

```csharp
public class ProductIndex
{
    public string Id { get; set; }
    public string CategoryId { get; set; }
    public Dictionary<string, object> Params { get; set; }
}
```

### Method for create mapping for ProductIndex:

```csharp
var indexDefinition = new RootObjectMapping
{
    Properties = new Dictionary<PropertyNameMarker, IElasticType>()
};

var paramsProperty = new ObjectMapping
{
    Properties = new Dictionary<PropertyNameMarker, IElasticType>()
};

var numberMapping = new NumberMapping();
var boolMapping = new BooleanMapping();
var stringMapping = new StringMapping
{
    Index = FieldIndexOption.NotAnalyzed
};

IEnumerable<object> properties = GetAllProperties();
foreach (var property in properties)
{
    switch (property.DataType)
    {
        case DataType.Logic:
            paramsProperty.Properties.Add(property.Id, boolMapping);
            break;
        case DataType.Numeric:
            paramsProperty.Properties.Add(property.Id, numberMapping);
            break;
        case DataType.Text:
            paramsProperty.Properties.Add(property.Id, stringMapping);
            break;
    }
}

indexDefinition.Properties.Add(Property.Name<ProductIndex>(p => p.Params), paramsProperty);
indexDefinition.Properties.Add(Property.Name<ProductIndex>(p => p.Id), stringMapping);
indexDefinition.Properties.Add(Property.Name<ProductIndex>(p => p.CategoryId), stringMapping);

_client.Map<ProductIndex>(x => x.InitializeUsing(indexDefinition));
```

### Method for search:

#### Build FilterContainer:

```csharp
FilterContainer filterContainer = BuildParamsFilter(filters);
```

#### Create search request:

```csharp
var request = new SearchRequest
{
    Size = 0,
    Aggregations = new Dictionary<string, IAggregationContainer>
    {
        {
            "agg", new AggregationContainer
            {
                Filter = new FilterAggregator
                {
                    Filter = filterContainer
                },
                Aggregations = new Dictionary<string, IAggregationContainer>
                {
                    {
                        "categoryId", new AggregationContainer
                        {
                            Terms = new TermsAggregator
                            {
                                Size = 0,
                                Field =
                                    Property.Path<ProductIndex>(p => p.CategoryId)
                            }
                        }
                    }
                }
            }
        }
    }
};
```

#### Execute query and return result category ids:

```csharp
ISearchResponse<ProductIndex> result = _client.Search<ProductIndex>(request);

SingleBucket filterAgg = result.Aggs.Filter("agg");
if (filterAgg != null)
{
    IEnumerable<string> categoryIds =
        filterAgg.Terms("categoryId").Items
            .Select(item => item.Key)
            .ToList();
    return categoryIds;
}
```

Source code available on [github](https://github.com/jincod/SearchServiceExample)