# 对象的扩展运算符

参见变量的解构赋值一章

{% hint style="warning" %}
1.解构赋值属于浅层拷贝，若一个键的值是复合类型（数组、对象、函数），那么解构赋值拷贝的是这个值的引用，而不是这个值的副本。

```javascript
let obj = {a:{b:1}};
let {...x}=obj;
obj.a.b = 2;
x.a.b;//2
```

2.**扩展运算符\(...\)的解构赋值**，不能复制继承自原型对象的属性

```javascript
const o = Object.create({x:1,y:2};
o.z=3;
let {x,...newObj}=o;
let {y,z} = newObj;
x//1
y//undefined
z//3
```

上面代码中，变量**x是单纯的解构赋值**，所以可以读取对象o继承的属性；变量**y和z是扩展运算符的解构赋值**，只能读取对象o自身的属性，所以变量z可以赋值成功，变量y取不到值。
{% endhint %}

对象的扩展运算符的一些使用场景：

-**拷贝对象**

```javascript
//拷贝对象(只拷贝对象实例属性)
let aClone = {...a};
//等同于
let aClone = Object.assign({},a);

/******************/

//要完整拷贝一个对象，还拷贝对象的原型属性，可以采用如下写法
//法一
const clone1={
    __proto__:Object.getPrototypeOf(obj),
    ...obj
};
//法二
const clone2 = Object.assign(
    Object.create(Object.getPrototypeOf(obj)),
    obj
);
//法三
const clone3 = Object.create(
    Object.getPrototypeOf(obj),
    Object.getOwnPropertyDescriptors(obj)
);
```

**合并两个对象**

```javascript
//合并对象a,b返回新的合成后对象ab
let ab = {...a,...b};
//等同于
let ab = Object.assign({},a,b);

//若用户自定义属性位于扩展运算符之后，这扩展运算符内部的同名属性会被覆盖
//这可以很方便的用来修改现有对象的部分属性
let newVersion = {
    ...previousVersion,
    name:'new name'
}
```

**设置新对象的默认值**

```javascript
//若把自定义属性放在扩展运算符前面，就变成了设置新对象的默认属性值
let aWithDefaults = {x:1,y:2,...a};
//等同于
let aWithDefaults = Object.assign({},{x:1,y:2},a);
//等同于
let aWithDefaults = Object.assign({x:1,y:2},a)
```



