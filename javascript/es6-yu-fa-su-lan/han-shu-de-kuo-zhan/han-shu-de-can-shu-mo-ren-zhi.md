# 函数的参数默认值

es6 之前不能直接为函数指定默认参数，只能采用变通方法（babel转译也是用的变通的方法）。

```javascript
function log(x, y) {
  y = y || 'World';
  console.log(x, y);
}

log('Hello') // Hello World
log('Hello', 'China') // Hello China
log('Hello', '') // Hello World
```

{% hint style="danger" %}
变通做法的缺点：不能为默认值赋值false、空字符串等布尔值为假的值。得需先检测是否赋值（typeof y === 'undefiend'）,再进一步判断默认情况。
{% endhint %}

es6 直接在语法上支持函数默认参数

```javascript
function log(x, y = 'World') {
  console.log(x, y);
}

log('Hello') // Hello World
log('Hello', 'China') // Hello China
log('Hello', '') // Hello
```

{% hint style="info" %}
使用函数默认参数的一些注意事项

1. 参数变量是默认声明的，所以在函数内**不能用 let 或 const 再次声明**（会报错）。
2. **使用参数默认值时，函数不能有同名参数**。（不使用默认值时时允许的）
3. 参数默认值不是传的值，而是每次都重新计算默认值表达式的值。默认值是惰性求值的。
{% endhint %}

**与结构赋值默认值结合使用**

注意对比一下两者的区别

```javascript
//函数在调用时必须掺入一个对象，负责x,y没法结构，默认值失效
function foo({x, y = 5}) {
  console.log(x, y);
}

//传入默认结构对象，即使调用时不传入对象，也能真确使用默认值
function foo({x,y=5}={}){
  console.log(x,y);
}
```

结合以下两例加深理解

```javascript
//调用时必须传入第二个对象参数，不然报错
function fetch(url, { body = '', method = 'GET', headers = {} }) {
  console.log(method);
}
fetch('http://example.com', {})// "GET"
fetch('http://example.com')//报错

//给第二个参数提供默认结构对象，就可以调用时不用传入第二个参数而默认值生效
function fetch(url, { body = '', method = 'GET', headers = {} } = {}) {
  console.log(method);
}
fetch('http://example.com')// "GET"
```

再次对比一下两例，了解结构再函数参数默认值中的应用

```javascript
// 写法一
function m1({x = 0, y = 0} = {}) {
  return [x, y];
}

// 写法二
function m2({x, y} = { x: 0, y: 0 }) {
  return [x, y];
}

// 函数没有参数的情况
m1() // [0, 0]
m2() // [0, 0]

// x 和 y 都有值的情况
m1({x: 3, y: 8}) // [3, 8]
m2({x: 3, y: 8}) // [3, 8]

// x 有值，y 无值的情况
m1({x: 3}) // [3, 0]
m2({x: 3}) // [3, undefined]

// x 和 y 都无值的情况
m1({}) // [0, 0];
m2({}) // [undefined, undefined]

m1({z: 3}) // [0, 0]
m2({z: 3}) // [undefined, undefined]
```

{% hint style="info" %}
参数默认值的位置，尽管 es6 没做强制要求（任意位置都行），但是若果默认参数不位于最后，函数调用已然没法完全省略默认参数（得为其流出相应位置）。只是一种不好的实现，python中默认参数的写法值得借鉴（函数默认参数放在尾部）。
{% endhint %}

{% hint style="danger" %}
函数的**默认参数**不会体现在函数的length属性中，因而会导致length属性失真。（函数的length属性返回函数中参数的个数）。若默认参数不是尾参数，甚至会导致其后的正常参数也不计入length。

同样，rest参数（类似python 可变参数），也会导致length失真。
{% endhint %}

{% hint style="info" %}
默认参数的作用域规则

一旦设置参数的默认值，函数进行声明初始化时，参数会形成一个单独的作用域（context）。等到初始化结束，这个这个租用与就会消失。这种语法行为在不设置参数默认值时是不会出现的。（结合以下几个例子了解默认参数值的作用域规则）
{% endhint %}

```javascript
//在此例中，y的默认值等于变量x,调用函数f时形成一个单独的作用域，
//在这个作用域里面默认值变量y指向第一个参数x,而不是全局变量x,
//所以输出2
var x = 1;
function f(x,y=x){
    console.log(y);
}
f(2);//2
/*--------------------------------------------------*/
//函数调用时y=x形成一个单独的作用域，这个作用域里面变量x没有定义，因而指向外层全局变量x.
//函数调用时，函数体内局部变量x影响不到默认值变量
let x =1;
function f(y=x){
    let x = 2;
    console.log(y);
}
f();//1
```

参数默认值的应用

* 利用参数默认值，指定某一参数不得省略
* 将默认值设为undefiend，表明参数可省略



