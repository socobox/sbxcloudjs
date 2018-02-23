# sbxcorejs

Welcome, this repo is a friendly implementation of [sbx-querybuilder](https://github.com/sbxcloud/sbx-querybuilder) library.

## Initialization
* * *

This library has a class names Find, this class need 3 params to initialize: 

| Name | Type | Description |
| ------ | ------ | ------ |
| model | String | Model name of sbx model. |
| isFind | Boolean | true for find and false for delete |
| domain | Integer | domain id |

### Note:
For every examples we gonna use model audit:

| Name | Type |
| ------ | ------ |
| action | String |
| user | Reference |
| consecutive | Integer |

### Now, the simplest way to use it.

```
// Nodejs:
const Find = require("sbxcorejs").Find;

// Javascript:
import { Find } from 'sbxcorejs';

const find = new Find('audit', true, 96);

// Pagination 
find.setPage(2); // default: 1
find.setPageSize(100); // default: 1000

console.log(find.query.compile());
/*
  { page: 2, size: 100, where: [], domain: 96, row_model: 'audit' }
*/
```

## Examples
* * *

### Function names and how to use it

With all attributes types we can use:
- andWhereIsEqual
- andWhereIsNull
- andWhereIsNotNull
- andWhereIsNotEqual
- orWhereIsEqual
- orWhereIsNull
- orWhereIsNotNull
- orWhereIsNotEqual

With References and String we can use:
- andWhereIn
- orWhereIn

With Strings and Text we can use:
- andWhereStartsWith
- andWhereEndsWith
- andWhereContains
- orWhereStartsWith
- orWhereEndsWith
- orWhereContains

With Integer, Float, Date we can use:
- andWhereGreaterThan
- andWhereLessThan
- andWhereGreaterOrEqualThan
- andWhereLessOrEqualThan
- orWhereGreaterThan
- orWhereLessThan
- orWhereGreaterOrEqualThan
- orWhereLessOrEqualThan

### All attributes usage

```
const Find = require("sbxcorejs").Find;
const find = new Find('audit', true, 96);

find.andWhereIsEqual('action', 'DEL')
    .orWhereIsEqual('action', 'GI')
    .andWhereIsNull('action')
    .orWhereIsNull('action')
    .andWhereIsNotNull('action')
    .orWhereIsNotNull('action')
    .andWhereIsNotEqual('action', 'DEL')
    .orWhereIsNotEqual('action', 'DEL');

find.query.compile();
```

### String and Text usage

```
const Find = require("sbxcorejs").Find;
const find = new Find('audit', true, 96);

find.andWhereStartsWith('action', 'DEL')
    .orWhereStartsWith('action', 'GI')
    .andWhereContains('action', 'DEL')
    .orWhereContains('action', 'GI')
    .andWhereEndsWith('action', 'DEL')
    .orWhereEndsWith('action', 'GI')
    .andWhereIn('action', ['DELETE', 'GIFT'])
    .orWhereIn('action', ['DELETE', 'GIFT']);

find.query.compile();
```

### Integer, Float and Date usage

```
const Find = require("sbxcorejs").Find;
const find = new Find('audit', true, 96);

find.andWhereGreaterThan('consecutive', 1)
    .orWhereGreaterThan('consecutive', 1)
    .andWhereLessThan('consecutive', 1000)
    .orWhereLessThan('consecutive', 1000)
    .andWhereGreaterOrEqualThan('consecutive', 1)
    .orWhereGreaterOrEqualThan('consecutive', 1)
    .andWhereLessOrEqualThan('consecutive', 1000)
    .orWhereLessOrEqualThan('consecutive', 1000);

find.query.compile();
```

### Note:

The find.query.compile() returns the body of the POST request to [sbxcloud](https://sbxcloud.com)