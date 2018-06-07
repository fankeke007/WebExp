# Proxy（代理器）

\#**需回头重捋每一种拦截用法与限制条件**

**1.概述**

Proxy用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种**“元编程”（meta programming）**，**即对编程语言进行编程**。

**Proxy可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写**。

es6 原生提供Proxy构造函数，用来生成Proxy实例。

```javascript
var proxy = new Proxy(target,handler);
//target：要拦截的目标对象
//handler：也是一个对象，用来定制拦截行为
```

```javascript
//同一个拦截器可以设置多个拦截操作
var handler = {
	//拦截属性访问
	get:function(target,name){
		if(name==='prototype'){
			return Object.prototype;
		}
		return 'Hello, '+name;
	},
	//拦截自身函数形式调用
	apply:function(target,thisBinding,args) {
		return args[0];
	},
	//拦截自身以构造函数形式调用
	construct:function(target,args){
		return {value:args[1]};
	}
}

var fproxy = new Proxy(function(x,y){
	return x+y;
},handler);

fproxy(1,2) // 1
new fproxy(1,2) // {value:2}
fproxy.prototype === Object.prototype //true
fproxy.foo // 'Hello, foo'
```

{% hint style="info" %}
**Proxy 支持拦截操作一览**（共13种）

1. **get\(target,propkey,receiver\)**：拦截对象属性的读取，比如proxy.foo和proxy\['foo'\]
2. **set\(target,propKey,value,receiver\)**：拦截对象的属性设置，如proxy.foo = v，返回一个Boolean值
3. **has\(target,propKey\)**：拦截propKey in proxy的操作，返回一个Boolean值
4. **deleteProperty\(target,propKey\)**：拦截delete proxy\[propKey\]的操作，返回一个Boolean值
5. **ownKeys\(target\)**：拦截Object.getOwnPropertyNames\(proxy\)、Object.getOwnPropertySymbols\(proxy\)、Object.keys\(proxy\)、for...in循环，返回一个数组。该方法返回目标对象所有自身的属性的属性名，而Object.keys\(\)返回结果只包含自身可枚举属性名
6. **getOwnPropertyDescriptor\(target,propKey\)**：拦截Object.getOwnPropertyDescriptor\(proxy,propKey\),返回属性的描述对象
7. **defineProperty\(target,propKey,propDesc\)**：拦截Object.defineProperty\(proxy,propKey,propDesc\)、Object.defineProperties\(proxy,propDescs\)，返回一个Boolean值
8. **preventExtensions\(target\)**：拦截Object.preventExtensions\(proxy\)，返回一个Boolean
9. **getPrototypeOf\(target\)**：拦截Object.getPrototypeOf\(proxy\),返回一个Boolean
10. **isExtensible\(target\)**：拦截Object.isExtensible\(proxy\)，返回Boolean
11. **setPrototypeOf\(target,proto\)**：拦截Object.setPrototypeOf\(proxy,proto\)，返回一个Boolean，若目标对象是函数，那么还有两种额外操作可以拦截，如下。
12. **apply\(target,object,args\)**：拦截Proxy实例作为函数调用的操作，如proxy\(...args\)、proxy.call\(**object**,...args\)、proxy.apply\(...\)
13. **construct\(target,args\)**：拦截Proxy 实例作为构造函数调用操作，如new proxy\(...args\)

参数解释：

* target：目标对象
* propKey：属性名
* receiver：proxy 实例本身 **\[可选\]**
{% endhint %}





