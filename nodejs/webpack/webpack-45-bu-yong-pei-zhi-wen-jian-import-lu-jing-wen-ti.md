**webpack4.x 无配置文件版本**

webpack4.x 之所以可以无需配置文件运行是因为其进行了许多默认配置，因此若想无配置文件使用，必须遵守其默认配置格式。默认结构见[目录结构](#目录结构)

无配置版限定太死，无法灵活应对大型复杂项目，因而个人建议还是应该使用带配置文件版。

**package.json**

![](/assets/webpack4.15.1-package.json.png)

###### **目录结构**

![](/assets/webpack4.15.1-folders.png)

**index.js**

```js
import _ from 'loadsh'
// var _ = require('lodash');

function component(){
    var element = document.createElement('div');
    element.innerHTML = _.join(['Hello','Webpack'],' ');
    return element;
}
document.body.appendChild(component());
```

若使用 import \_ from 'lodash'，会报路径错误。使用require 不会。

import会在index.js同目录下查找![](/assets/20180706error.png)

