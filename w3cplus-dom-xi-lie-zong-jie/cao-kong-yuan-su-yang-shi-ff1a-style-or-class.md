> 本篇文档主要总结js操作元素样式改变的两大类方法：class-and-style

[样式和类](#style-and--class)

* [直接设置style](#style)
* [通过 className 和 classList 控制样式](#class)
* [样式和类操作总结](#summary)

## 样式和类 {#style-and--class}

前端页面的交互（UI效果的变化）常常会通过如下两种方式来实现：

1. 在 HTML 元素上添加类名，然后再 CSS 样式文件中处理样式
2. 通过 JavaScript 控制 HTML 元素的 style 属性改变元素样式

两种方式的优劣比较：

* 通过添加或删除class能使得样式与表现分离 ；

* 通过style属性能完成某些class不能达到的效果（动态计算与设置元素坐标）；

```js
elem.style.left = left;
elem.style.top = top ;
```

### **直接设置style** {#style}

[CSSStyleDeclaration](https://developer.mozilla.org/zh-CN/docs/Web/API/CSSStyleDeclaration) ：表示一个CSS 属性键值对的集合。

CSSSTyleDeclaration 接口可以用来操做元素的样式，常见的方式（接口）有：

* 元素节点的style属性，即HTMLElement.style
* CSSStyle 实例的 style 属性，即 HTMLElement.style.cssText
* window.getComputedStyle\(\)

```js
//HTMLElement.style
//style 是 HTML 元素的一个标签属性，它也是元素的节点，可以通过
//getAttribute/setAttrubute/removeAttribute 的方式来读写或删除DOM元素的属性

document.querySelector('div').setAttribute(
    'style',
    'background-color: orange; z-index: 9999; border-left-width: 5px;'
)
```

```js
//HTMLElement.style.cssText 
//可以通过 HEMLElement.style.property = value 的方式给style属性添加样式，
//但对一个元素需添加多个属性值时需要多次写，这样大大降低开发效率，
//CSSStyleDeclaration 的 HTMLElement.style.cssText属性用来读写当前元素的style值

//此种方式将会覆盖对象原有的style属性
document.querySelector('div').style.cssText = "color: rgb(255, 51, 102); font-size: 2rem; padding: 10px;"

//可以通过如下变通，使得原有style属性不被覆盖
document.querySelector('div').style.cssText += "color: rgb(255, 51, 102); font-size: 2rem; padding: 10px;"

//删除元素样式
document.querySelector('div').style.cssText = '';
```

```
//window.getComputedStyle() 
//浏览器解析CSS 样式一共有5个来源（行内、style标签、link标签、浏览器默认、浏览器用户自定义）
//js通过getComputedStyle(elem) 可以获取浏览器计算后的最终样式（只读）

window.getComputedStyle(document.querySelector('h1'),[null]);//可选的null兼容老版本
window.getComputedStyle(document.querySelector('h1'));

//通过传入第二个参数可以获取【伪元素】的样式（通过style无法获取伪元素样式）
window.getComputedStyle(document.querySelector('h1'),':before');
```

### 通过 className 和 classList 控制样式 {#class}

对与不支持classList的老旧浏览器（IE9及以下），可通过类似jquery封装addClass\(\)和removeClass\(\)方法，完成对元素class的增删。对于支持classList的浏览器，直接利用classList对象属性与方法即可。

### 样式和类操作总结 {#summary}

* 通过DOM Element对象的getAttribute\(\)、setAttribute\(\)和removeAttribute\(\)等方法修改元素的style属性
* 通过对元素节点的style来读写行内CSS样式
* 通过style对象的cssText属性来修改全部的style属性
* 通过style对象的setProperty\(\)、getPropertyValue\(\)、removeProperty\(\)等方法来读写行内CSS样式
* 通过window.getComputedStyle\(\)方法获得浏览器最终计算的样式规则
* 通过className或classList给元素添加或删除类名，配合样式文件来修改元素样式



