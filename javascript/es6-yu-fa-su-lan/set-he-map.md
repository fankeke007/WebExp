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



