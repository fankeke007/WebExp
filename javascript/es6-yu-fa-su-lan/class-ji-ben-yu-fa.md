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

2.严格模式

类和模块内部默认就是严格模式。即只要代码写在类中或者模块之中，就只有严格模式可用。（今后写代码也尽量使用严格模式，因为未来的代码将都是运行在严格模式之中）（传送门：[严格模式与普通模式的区别](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)）



