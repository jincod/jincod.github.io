---
title: Knockout mapping hacks
tags: [javascript, knockout, knockout-mapping]
redirect_from: /post/124133490245
---
### Problem

Some fields defined in **viewModel** but missed in **data** will be lost after using ko.mapping.

### View model definition

```javascript
var viewModel = {
  id: ko.observable(),
  name: ko.observable("name"),
  items: ko.observableArray()
};
var data = {
    id: 1,
    items: [{text: "text", value: "value"}]
};
ko.mapping.fromJS(data, {}, viewModel);
console.log(ko.mapping.toJSON(viewModel));
```

### Result

```json
{"id":1,"items":[{"text":"text","value":"value"}]}
```

'name' field was missing.

```javascript
var data = {
    id: 1,
    items: [{text: "text", value: "value"}]
};
ko.mapping.fromJS(data, {include: Object.keys(viewModel)}, viewModel);
console.log(ko.mapping.toJSON(viewModel));
```

### Result

```json
{"id":1,"name":"name","items":[{"text":"text","value":"value"}]}
```

Get correct viewModel after mapping.

### Solution

```javascript
var maping = {
  include: Object.keys(viewModel)
};
ko.mapping.fromJS(data, mapping, viewModel);
```

[https://jsfiddle.net/cvdex801/](https://jsfiddle.net/cvdex801/)