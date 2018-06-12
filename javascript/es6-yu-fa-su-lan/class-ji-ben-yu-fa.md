# Class 基本语法

**1.简介**

es5中生成实例对象的传统方法是通过构造函数：这和传统的面向对象差异很大。

```javascript
function Point(x,y){
    this.x = x;
    this.y = y;
};
Point.prototype.toString = function(){
    return '('+this.x+', '+this.y+')';
};
```

es6 提供了更接近传统语言的写法，引入了Class（类）这个概念，作为对象的模板。通过class关键字，可以定义类。其实质是一个语法糖，它的绝大部份功能，es5都可以做到，新的class写法只是让对象原型的写法更加清晰、更加面型对象编程的原发而已。上面的用es6的class改写如下：

```javascript
//定义类
class Point {
    constructor(x,y){
        this.x = x;
        this.y = y;
    }
    //两个方法之间不能有逗号，会报错
    
    //直接写方法名即可，不需function声明
    toString(){
        return '('+this.x+', '+this.y+')';
    }
}
```

```javascript
//es6 的类完全可以看作是构造函数的另一种写法
typeof Point //'function'
Point === Point.prototype.constructor // true
```

由于类的方法都定义在prototype对象上面，所以类的新方法可以添加在prototype对象上面。Object.assign\(\)可以方便的一次向类添加多个方法。

```javascript
Object.assign(Point.prototype,{
    toString(){},
    toValue(){}
})
```

{% hint style="warning" %}
通过class定义的类的内部所有的方法都是不可枚举的，这与es5构造函数原型上定义方法的行为是不一致的。
{% endhint %}

**2.严格模式**

类和模块内部默认就是严格模式。即只要代码写在类中或者模块之中，就只有严格模式可用。（今后写代码也尽量使用严格模式，因为未来的代码将都是运行在严格模式之中）（传送门：[严格模式与普通模式的区别](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)）

3**.constructor**

constructor 方法是类的默认方法，通过new命令生成对象实例时，自动调用该方法。一个类必须有constructor方法，若没有显示定义，一个空的constructor方法会被默认添加。constructor方法默认返回实例对象（即：this），完全可以指定返回另外一个实例对象。

```javascript
//返回一个全新对象，到时返回结果不是Foo的实例
class Foo {
    constructor(){
        return Object.create(null); 
    }
}
```

类必须使用new调用，否则会报错。这是它跟普通构造函数的一个主要区别，后者不用new也可以调用。

**4.类的实例对象**

实例的属性除非显示定义在其本身（即定义在this对象上），否则都定义在原型上（即定义在class上）。通过实例的\_\_proto\_\_属性可以获得实例的原型对象，对其进行修改将会影响该类的所有实例。

**5.Class 表达式**

类也可以像函数一样使用表达式的形式定义。

下面代码使用表达式定义了一个类。需要注意的是，**这个类的名字是MyClass而不是Me，Me只在Class的内部代码可用，指代当前类**。若类的内部没有使用Me的话，则可以省略Me。

```javascript
const MyClass = class Me{
    getClassName(){
        return Me.name;
    }
}
```

采用class表达式可以写出立即执行的Class

```javascript
let person = new class {
    constructor(name){
        this.name = name;
    }
    sayName(){
        console.log(this.name);
    }
}('haha')
person.say();//'haha'
```

6.**类不存在变量提升**

**注意：这一点与es5 完全不同**。

**7.私有方法和私有属性**

以下划线命名的方式区分（如\_bar），不能做到严格意义上的“私有”，外界还是能访问。es6 中可以通过Symbol来模拟私有属性。es2018 有一个提案使用 \#号前缀表示私有属性或方法。

**8.this指向**

类方法内部若有this，默认指向类的实例。**但是，必须非常小心，一旦单独使用该方法，很可能报错**。即会出现this丢失的情况。

{% hint style="info" %}
**单独使用类方法时防止this丢失的几种方法**

1. 通过bind显示绑定
2. 使用箭头函数
3. 使用Proxy，获取方法时，自动绑定this

