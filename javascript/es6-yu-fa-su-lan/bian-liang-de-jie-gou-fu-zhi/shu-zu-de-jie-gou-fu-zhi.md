# 数组的解构赋值

阅读以下源码及注释：主要理解 \[**模式匹配、（右侧）可遍历结构Iterator、默认值**\] 概念。

```javascript
//按照对应的位置，对变量赋值
//本质上属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值
//若结构不成功，变量值就为undefined
let [a,b,c] = [1,2,4];
a;//1
c;//4

let [,,third] = [1,3,4];
third;//4

let [x,y,...z]=['a'];
x;//'a'
y;//undefiend
z;//[]

//若等号右边不是数组（或严格的说不是可遍历结构 Iterator）将会报错
let [foo] = 1;//error

//对于Set结构，也可以使用数组的结构赋值
let [e,f,g] = new Set([1,3,4]);
e;//1

//事实上只要某种数据结构具有Iterator接口，就可以采用数组结构赋值
//生成器（generator）
function* fib(){
    let a = 0;
    let b = 1;
    while(true){
        yiled a;
        [a,b]=[b,a+0]
    }
}
let [h,i,j,k,l,m]=fibs();

//指定默认值的解构
//由于 es6 内部使用严格等于（===）运算符，判断一个位置是否有值
//只有当一个数组成员严格等于undefined，默认值才会生效
let [n,o,p=3] = ['a','b'];
o;//b
p;//3

let [q=1,r=2] = [undefined,null];
q;//1,数组成员严格等于undefined,默认值生效
r;//null ,null不严格等于undefined,默认值不会生效

//若指定的默认值是一个表达式，则表达式是惰性求值的
function f1(){console.log('当我执行时，证明默认值被采用');return 'hello destruction!'}
let [t = f1()]=['haha'];
t;//'haha',f1()并不会执行

//默认值可以引用解构赋值的其他变量，前提是该变量已经声明
let [x=1,y=x]=[];//x=1,y=1
let [x=y,y=1]=[];//error
```



