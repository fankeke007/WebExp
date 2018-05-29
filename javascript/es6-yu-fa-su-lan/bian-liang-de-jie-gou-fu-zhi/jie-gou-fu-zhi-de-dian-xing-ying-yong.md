# 解构赋值的典型应用

**1.交换变量值**

```javascript
//不在需要第三方临时变量作跳板
//前面fibonacci数列生成器中有用到
let x = 1;
let y = 2;
[x,y]=[y,x];
```

**2.从函数返回多个值**

```javascript
//函数一次只能返回一个值，但是可以通过对返回的数组或者兑现解构，更便捷的获取多个返回值
function eg(){
    return [1,2,3];
}
let [a,b,c]=eg();
```

**3.函数参数的定义**

```javascript
//解构赋值可以方便将一组参数与变量名对应起来
function f([x,y,z]){return x + y + z};
f([1,2,3]);//6

//参数是一组无序值
function f1({x,y,z}){...}
f1({x:1,y:2,z:3});

//es5以前要实现参数是无序值，得传入一个对象，但使用参数时得使用obj.attr形式
```

**4.提取json数据**

```javascript
let jsonData = {
    id:42,
    status:'ok',
    data:[867,5309]
}
let {id,status,data:number}=jsonData;
```

**5.函数参数的默认值**

```javascript
//指定默认参数避免了以往函数体内大量的var foo=config.foo || default.foo;语句
jQuery.ajax = function(
    url,
    {
        async=true,
        beforeSend=function(){},
        cache=true,
        complete=function(){},
        crossDomain=false,
        global=true,
        //...more config
    }
){
    //do something
};
```

**6.遍历Map结构**

任何部署了Iterator 接口的对象都可以使用for...of循环遍历。Map结构原生支持Iterator接口，配合变量的解构赋值，获取键名和值名就非常方便。

```javascript
const map = new Map();
map.set('first','hello');
map.set('second','world');

//同时获取键与值
for (let [key,value] of map){
    console.log(key + ' is ' + value);
}

//只获取键
for (let [key] of map){
    console.log(key);
}

//只获取值
for (let [,value] of map){
    console.log(value);
}
```

**7.获取模块的指定方法**

```javascript
const {SourceMapConsumer,SourceNode} = require('source-map');
```



