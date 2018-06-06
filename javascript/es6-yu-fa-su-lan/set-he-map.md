# Set 和 Map

**1.set**

es6提供了新的数据结构Set，它类似与数组，但是成员的值都是唯一的，没有重复的值。（和数学中的集合类似，也和python中的set类似。**集合特性：确定性，互异性、无序性**）

```javascript
//eg1:利用数组初始化
const set = new Set([1,2,4,5,6]);
[...set] //[1,2,4,5,6]

//eg2:集合大小size
const items = new Set([1,2,4,5,6]);
items.size // 5

//eg3：通过类数组对象初始化
const set = new Set(document.querySelectorAll('div'));
set.size // 34

//去除数组重复成员
[...new Set(array)]
```

{% hint style="warning" %}
1. 向Set加入（add）值的时候，不会发生类型转换，所以5和‘5’是两个不同的值。
2. 两个对象总是不相等的，当向Set中add两个空对象{}时，它们被视为不等值。
3. 
{% endhint %}

{% hint style="info" %}
**Set 实例的属性和方法**

**原型方法：**

* Set.prototype.constructor：构造函数，默认为Set函数
* Set.prototype.size：返回Set实例的成员数量

**操作方法：**

* add\(value\)：添加某个值，返回Set结构本身，类似数组的push
* delete\(value\)：删除某个值，返回一个Boolean值，表示删除是否成功
* has\(value\)：返回一个Boolean值，表示该值是否是Set成员
* cleatr\(value\)：清除所有成员，没有返回值

**遍历方法：**

* keys\(\)：返回键名的遍历器
* values\(\)：返回值名的遍历器
* entries\(\)：返回键值对的遍历器
* forEach\(\)：使用回调函数遍历每个成员
{% endhint %}

```javascript
let set = new Set(['red','green','yellow']);

for (let item of set.keys()){
    console.log(item);
}
//red green yellow

for (let item of set.values()){
    console.log(item);
}
// red green yellow

for (let item of set.entries()){
    console.log(item);
}
// ['red','red'] ['green','green'] ['yellow','yellow']
```

{% hint style="info" %}
Set 结构的实例默认可遍历，它的默认遍历器生成函数就是他的values方法，因而利用values遍历是可省略values，直接**for\(let item of set\)**

```javascript
Set.prototype[Symbol.iterator] === Set.prototype.values
```
{% endhint %}

**遍历的应用**

利用扩展运算符，在Set和Array之间转换。可以是Set间接具有Array的其他方法（map/filter等）

```javascript
//集合的交并补

//并集
let union = new Set([...a,...b]);

//交集
let intersect = new Set([...a].filter(x=>b.has(x)));

//补集
let difference = new Set([...a].filter(x=>!b.hsa(x)));
```

**2.WeakSet**

**WeakSet 和 Set 类似，但是有两个区别：**

1. WeakSet 成员只能是对象，而不是其他类型的值。
2. WeakSet中的对象都是弱引用，即垃圾回收机制不考虑WeakSet对该对象的引用，若其他对象都不在引用该对象，垃圾回收机制会自动收回该对象所占用的内存，而不考虑对象是否还存在与WeakSet中。
3. （基于上一点推出）由于垃圾回收机制的不可预测性，因此es6规定WeakSet不可遍历

这些特点同样适用于WeakMap。

**语法：**WeakSet 是一个构造函数，可以接受一个数组或者一个类数组的对象作为参数。（实际上任何具有Iterable接口的对象，都可以作为WeakSet的参数。）**该数组的所有成员**都会自动成为**WeakSet实例对象的成员**。（**传入参数数组的成员必须是对象**）

**WeakSet有以下三种方法**：

1. WeakSet.prototype.add\(value\)
2. WeakSet.prototype.delete\(value\)
3. WeakSet.prototype.has\(value\)

WeakSet的一个用处是存储DOM节点，而不用担心这些节点从文档删除是，会引发内存泄漏。

```javascript
const foos = new WeakSet();
class Foo {
    constructor(){
        foos.add(this);    
    }  //注意这里不能有逗号，会报错
    method(){
        if(!foos.has(this)){
            throw new TypeError('Foo.prototype.method 只能在\
            Foo实例上使用');
        }
    }
}
//？？？（意义与用途）
//上面代码保证了Foo的实例方法，只能在Foo的实例上调用。
//这里使用 WeakSet 的好处是，foos对实例的引用，
//不会被计入内存回收机制，所以删除实例的时候，
//不用考虑foos，也不会出现内存泄漏。
```

**3.map**

js的对象Object，本质上是键值对的集合（hash 结构），但是传统上只能使用字符串当做键，这给它的使用带来了限制。

```javascript
const data = {};
const element = document.getElementById('myDiv');
data[element]='metadata';
data['[object HTMLDivElement]'] // 'metadata'

//原意是将一个DOM节点作为对象data的键，但是由于对象只能接受字符串作为键名，
//所以element被自动转换为了‘[object HTMLDivElement]’
```

为了解决传统对象只能以字符串作为键名的限制，es6引入了Map。它类似与Object，也是键值对的集合，但是键的范围不在限制于支付串，各种类型的值（包括对象）都可以当做键。

{% hint style="info" %}
就是说，Object结构实现了“字符串--值”的对应，Map结构提供了“值--值”的对应。Map是一种跟完善的Hash结构的实现。
{% endhint %}

```javascript
const m = new Map();
const o = {p:'Hello es6!'};

m.set(o,'content');
m.get(o);//'content'

m.has(o) //true
m.delete(o) //true
m.has(o)  //false
```

作为构造函数Map，可以接受一个数组（或任何具有Iterator接口且每一个成员都是一个双元素数组的数据结构）作为参数，该数组的成员是一个个表示键值对的数组。

```javascript
const map = New Map([
    ['name','张三'],
    ['title','Author']
]);
map.size // 2
map.has('name') //true
map.get('titile') //'Author'

//等同于
const map = new Map();
const items = [
    ['name','张三'],
    ['title','Author']
];
items.forEach(
    ([key,value])=>map.set(key,value);
);
```

{% hint style="info" %}
Map 实例的属性与方法

属性：

* size：返回Map结构的成员总数

操作方法：

* set\(key,value\)：设置键名key对应的值为value
* get\(key,value\)：读取key对应的键值
* has\(key\)
* delete\(key\)
* clear\(\)

遍历方法：\(**Map的遍历顺序就是插入顺序**\)

* keys\(\)
* values\(\)
* entries\(\)    **//Map 结构默认遍历器接口**
* forEach\(\)  **//可传入第二个参数用来绑定this**
{% endhint %}

{% hint style="info" %}
**与其他数据结构的相互转换：\(需熟练\)**

1. Map  &lt;=&gt; Array
2. Map  &lt;=&gt; Object
3. Map &lt;=&gt; JSON
{% endhint %}



