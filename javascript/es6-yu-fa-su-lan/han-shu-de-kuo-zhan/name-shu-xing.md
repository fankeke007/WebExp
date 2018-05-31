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

```javascript
// 箭头函数转成 ES5 的代码如下

// ES6
function foo() {
  setTimeout(() => {
    console.log('id:', this.id);
  }, 100);
}

// ES5
function foo() {
  var _this = this;

  setTimeout(function () {
    console.log('id:', _this.id);
  }, 100);
}
```

```javascript
//下面代码之中，只有一个this，就是函数foo的this，
//所以t1、t2、t3都输出同样的结果。
//因为所有的内层函数都是箭头函数，都没有自己的this，
//它们的this其实都是最外层foo函数的this

function foo() {
  return () => {
    return () => {
      return () => {
        console.log('id:', this.id);
      };
    };
  };
}

var f = foo.call({id: 1});

var t1 = f.call({id: 2})()(); // id: 1
var t2 = f().call({id: 3})(); // id: 1
var t3 = f()().call({id: 4}); // id: 1
```

{% hint style="warning" %}
1. arguments、super、new.target 这三个变量在箭头函数中都不存在，若在其中使用则指向外层函数对应的变量。
2. 由于箭头函数没有自己的this（箭头函数中的this指向定义时外层的this），所以也不能用call\(\)/apply\(\)/bind\(\) 这些方法去改变this的指向。

```javascript
(function() {
  return [
    (() => this.x).bind({ x: 'inner' })()
  ];
}).call({ x: 'outer' });
// ['outer']
```
{% endhint %}

**嵌套的箭头函数使用方法**

```javascript
//es5
function insert(value){
    return {into:function(array){
        return {after:function(afterValue){
            array.splice(array.indexOf(afterValue)+1,0,value);
            return array;
        }}
    }}
}
insert(2).into([1,3]).after(1);

//es6
let insert = (value)=>(
    {into:(array)=>(
        {after:(afterValue)=>{
            array.splice(array.indexOf(afterValue)+1,0,value);
            return array;
        }
    })
});
insert(2).into([1,3]).after(1);
```



