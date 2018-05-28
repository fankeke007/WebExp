# 变量的结构赋值

**解构（Destruction）**：es6 允许按照一定的模式，从数组和对象中提取值，这被称为结构。

以下直接上代码，理解 es6 的结构赋值用法。

1.**数组的结构赋值**

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
function* fib(){
    let a = 0;
    let b = 1;
    while(true){
        yiled a;
        [a,b]=[b,a+0]
    }
}
let [a,b,c,d,e,f]=fibs();

```

