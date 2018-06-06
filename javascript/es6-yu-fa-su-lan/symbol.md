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

