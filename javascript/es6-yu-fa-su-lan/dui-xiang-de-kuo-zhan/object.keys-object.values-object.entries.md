# Object.keys/Object.values/Object.entries

**1.Object.keys\(\)**

es5 标准，返回一个数组，成员是参数对象自身的所有可遍历属性的键名。

es2017 引入了和**Object.keys\(\)配套的 Object.values\(\)** 和 **Object.entries\(\)**，作为遍历对象的一个补充。

**2.Object.values\(\)**

返回一个数组，成员是参数对象自身的所有可遍历属性的键值。

**3.Object.entries\(\)**

返回一个数组，成员是参数对象自身所有可遍历属性的键值对数组。

{% hint style="warning" %}
使用的几点建议

1. 返回数组成员顺序，与属性遍历返回的顺序一致：先数字升序，其次字符串按加入时间，最后Symbol也按加入时间
2. 会过滤Symbol属性
3. 若参数是一个字符串，keys放回index组成数组，values返回字符数组，entries返回\[index,val\]数组
4. 若参数不是一个对象，会先将其转换为对象。数值和布尔（包装对象）会返回空数组
{% endhint %}



