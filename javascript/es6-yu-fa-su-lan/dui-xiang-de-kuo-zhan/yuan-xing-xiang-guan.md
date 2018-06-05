# 原型相关

* \_\_proto\_\_
* Object.setPrototypeOf\(\)
* Object.getPrototypeOf\(\)

**1.\_\_proto\_\_**

在es6之已经被各大浏览器厂商实现，但是es6将其纳入标准。

{% hint style="danger" %}
通过这个属性，可以改变一个对象的\[\[Prototype\]\]属性，这种行为在每一个JavaScript引擎和浏览器中都是一个非常慢且影响性能的操作。使用这种方式来改变和继承属性是对性能影响非常严重的。

**不推荐使用这个属性，在浏览器之外的其他环境可能不支持**。

推荐使用：Object.setPrototypeOf\(\)【写操作】、Object.getPrototypeOf\(\)【读操作】、Object.create\(\)【生成操作】代替\_\_proto\_\_.
{% endhint %}

**2.Object.setPrototypeOf\(\)**

作用与\_\_proto\_\_相同，用来设置一个对象的prototype对象。它是es6正式推荐的设置原型对象的方法。

**3.Object.getProtorypeOf\(\)**

用于读取一个对象的原型

