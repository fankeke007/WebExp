# super关键字

this关键字总是指向函数所在的当前对象，es6新增了另一个类似的关键字super，指向当前对象的原型对象。

```javascript
const proto = {
    foo:'hello'
};
const obj = {
    foo:'world',
    //这里若换成find:function(){...}则会报错
    find(){          
        return super.foo;
    }
};
Object.setPrototypeOf(obj,proto);
obj.find();
```

{% hint style="danger" %}
super关键字表示原型对象时，只能用在对象的方法之中，用在其他地方会报错。

以下三种super用法会报错：

```javascript
// 报错
const obj = {
  foo: super.foo
}

// 报错
const obj = {
  foo: () => super.foo
}

// 报错
const obj = {
  foo: function () {
    return super.foo
  }
}
```

因为对于 JavaScript 引擎来说，这里的super都没有用在对象的方法之中。第一种写法是super用在属性里面，第二种和第三种写法是super用在一个函数里面，然后赋值给foo属性。**目前，只有对象方法的简写法可以让 JavaScript 引擎确认，定义的是对象的方法**。
{% endhint %}



