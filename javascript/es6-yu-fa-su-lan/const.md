# const

**1.作用**

声明一个**只读**常量，一旦声明，常量值就不能改变。**声明const常量时必须得初始化**。const 声明变量的作用域及变量特性（如提升等）与 let 同。

{% hint style="info" %}
const 实际保证的是常量指向的内存地址不得改动。对于简单变量（number、string、Boolean），值就保存在变量指向的那个内存地址，因此等同于常量。

但对于符合类型的数据（Array、Object），变量指向的内存地址保存的只是一个指针，const只能保证这个指针是固定的，但是不能保证它指向的数据结构是不可变的。
{% endhint %}

1.1 值为符合类型的情况

```javascript
const a = []
a.push('Hello');
a.push('Fankeke');
a;//['Hello','Fankeke']
a = [];//TypeError：Assignment to constant variable
```

1.2 冻结符合对象

```javascript
const foo = Object.freeze({P:'Hello'});
foo.prop = 123;//不起作用，严格模式下会报错
```

彻底冻结对象（循环递归冻结）

```javascript
var constantize = obj =>{
	Object.freeze(obj);
  	Object.keys(obj).forEach((key,val) =>{
    	if(typeof obj[key] === 'object'){
        	constantize(obj[key]);
        }
    } )

}
```

> **es6 声明变量的6种方法**
>
> es5 只有两种声明变量的方法：var 和 function 。es6 新添加了 let 、const、import、class 命令。



