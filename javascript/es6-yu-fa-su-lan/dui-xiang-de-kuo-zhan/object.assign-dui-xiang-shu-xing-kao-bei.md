---
description: 将源对象自身可枚举属性拷贝到目标对象，是浅拷贝。
---

# Object.assign\(\) 对象属性拷贝

```javascript
//后面源同名属性会覆盖前面的
const target = {a:1,b:1};
const source1 = {b:2,c:2};
const source3 = {c:3};

Object.assign(target,source1,source2);
target //{a:1,b:2,c:3}
```

{% hint style="danger" %}
1. 若只有一个参数，会直接返回该参数的对象形式（不是对象的会先转换成对象）
2. 若null、undefined为第一个参数（即为目标对象，会报错）；不为第一个参数不会报错，但因无法转换为对象会跳过。
3. 其他类型值（数值、字符串和布尔值）不在首参数，不会报错，但是除了字符串会以数组形式拷贝到目标对象，其他值都不会产生效果。
4. 取值函数（get）将进行求值后再复制
{% endhint %}

```javascript
const v1 = 'abc';
const v2 = true;
const v3 = 12;

const obj=Object.assign({},v1,v2,v3);
obj; //{"0":"a","1":"b","2":"c"}
```

{% hint style="info" %}
**Object.assign\(\) 常见用途**

1. 为对象添加属性
2. 为对象添加方法
3. 克隆对象
4. 合并多个对象
5. 为属性指定默认值
{% endhint %}



