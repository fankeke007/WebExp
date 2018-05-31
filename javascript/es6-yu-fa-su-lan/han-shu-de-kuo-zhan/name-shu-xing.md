# 箭头函数

箭头函数具体使用方法见如下几例

```javascript
var f = v => v;

// 等同于
var f = function (v) {
  return v;
};
```

```javascript
//如果箭头函数不需要参数或需要多个参数，就使用一个圆括号代表参数部分

var f = () => 5;
// 等同于
var f = function () { return 5 };

var sum = (num1, num2) => num1 + num2;
// 等同于
var sum = function(num1, num2) {
  return num1 + num2;
};
```

```javascript
// 如果箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用return语句返回

var sum = (num1, num2) => { return num1 + num2; }
```

```javascript
// 由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号，否则会报错

// 报错
let getTempItem = id => { id: id, name: "Temp" };

// 不报错
let getTempItem = id => ({ id: id, name: "Temp" });
```

```javascript
// 如果箭头函数只有一行语句，且不需要返回值，可以采用下面的写法，就不用写大括号了

let fn = () => void doesNotReturn();
```

```javascript
// 箭头函数与变量解构结合使用

const full = ({ first, last }) => first + ' ' + last;

// 等同于
function full(person) {
  return person.first + ' ' + person.last;
}
```

```javascript
// 箭头函数的一个用处是简化回调函数

// 正常函数写法
[1,2,3].map(function (x) {
  return x * x;
});

// 箭头函数写法
[1,2,3].map(x => x * x);

/*----------另一个例子----------*/
// 正常函数写法
var result = values.sort(function (a, b) {
  return a - b;
});

// 箭头函数写法
var result = values.sort((a, b) => a - b);
```

```javascript
//  rest 参数与箭头函数结合的例子

const numbers = (...nums) => nums;

numbers(1, 2, 3, 4, 5)
// [1,2,3,4,5]

const headAndTail = (head, ...tail) => [head, tail];

headAndTail(1, 2, 3, 4, 5)
// [1,[2,3,4,5]]
```

{% hint style="info" %}
箭头函数使用注意事项

1. 函数体内的this对象，就是**定义时所在的对象**，而**不是使用时所在的对象**
2. 不可以当做构造函数，会报错
3. 不可以使用 **arguments** 对象，该对象在函数内不存在。可以使用rest参数代替
4. 不可以使用 **yield** 命令，因而**箭头函数不能用作generator函数**
{% endhint %}

```javascript
//结合以下几例理解第一点（总要）

//例子1
function foo(){
    setTimeout(
        ()=>{console.log('id:':this.id);},
        1000
    );
}
var id = 21;
foo.call({id:42});//id:42

//箭头函数可以让setTimeout回调里面的this，绑定定义时所在的作用域，而不是指向运行时所在的作用域

//例子2
function Timer(){
    this.s1 = 0;
    this.s2 = 0;
    setInterval(
        ()=>this.s1++,
        1000
    );
    setInterval(
        function(){this.s2++},
        1000
    );
}
var timer = new Timer();

setTimeout(()=>console.log('s1: ',timer.s1),3100);
setTimeout(()=>console.log('s2: ',timer.s2),3100);
//s1: 3
//s2: 0 一直为0
```

