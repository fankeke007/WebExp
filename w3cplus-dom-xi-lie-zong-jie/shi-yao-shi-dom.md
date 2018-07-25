> 来之灵魂深处的拷问：如何向前端小白讲清DOM？

## 什么是DOM？

DOM（Document Object Model），即文档对象模型。

> DOM 提供了**对文档（html/xml）的结构化的表述**，并定义了一种方式可以在程序中对文档结构进行访问，从而改变文档的结构、样式和内容。
>
> **DOM 将文档解析为一个由节点和对象**（包含属性和方法的对象）**组成的结构集合**。简言之，**DOM将 web 页面和脚本或程序语言连接起来**。
>
> -- MDN《DOM 概述》

---

> 一个 web 页面就是一个文档，这个文档在浏览器中可以有两种展现方式：网页 或 源码。但上述两种情况中都是同一份文档。DOM 提供了对同一份文档的另一种呈现，存储和操作的方式。DOM 是web页面的完全的面向对象的表述，它能够使用如JavaScript、python等脚本语言进行修改。
>
> -- MDN《DOM 概述》

---

> DOM 和HTML源代码的区别？
>
> 两种情况会导致浏览器生成的DOM和HTML源代码不同：  
> 1. DOM被客户端JavaScript修改  
> 2. 浏览器会自动修复源代码中的错误

---

> DOM 被设计成与特定的编程语言相独立，使文档的结构化表述可以通过单一、一致的API获得。

**个人总结：DOM 是页面的HTML、CSS 、JavaScript联合起来后页面 对象化，结构化 的综合体现。**

参见《浏览器原理总结》（结合浏览器工作原理解释）

## DOM 遍历

参见[《DOM 遍历》](/w3cplus-dom-xi-lie-zong-jie/dom-bian-li.md)

## DOM 修改

参见[《DOM 查、增、改、删》](/w3cplus-dom-xi-lie-zong-jie/dom-cha-3001-zeng-3001-gai-3001-shan.md "操控（修改）DOM")

### 

文档参考：

【1】[MDN《DOM 概述》](https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model/Introduction)

【2】[Understanding the DOM](https://www.digitalocean.com/community/tutorial_series/understanding-the-dom-document-object-model)

【3】[理解 DOM](https://www.w3cplus.com/javascript/understanding-the-dom.html)

