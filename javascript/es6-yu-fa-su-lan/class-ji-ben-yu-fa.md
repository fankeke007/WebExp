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

8.this指向

类方法内部若有this，默认指向类的实例。**但是，必须非常小心，一旦单独使用该方法，很可能报错**。即会出现this丢失的情况。

{% hint style="info" %}
防止this丢失的几种方法

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

