# Class 的继承

**1.简介**

Class可以通过extends 关键字实现继承，这比 es5 通过修改原型链实现继承，要清晰和方便许多。

```javascript
//父类
class Point{
    constructor(x,y){
        this.x = x;
        this.y = y;
    }
    toString(){
        return 'x: '+this.x+' y: '+this.y;
    }
};
//子类
class ColorPoint extends Point{
    constructor(x,y,color){
        super(x,y); //调用父类的constructor
        this.color=color;
    }
    toString(){
        return this.color+' '+super.toString();
    }
}
```

上面的代码中，constructor和toString方法中，都出现了super关键字，它在这里表示父类的构造函数，用来新建父类的this对象。**子类必须在constructor方法中调用super方法，否则新建实例时会报错。这是因为子类自己的this对象，必须先通过父类的构造函数完成塑造，得到与父类同样的实例属性和方法，然后再对其进行加工，加上子类自己的实例属性和方法。若不调用super方法，子类就得不到this对象**。

{% hint style="warning" %}
**es5 继承 VS es6 继承**

es5 继承，实质是先创造子类的实例对象this，然后再将父类的方法添加到this上面（Parent.apply\(this\)）.

es6的继承机制完全不同，实质是先创建父类的实例对象this（所以必须先调用super方法），然后再调用子类的构造函数修改this。
{% endhint %}

{% hint style="danger" %}
在子类的构造函数之中，只有调用super之后，才可以使用this关键字，否则会报错。这是因为子类实例的构建是基于对父类实例的加工，只有super方法才能返回父类的实例。
{% endhint %}

**2.Object.getPrototypeOf\(\)**

这个方法可以用来从子类上获取父类。可以用来判断一个类是否继承了另一个类。

```javascript
Object.getPrototypeOf(ColorPoint) === Point
//true
```

**3.super关键字**

可以当做**函数使用**也可以当做**对象使用**。

**super作为函数调用时**，代表父类的构造函数，es6 要求子类的构造函数必须执行一次super函数。作为函数时super只能用在子类的构造函数之中，用在其他地方会报错。

**super 作为对象调用时**，在**普通方法中，指向父类的原型对象**；在**静态方法中，指向父类**。es6 规定，在子类**普通方法中通过super调用父类的方法是，方法内部的this指向当前的子类实例**。在子类**静态方法中通过super调用父类的方法时，方法内部的this指向当前的子类，而不是子类的实例**。

{% hint style="warning" %}
注意作为函数调用时，super虽然代表了父类的的构造函数，但是返回的是子类的实例，即super内部的this指的是子类，因此super\(\)这里相当于：**Point.prototype.constructor.call\(this\)**.

```javascript
class A{
    constructor(){
        console.log(new.target.name);
    }
}
class B extends A{
    constructor(){
        super();
    }
}
new A(); // A
new B(); // B
```
{% endhint %}

**4.类的prototype属性和\_\_proto\_\_属性**

```javascript
class A{};
class B extends A{};

B.__proto__ === A; //true
B.prototype.__proto__ === A.prototype // true
```

**子类的\_\_proto\_\_属性**，**表示构造函数的继承**，总是指向父类。

**子类prototype属性的\_\_proto\_\_属性**，**表示方法的继承**，总是指向父类的prototype属性。

这样额结果是因为类的继承是按照下面的模式实现的：（两条继承链）

```javascript
class A{};
class B{};

//B的实例继承A的实例
Object.setPrototypeOf(B.prototype,A.prototype);

//B 继承 A 的静态属性
Object.setPrototypeOf(B,A);

const b = new B();
```

？？这两条继承链可以这样理解：**作为一个对象**，子类（B）的原型（\_\_proto\_\_属性）是父类（A）；**作为一个构造函数**，子类（B）的原型对象（prototype属性）是父类的原型对象（prototype属性）的实例。

{% hint style="warning" %}
**原型对象 与 构造函数的prototype属性 之间的区别**

**原型对象**：可以通过Object.getPrototypeOf\(obj\)或者已被弃用的**\_\_proto\_\_**属性获得。

**前者（原型对象）是每个实例上都有的属性**，**后者是构造函数的属性**。

Object.getPrototypeOf\(new Foobar\(\)\) 和 Foobar.prototype指向着同一个对象。

**总结：实例的原型对象等于创建实例的构造函数的（prototype）原型属性**
{% endhint %}

验证以上结论：

```javascript
//验证1
//c 是对象的实例，其原型对象等于其构造函数（Object）的原型属性Object.prototype
var c = {};
c.__proto__ === Object.prototype; //true

//验证2
//因为class A 实质是构造函数 function A(){} 的语法糖，故A实质上是Function的实例
A.__proto__ === Funciton.prototype; //true

//验证3 (暂无法验证)
class A{};
class B extends A{};

```

