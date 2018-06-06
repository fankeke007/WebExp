# Symbol

**1.概述**

es5 对象属性名都是字符串，这容易造成属性名冲突。es6中引入Symbol，提供了一种机制，保证每个属性名都是独一无二的，这样就从根本上防止属性名的冲突。

es6 引入了一种新的原始数据类型Symbol，表示独一无二的值，它是js语言的第七种数据类型。（前6种复习一下：number、string、object、oolean、null、undefined）

Symbol值可以通过Symbol函数生成。现在对象属性可以有两种类型：字符串和Symbol类型。凡是属性名是Symbol类型，都是独一无二的，可以保证不会与其他属性名产生冲突。

{% hint style="danger" %}
注意，Symbol函数不能和new一起使用，否则会报错。这是因为生成的Symbol是一个原始类型的值，而不是对象。
{% endhint %}

Symbol可以接受一个**字符串**作为参数，表示对Symbol实例的描述，主要是为了在控制台显示或转换为字符串时便于区分。若Symbol的参数是一个对象，就会调用对象的toString方法，将其转为字符串，然后才生成一个Symbol值。

{% hint style="danger" %}
注意，Symbol函数的参数只是表示对当前Symbol值的描述，因此相同的参数的Symbol函数的返回值是不相等的。
{% endhint %}

{% hint style="info" %}
1. Symbol值不能与其他类型的值进行运算，会报错
2. Symbol值可以显式转换为字符串
3. Symbol值可以转化为Boolean值，但是不能转换为数值
{% endhint %}

**2.作为属性名的Symbol**

由于每一个Symbol值都是不相等的，这意味着Symbol值可以作为标识符，用于对象的属性名，就能保证不会出现同名的属性。

```javascript
//Symbol值作为属性名的三种写法
let mySymbol = Symbol();
//one
let a = {};
a[mySymbol] = 'Hello!';

//two
let a = {
    [mySymbol]:'Hello!'
}

//three
let a = {};
Object.defineProperty(a,mySymbol,{value:'Hello!'});

//调用Symbol属性时，这样写
a[mySymbol] //hello
```

{% hint style="danger" %}
Symbol 值作为属性名时，不能用点运算符。同理在对象内部，使用Symbol值定义属性时，Symbol值必须放在方括号中。

```javascript
const mySymbol = Symblo();
const a = {};
a.mySymbol = 'Hello!' //新增了一个字符串属性名
a[Symbol]  //undefined
a['mySymbol']  //'Hello!'
```

？？Symbol的内部实现：是否是guid??
{% endhint %}

{% hint style="info" %}
用Symbol定义常量可以保证这组常量的值是不相等的
{% endhint %}

**3.Symbol用例：消除魔术字符串**

魔术字符串是指在代码中多次出现，与代码形成强耦合的某一个具体的字符串或者数值。

```javascript
funciton getArea(shape,options){
	let area = 0;
	switch(shape){
		case 'Triangle' :
			area = .5*options.width*options.height;
			break;
			/*...more code...*/
	}
	return area;
}
getArea('Triangle',{width:100,height:100});
```

“Triangle”即为魔术字符串，多次出现与代码强烈耦合，不利于将来的修改维护。常用的消除魔术字符串的方法是把它写成一个变量：

```javascript
//shapeType.triangle 属性值更适合用Symbol来表示，
//能保障其不与其他shapeType属性值冲突
const shapeType = {
	triangle :'Triangle'
}
funciton getArea(shape,options){
	let area = 0;
	switch(shape){
		case shapeType.triangle :
			area = .5*options.width*options.height;
			break;
			/*...more code...*/
	}
	return area;
}
getArea(shapeType.triangle,{width:100,height:100});
```

**4.Symbol属性名遍历**：**Object.getOwnPropertySymbols\(\)**

```javascript
const obj = {};
let a = Symbol('a');
let b = Symbol('b');

obj[a]='Hello';
obj[b]='es6'；

const objectSymbols = Object.getOwnPropertySymbols(obj);

objectSymbols; //[Symbol(a),Symbol(b)]
```

{% hint style="info" %}
Reflect.ownKeys\(\)方法可以返回所有类型的键名，包括常规键名和Symbol键名。
{% endhint %}

**5.Symbol.for\(\)/Symbol.keyFor\(\)**

有时我们希望使用同一个Symbol值，Symbol.for方法可以做到这一点。它接受一个字符串作为参数，然后搜索有没有以该参数作为名称的Symbol值，若有，就返回这个Symbol值，否则，就新建一个并返回一个以字符串为名称的Symbol值。

```javascript
let s1 = Symbol.for('foo');
let s2 = Symbol.for('foo');

s1 === s2; // true
```

Symbol.for 与 Symbol 这两种写法都会生成新的Symbol。它们的区别是，前者会被登记在全局环境中供搜索，后者不会。

Symbol.keyFor 方法返回一个已登记的Symbol类型值的key。

```javascript
let s1 = Symbol.for('foo');
Symbol.keyFor(s1); // 'foo'

let s2 = Symbol('bar');
Symbol.keyFor(s2);//undefined
```

{% hint style="info" %}
Symbol.for为Symbol值登记的名字，是全局环境的，可以在不同的iframe或service worker 中取到同一个值。
{% endhint %}

**6.实例：模块的Singleton模式（单例模式）**

（文中使用nodejs 的模块文件多次加载返回同一个对象的例子，不够严谨）

**7.内置的Symbol值**

除了自己定义使用Symbol值以外，es6还提供了11个内置的Symbol值，指向语言内部使用的方法。\(了解每一个属性使用场合\)

{% hint style="info" %}
1. Symbol.hasInstance
2. Symbol.isConcatSpreadable
3. Symbol.species
4. Symbol.match
5. Symbol.replace
6. Symbol.search
7. Symbol.split
8. Symbol.iterator
9. Symbol.toPrimitive
10. Symbol.toStringTag
11. Symbol.unscopables
{% endhint %}



