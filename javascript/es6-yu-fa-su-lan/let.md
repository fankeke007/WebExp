# let

1.**作用**

**声明块级作用域变量**，**不会进行变量提升**，因此得先声明后使用，否则会报错 **ReferenceError** 。

```javascript
//var 情形
console.log(foo); //undefined
var foo = 2;

//let 情形
console.log(bar); //error : ReferenceError
let bar = 2;
```

**2.典型使用方法**

2.1 替代循环中的闭包

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
```

