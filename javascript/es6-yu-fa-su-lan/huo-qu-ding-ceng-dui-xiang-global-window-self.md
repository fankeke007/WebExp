---
description: 获取顶层对象的同用方法
---

# 获取顶层对象（global / window / self）

1.**顶层对象属性**

顶层对象，在浏览器环境中是指 window 对象，在 node 指的是 global 对象。**在 es5 中，顶层对象属性与全局变量是等价的**。

{% hint style="info" %}
> 顶层对象的属性和全局变量挂钩，被认为是JavaScript语言最大的设计败笔之一。es6 为了改变这一点，一方面规定，为了保持兼容性，var 和 function 声明的全局变量依旧是顶层对象的属性；另一方面，let、const 声明的全局变量，不属于顶层对象的属性。也就是从es6开始全局变量将逐步与顶层对象的属性脱钩。
{% endhint %}

```javascript
var a = 1;
//若在node环境可以写成global.a
//或者采用更通用的写法：this.a
window.a; // 1

let b = 5;
window.b; //undefiend
window.b = 3;
window.b; //3
b; // 5  ,let 声明的全局变量将不再是顶层对象的属性
```

**2.获取 global 对象**

es5 的顶层对象，本身也是一个问题，因为他在各种实现里面不统一：

* 浏览器里面，顶层对象是 **window** ，但 **Node** 和 **web worker** 没有 window。
* 浏览器和web worker 里，self 是指向顶层对象，但 node 没有self。
* Node 里面，顶层对象是 global，但其他环境都不支持。

同一段代码为了能够在各种环境，都能渠道顶层对象，现在一般是使用 **this** 对象，但是有局限性：

* 全局环境中，this 会返回顶层对象，但是 Node 木块和 es6 中，this 返回当前模块。
*  函数里面的this，若函数不做对象方法运行，而是单纯作为函数运行，this 会指向顶层对象。但是在严格模式下，this 会返回 undefined。
* 不管是严格模式还是普通模式，new Function\(' return this '\)\(\),总会返回全局对象，但是浏览器若启用了CSP（内容安全策略），那么eval 和 new Function这些方法可能无法使用。

两种折中的在所有环境下获取全局（顶层）对象的方法：

```javascript
//方法一
(typeof window !== 'undefined' 
    ? window 
    : (typeof process === 'object' && typeof require === 'function' && typeof global ==='object')
        ? global
        : this);

//方法二
var getGlobal = function(){
    if( typeof self!== 'undefined' ){ return self;}
    if( typeof window !== 'undefined' ){ return window;}
    if( typeof global !== 'undefined' ){ return global;}
    throw new Error('unable to locate global object');
}
```

