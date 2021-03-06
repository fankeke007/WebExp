# 严格模式

es6 对严格模式做了一点修改，规定只要函数参数使用了默认值、解构赋值、或者**扩展运算符**，那么函数内部就不能显示设定为严格模式，否则会报错。

这样规定的原因是，函数内部的严格模式，同时适用于函数体和函数参数。但是，函数执行的时候，先执行函数参数，然后再是函数体。这样就有一个不合理的地方，只有从函数体之中，才能知道参数是否应该以严格模式执行，但是参数却应该优先于函数体执行。

规避这种限制的两个方法：

* 设定全局严格模式
* 把函数包在一个无参数的立即执行函数里面

```javascript
//方法一
'use strict';

function doSomething(a, b = a) {
  // code
}

//方法二
const doSomething = (function () {
  'use strict';
  return function(value = 42) {
    return value;
  };
}());
```



