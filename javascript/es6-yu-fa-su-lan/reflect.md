# Reflect

1.概述

Reflect 对象与 Proxy 对象一样，也是es6 **为了操作对象而提供的新API**。

{% hint style="info" %}
Reflect 对象设计的目的，有如下几个：

1. **将Object对象的一些明显属于语言内部的方法（如Object.defineProperty），放到Reflect对象上**。现阶段这些方法同时在Object和Reflect对象上部署，未来的新方法将只在Reflect上部署。也就是说可以通过Reflect对象拿到语言内部的方法。
2. **修改某些Object方法的返回结果，让其变得合理**。如Object.defineProperty\(obj,name,desc\)在无法定义属性时，会抛出一个错误，而Reflect.defineProperty\(obj,name,desc\)则返回false。
3. **让Object操作都变成函数行为**。某些Object操作是命令式，比如name  in  obj 和delete obj\[name\]，而Reflect.has\(obj,name\) 和 Reflect.deleteProperty\(obj,name\)
4. Reflect 对象的方法和Proxy 对象的方法一一对应，只要是Proxy对象的方法，就能在Reflect对象上找到对应的方法。这就让Proxy对象可以很方便地调用对应的Reflect方法，完成默认行为，作为修改行为的基础。**也就是，不管Proxy怎么修改默认行为，你总可以在Reflect上获取默认行为**。
{% endhint %}

```javascript
//一些例子

// 老写法
'assign' in Object // true
// 新写法
Reflect.has(Object, 'assign') // true

//Proxy 和 Reflect
Proxy(target, {
  set: function(target, name, value, receiver) {
    var success = Reflect.set(target,name, value, receiver);
    if (success) {
      log('property ' + name + ' on ' + target + ' set to ' + value);
    }
    return success;
  }
});

var loggedObj = new Proxy(obj, {
  get(target, name) {
    console.log('get', target, name);
    return Reflect.get(target, name);
  },
  deleteProperty(target, name) {
    console.log('delete' + name);
    return Reflect.deleteProperty(target, name);
  },
  has(target, name) {
    console.log('has' + name);
    return Reflect.has(target, name);
  }
});

// 老写法
Function.prototype.apply.call(Math.floor, undefined, [1.75]) // 1

// 新写法
Reflect.apply(Math.floor, undefined, [1.75]) // 1
```

{% hint style="info" %}
Reflect 静态方法汇总

1. **Reflect.apply\(target , thisArg , args\)**
2. **Reflect.construct\(target,args\)**
3. Reflect.get\(target,name,receiver\)
4. Reflect.set\(target,name,value,reciver\)
5. Reflect.defineProperty\(target,name,desc\)
6. 
{% endhint %}

