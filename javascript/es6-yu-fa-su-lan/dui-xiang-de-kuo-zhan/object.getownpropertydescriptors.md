# Object.getOwnPropertyDescriptors\(\)

**返回指定对象所有自身属性的描述对象**。

**该方法的引入，主要是为了解决Object.assign\(\)无法正确拷贝get属性和set属性的问题**。

Object.assign\(\)总是拷贝一个属性的值，而不会拷贝它背后的赋值方法或取值方法。而Object.getOwnpropertyDescriptors\(\)配合Object.defineProperties\(\)方法，就可以实现正确拷贝。

```javascript
//属于浅拷贝
const source = {
    set foo(value){
        console.log(value);
    }
};
const target2 = {};
Object.defineProperties(target2,Object.getOwnPropertyDescriptors(source));
Object.getOwnPropertyDescriptor(target2,'foo');
//{
//get:undefined,
//set:[Function:set foo],
//enumerable:true,
//configrable:true
//}
```

Object.getOwnPropertyDescriptors\(\)方法的另一个用处，是配合Object.create方法，**将对象属性克隆到一个新对象**。这属于浅拷贝。

```javascript
//实现对象的浅拷贝
const shallowClone = (obj)=>Object.create(
        Object.getPrototypeOf(obj),
        Object.getOwnPropertyDescriptors(obj)
);
```

利用Object.getOwnPropertyDesctiptors\(\)实现Mixin模式：

```javascript
let mix = (object) => ({
    with:(...mixins) => mixins.reduce(
        (c,mixin) => Objects.create(c,Object.getOwnPropertyDescriptors(mixin))
    ,object)
});

let a = {a:'a'};
let b = {b:'b'};
let c = {c:'c'};
let d = mix(c).with(a,b);

d.c // "c"
d.a // "a"
d.b // "b"
```

