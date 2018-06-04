# 方法的name属性

函数的name属性，返回函数名。对象方法也是函数，因此也有name属性。

若对象的方法使用了**取值函数（getter \)**或**存值函数 \(setter）**，则name属性不是在该方法上面，而是**该方法的属性的描述对象的get和set属性上面**，返回值是方法名前加上 get 或 set 。

```javascript
const obj = {
    get foo(){},
    set foo(){}
};

obj.foo.name;//TypeError:Cannot read property 'name' of undefined
const descriptor = Object.getOwnPropertyDescriptor(obj,'foo');

descriptor.get.name // "get foo"
descriptor.set.name // "set foo"
```

{% hint style="warning" %}
两种特殊的情况

1. bind 方法创造的函数，name属性返回bound加上原函数的名字
2. Function构造函数创造的函数，name属性返回anonymous
3. 若对象方法是一个Symbol值，那么name属性返回的是这个Symbol值的描述
{% endhint %}

```javascript
const key1 = Symbol('description');
const key2 = Symbol();
let obj = {
    [key1](){},
    [key2](){}
};
obj[key1].name //"[description]"
obj[key2].name //''
```

