# let

1.**作用**

**声明块级作用域变量**，**不会进行变量提升**，因此得先声明后使用，否则会报错 **ReferenceError** 。

**1.1 块级作用域示例**

```javascript
{
    let a = 2;
    var b = 3;
}
console.log(a);//ReferenceError
console.log(b);//3
```

**1.2** **变量提升示例**

```javascript
//var 情形
console.log(foo); //undefined
var foo = 2;

//let 情形
console.log(bar); //error : ReferenceError
let bar = 2;
```

**2.典型使用方法**

**2.1 替代循环中的闭包**

```javascript
// 循环变量使用var情形
var a = [];
for(var i = 0; i < 10; i++){
	(function(i){
		a[i] = function(){
			console.log(i);
		}
	})(i)
}
a[4]();//4,得使用闭包才能达到运行期间记住i状态的效果，若不使用闭包，则输出全是10

//循环变量使用let情形
var a = [];
for(let i = 0; i < 10; i++){
	a[i] = () => console.log(i);
}
a[4]();//4
```

**3.注意事项**

{% hint style="danger" %}
es6 明确规定，若在区块中存在let 、const 命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域，凡在声明之前就使用这些变量，就会报错。
{% endhint %}

```javascript
//
(function(a){
	return function scop(){
		console.log(a);  //2
		console.log(a);  //2
	}
})(2)

// let
(function(a){
	return function scop(){
		console.log(a);  //ReferenceError
		let a = 3;	
		console.log(a);  //因报错无法执行到此处
	}
})(2)

//var
(function(a){
	return function scop(){
		console.log(a);  //undefiend
		var a = 3;	
		console.log(a);  //3
	}
})(2)
```

