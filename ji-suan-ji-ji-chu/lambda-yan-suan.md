---
description: lambda 演算相关知识速览
---

# lambda 演算

参考链接：[cgnail's weblog](http://cgnail.github.io/academic/lambda-1/)

#### **1.lambda 演算语法**

```javascript
//函数定义:一个参数为x的函数，返回值为body的计算结果
lambda x.body
//标识符引用：标识符引用就是一个名字，这个名字用于匹配函数表达式中的某个参数名
//函数应用：函数应用把函数值（函数定义表达式）放到它的参数前面
(lambda x.plus x x)y
```

{% hint style="info" %}
**柯里化**

 lambda演算中的一个技巧：一个函数（lambda表达式）只接受一个参数的情况下怎么实现加法？答案是柯里化：函数返回一个带一个参数的函数，这样就可以实现两个参数的函数了。

```text
lambda x.(lambda y.plus x y)
```
{% endhint %}

{% hint style="info" %}
**自由标识符 VS 绑定标识符**

在对一个lambda演算表达式进行求值的时候，不能引用任何未绑定的标识符。如果一个标识符是一个闭合的lambda表达式的参数，我们称这个标识符是（被）绑定的（绑定标识符）；若一个标识符在任何上下文中都没有绑定，那么它是自由变量（自由表示符）。

```text
lambda x.plus x y
//这个表达式中plus和y是自由的，x是绑定的
```

```text
lambda x y.y x
//这个表达式中x,y都是绑定的
```

```text
lambda y.(lambda x.plus x y)
//在内层表达式中y和plus是自由的
//在完整表达式中，x,y是绑定的，plus仍是自由的
```

**常使用free\(x\)，来表示表达式中自由的标识符x**。

**一个lambda演算表达式中只有所有的变量都是绑定的时候才是合法的。但是，当我们脱离上下文，关注一个复杂表达式的子表达式时，自由变量是允许存在的。**
{% endhint %}

#### 2.lambda演算运算法则

lambda演算只有两条真正法则：Alpha 和 Beta。Alpha被称为【转换】，Beta被称为【规约】。

```javascript
//Alpha 转换

//变量的名称是不重要的：给定lambda演算中的任意表达式，
//我们可以修改函数参数的名称，只要我们同时修改函数体内
//所有对它的自由引用。

lambda x.if(=x 0) then 1 else x^2

//使用Alpha转换，将x变为y（写作alpha[x/y]）,一下演算式完全等价
lambda y.if(=y 0) then 1 else y^2

//这样丝毫不会改变表达式的含义，但这一点很重要，因为它使得我们可以实现比如递归之类的事情
```

```text
//Beta 规约

//Beta 规约使得lambda演算能够执行任何可以由机器来完成的计算。
//Beta 规约：假设有一函数表达式：“(lambda x.x+1)3”。我们可以
//通过替换函数体（即“x+1”）来实现函数应用，用数值“3”取代引用的参数“x”。
//于是Beta 规约的结果就是：“3+1”

(lambda x y.x y)(lambda z.z*z) 3
//3*3
```

{% hint style="warning" %}
Beta 规约

```text
//lambda 规约的形式化写法
lambda x.B e = B[x := e] if free(e) subset free(B[x := e])
```

最后的条件“**if free\(e\) subset free\(B\[x := e\]\)**”说明了为什么我们需要Alpha转换：**我们只有在不引起绑定标识符和自由标识符之间的任何冲突的情况下，才可以做Beta规约**：**如果标识符“z”在“e”中是自由的，那么我们就需要确保，Beta规约不会导致“z”变成绑定的。如果在“B”中绑定的变量和“e”中的自由变量产生命名冲突，我们就需要用Alpha转换来更改标识符名称，使之不同。**

```text
(lambda z . (lambda x . x + z)) (x + 2) //参数“x+2”中，x是自由的，若我们不遵守规则直接做Beta规约，得到结果如下//lambda x.x+x+2//使得原先在“x+2”中的自由变量现在变绑定了,假设我们再应用该函数：//(lambda x.x+x+2)3//结果：3+3+2//若我们按照应有的方式先采用Alpha转换，如下：//step1:alpha[x/y](lambda z.(lambda y.y + z))(x+2)//step2:Beta 规约(lambda y.y+x+2)3//step3:再次Beta 规约//结果：3+x+2
```
{% endhint %}



