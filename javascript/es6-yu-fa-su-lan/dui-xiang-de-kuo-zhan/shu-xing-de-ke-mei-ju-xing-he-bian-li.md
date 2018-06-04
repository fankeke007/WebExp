# 属性的可枚举性和遍历

**1.可枚举性**

Object.getOwnPropertyDescriptor\(\)方法返回指定对象上一个**自有属性**的属性描述符（或叫属性描述对象）。属性描述对象的enumerable属性称为“可枚举性”，若该属性为false，就表示某些操作会忽略当前属性。

{% hint style="info" %}
**会忽略enumerable为false的四个操作**：

1. for...in 循环：遍历对象自身和继承的可枚举属性
2. Object.keys\(\)：返回对象自身的所有可枚举的属性名
3. JSON.stringify\(\)：只串行化自身的可枚举的属性
4. Object.assign\(\)：忽略enumerable为false的属性，只拷贝对象自身的可枚举属性

前3个es5 就有，第四个为 es6 新增方法。
{% endhint %}

{% hint style="danger" %}
es6 规定：所有Class的原型方法都是不可枚举的

```javascript
Object.getOwnPropertyDesctiptor(class {foo(){}}.prototype,'foo').enumerable;
//false
```
{% endhint %}

{% hint style="info" %}
总的来说，操作中引入继承的属性会让问题复杂化，大多数时候，我们只关心对象自身的属性。所以，**尽量不要用for...in循环，而用Object.kyes\(\)**.
{% endhint %}

**2.属性的遍历**

es6 一共有5中方法可以遍历对象的属性：

1. **for...in** ：**自身或继承**的可枚举属性，不含Symbol属性
2. **Object.keys\(\)**：返回**自身可枚举属性名数组**，不含Symbol
3. **Object.getOwnPropertyNames\(obj\)**：不含Symbol，但是包含不可枚举属性
4. Object.getOwnPropertySymbols\(obj\)：返回对象自身所有Symbol属性的键名
5. Reflect.ownKeys\(obj\)：返回对象自身所有键名（不管是否可枚举，是否Symbol）

{% hint style="info" %}
以上5中方法遍历对象的键名，都遵守共同的属性遍历的次序规则：

* 首先遍历所有的数值键，按照数值升序排列
* 其次遍历所有字符串键，按照加入时间升序排列
* 最后遍历所有的Symbol键，按照加入时间升序排列

```javascript
Reflect.ownkeys({[Symbol()]:0,b:0,10:0,2:0,a:0})
//['2','10','b','a',Symbol()]
```
{% endhint %}



