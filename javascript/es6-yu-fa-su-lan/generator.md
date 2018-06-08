# Generator

1.概述

Generator 函数时 es6 提供的一种异步编程解决方案。

**语法上**可将Generator函数理解成一个状态机，封装了多个内部状态。

**形式上**，Generator函数是一个普通函数，但是有两个特征：**1.function关键字和函数名之间有一个星号**；**2.函数体内部使用yield表达式，定义不同的内部状态**。

**执行Generator函数会返回一个遍历器对象**。返回的遍历器对象可依次遍历Generator函数内部的每一个状态。

Generator函数调用的方法和普通函数一样，也是在函数名后面加上一对圆括号。不同的是，**调用Generator函数后，该函数并不执行，返回的也不是函数运行结束时的结果，而是一个指向内部状态的指针对象（即遍历器对象）**。

下一步，必须调用遍历器对象的next方法，使得指针移向下一个状态。直到遇到下一个yield表达式（或return）为止。换言之，Generator函数是分段执行的，yield表达式是暂停执行的标记，而next方法可以恢复执行。

总结：调用Generator函数，返回一个遍历器对象，代表Generator函数的内部指针。以后，每次调用next方法，就会返回一个有value和done两个属性的对象。value属性表示当前内部状态的值，是yield表达式后面那个表达式的值；done属性是一个布尔值，表示是否遍历结束。

{% hint style="info" %}
**yield VS return**

相似：都能返回紧跟在语句后面的那个表达式的值。

区别：每次遇到yield，函数暂停执行，下一次再从该位置继续向后执行。而return语句不具备位置记忆的功能。一个函数里，只能执行一次return语句，但是可以执行多次（多个）yield表达式。Generator函数可以返回一系列值，因为可以有任意多个yield。
{% endhint %}

{% hint style="warning" %}
yield使用的几点注意

1. yield表达式只能用在Generator函数里面，用在其他地方会报错
2. yield表达式若用在另一个表达式之中，必须放在圆括号里面
3. 
{% endhint %}

