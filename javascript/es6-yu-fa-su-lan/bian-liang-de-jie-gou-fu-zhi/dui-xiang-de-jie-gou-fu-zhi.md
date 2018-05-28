# 对象的解构赋值



对象的解构与数组有一个重要的不同，在**数组中变量的取值由其位置决定**；**在对象中** ~~****_变量名_~~  **模式名必须与属性名同才能取到真确的值**。

```javascript
//本质：以下两个对象解构赋值语句是等价的，便于我们理解对象解构的本质
let {foo,bar} = {foo:'1',bar:'2'};//是下一个的简写
let {foo:foo,bar:bar} = {foo:'1',bar:'2'};
//结合以下两例理解对象解构赋值：真正被赋值的是后者，而不是前者
//前者只是匹配模式，当省略后者时，默认变量名与属性名（也即与模式名）相同
let {foo:baz} = {foo:'1',bar:'2'};
baz;//'1',foo是匹配模式，baz才是变量，匹配模式必须与某一属性名同才能成功解构赋值
foo;//error:foo is not defined

//嵌套解构对象的解构赋值
const node = {
    loc:{
        start:{
            line:1,
            colum:5
        }
    }
}
//下面代码有3次解构赋值，分别是对loc、start、line三个属性的解构赋值
//最后一次对line属性的解构赋值中，只有line是变量，loc 和 start 都是模式，不是变量
let {loc,loc:{start},loc:{start:{line}}} = node;

//对象解构赋值的默认值
//默认值生效的条件是对象的属性值严格等于undefiend
let {x=3} = {};
x;//3

//将一个已经声明的变量用于解构赋值的注意事项
//js 会将{x}理解成一个代码块，从而发生语法错误。只有不将大括号写在行首，避免js将其解释为代码块，就能解决这个问题
let x;
{x} = {x:1};//SyntaxError:syntax error
//将一个已经声明的变量用于解构赋值的正确写法
let x;
({x}={x:1});

//对象解构赋值的一个便捷应用
//经过以下解构则可通过短变量访问相应的方法
let {log,sin,cos} = Math;

//对数组进行对象解构赋值
//注意 [arr.length-1]:last 的写法：属性名表达式
let arr = [1,2,3];
let {0:first,[arr.length-1]:last} = arr;

```