```javascript
//法一：构造函数中绑定this
class Logger{
    constructor(){
        this.printName = this.printName.bind(this);
    }
}

//法二：箭头函数
class Logger{
    constructor(){
        this.printName = (name = 'there')=>{
            this.print(`Hello ${name}`);
        }
    }
}

//法三：Proxy
function selfish(target){
    const cache = new WeakMap();
    const handler = {
        get (target,key){
            const value = Reflect.get(target,key);
            if(typeof value !== 'function'){
                return value;
            }
            if(!cache.has(value)){
                cache.set(value,value.bind(target));
            }
            return cache.get(value);
        }
    };
    const proxy = new Proxy(target,handler);
    return proxy;
}
const logger = selfish(new Logger());
```
{% endhint %}

**9.name属性**

name属性总是返回紧跟在class关键字后面的类名。

**10.Class的取值（getter）与存值（setter）函数**

**与es5 一样，在“类”的内部可以使用get和set关键字，对某个属性设置存值和取值函数，拦截该属性的存取行为**。

```javascript
class MyClass{
    constructor(){}
    get prop(){
        return 'getter';
    }
    set prop(value){
        console.log('setter: '+value);
    }
}
let inst = new MyClass();
inst.prop = 123; //setter: 123
inst.prop; //'getter'
```

**11.Class 的Generator方法**

若类的某个方法之前有 \* 号，就表示该方法是一个Generator函数。

下面代码中，Foo类的Symbol.iterator方法前有一个星号，表示该方法是一个Generator函数。Symbol.iterator 方法返回一个Foo类的默认遍历器，for...of循环会自动调用这个遍历器。

```javascript
class Foo{
    constructor(...args){
        this.args = args;
    }
    *[Symbol.iterator](){
        for (let arg of this.args){
            yield arg;
        }
    }
}
for(let x of new Foo('hello','fankeke')){
    console.log(x);
}
//hello
//fankeke
```

**12.Class 的静态方法**

类相当于实例的原型，所有在类中定义的方法都会被实例继承。若在一个方法前加上static关键字，则该方法不会被实例继承，需要直接同过类来调用，这就称为静态方法。若静态方法包含this关键字，这个this指的是类，而不是实例。（静态方法可以与非静态方法重名）。父类的静态方法可以被子类继承。静态方法也可以从super对象上调用。

{% hint style="info" %}
Class 的 static 静态方法使用注意事项汇总

1. 静态方法只能通过类直接调用，不能通过实例调用
2. 静态方法可以被子类继承
3. 子类中可以通过super调用父类静态方法
{% endhint %}

**13.Class 的静态属性和实例属性**

静态属性指的是Class本身的属性，即Class.propName，而不是定义在实例对象（this）上的属性。目前只能通过Foo.prop的形式定义一个Foo类的静态属性prop。es6 明确规定，Class 内部只有静态方法，没有静态属性。

目前有一个提案对静态属性和实例属性都规定了新的写法。

```javascript
//以下各浏览器厂商及Babel都还未实现

//类的实例属性可以用等式写入类的定义之中，之前定义实例属性只能写在constructor之中
class MyClass{
    myProp = 112;
    constructor(){
        console.log(this.myProp);
    }
}

//类的静态属性只需在前面实例的静态属性的基础上加上static关键字就可以了
class MyClass{
    static myProp = 112;
}

//新的提案的语法在语义上更直接
```

**14.new.target 属性**

new是从构造函数生成实例对象的命令。es6 为new 命令引入一个**new.target** 属性，**该属性一般用在构造函数之中，返回new命令作用于的那个构造函数**。若构造函数不是通过new命令调用的，new.target会返回undefiend，因此这个属性可以用来确定构造函数是怎么调用的。

Class 内部调用new.target ，返回当前Class。子类继承父类是，new.target 会返回子类。利用这个特点可以写出不能独立使用，不需继承后才能使用的类。

```javascript
class Shape{
    constructor(){
        if(new.target === Shape){
            throw new Error('本类不能实例化');
        }
    }
}
class Rectangle extends Shape{
    constructor(length,width){
        super();
        //...
    }
}
var x = new Shape(); // 报错 
var y = new Rectangle(3, 4); // 正确
```

