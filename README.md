# sbxcorejs

Welcome, this repo is a friendly implementation of [sbx-querybuilder](https://github.com/sbxcloud/sbx-querybuilder) library.

### Initialization

This library has a class names Find, this class need 3 params to initialize: 

| Name | Type | Description |
| ------ | ------ | ------ |
| model | String | Model name of sbx model. |
| isFind | Boolean | true for find and false for delete |
| domain | Integer | domain id |

Note:\s\s
For every examples we gonna use model audit:

| Name | Type |
| ------ | ------ |
| action | String |
| user | Reference |
| date | Date |

Now, the simplest way to use it.

```
// Nodejs:
const Find = require("sbxcorejs").Find;

// Javascript:
import { Find } from 'sbxcorejs';

const find = new Find('audit', true, 96);

console.log(find.query.compile());
/*
  { page: 1, size: 1000, where: [], domain: 96, row_model: 'audit' }
*/
```


