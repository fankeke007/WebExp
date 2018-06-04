# 属性的简洁表示法

es6 允许直接写入变量和函数，作为对象的属性和方法，使得书写更为简洁。

```javascript
const foo = 'bar';
const baz = {foo};
baz // {foo:'bar'}

//等同于
const baz = {foo:foo};
```

{% hint style="info" %}
直接写入变量和函数的前提条件是：属性名和变量名相同。
{% endhint %}

```javascript
function f(x,y){
    return {x,y};
}
//等同于
function f(x,y){
    return {x:x,y:y};
}
f(1,2) // Object {x:1,y:2}
```

```javascript
//除了属性简写，方法也可以简写
const o = {
    method(){
        return "hello";
    }
};
//等同于
const o = {
    method:function(){
        return "hello";
    }
}
```

{% hint style="warning" %}
1. 简洁写法的属性名总是字符串
2. 若某个方法值是一个Generator函数，前面需加上星号
{% endhint %}



