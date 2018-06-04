# 属性名表达式

js 定义对象的属性，有两种方法

```javascript
//方法一：字节用标识符作为属性名
obj.foo = 'haha';

//方法二：用表达式作属性名(或方法名)
obj['a'+'bc'] = 123;
```

若在对象字面量中定义定义对象属性，es5 中只能使用方法一，es6 中两种方法皆可。

```javascript
let propkey = 'hello';
let obj = {
    [propkey]:true,
    ['a'+'bc'] = 123
}
```

{% hint style="warning" %}
使用表达式属性名的一些注意事项：

1.属性名表达式与简洁表示法不能同时使用，会报错

2.属性名表达式若是一个对象，默认情况下会自动将对象转为字符串\[object Object\]，因此若有多个对象作为属性名，最后的会覆盖前面的。
{% endhint %}

