> **DOM 节点的全部属性和方法都是继承的结果**。

![](/assets/dom-node-properties-1.png)

图1.[DOM 继承树](https://www.w3cplus.com/javascript/node-properties-type-tag-and-contents.html)

**对继承树的解释**：

* **EventTarget**：是 root **抽象类**，各类永远不会创建实例。它作为一个基础所有DOM 节点都是其后代，从其继承了Event接口。
* **Node**：也是一个**抽象类**，作为DOM节点的基础。他提供了核心功能：parentNode、nextSibling、childNodes 等。Text、Element、Comment 都继承自Node类。
* **Element**：是DOM的基本类。它提供了元素级的收索，如 nextElementSibling、children、getElementById、querySelector等。在浏览器中不仅有HTML，还有XML、SVG文档。**元素类是更具体的类的一些基础**，如 SVGElement、XMLElement 和 HTMLElement。
* **HTMLElement**：是HTML元素的基本类，它由各种HTML元素继承。如 HTMLInputElement、HTMLBodyElement、HTMLAnchorElement等。

如 DOM 对象中的 &lt;input&gt; 元素，它属于 HTMLElement 类中的 HTMLInputElement 类。**其属性和方法是其自身和继承链上类的属性和方法的累加**：

* HTMLInputElement：提供了 input 特定的属性
* HTMLElement：提供常用的HTML元素方法（getter、setter）
* Element：提供元素通用方法
* Node：提供公共的DOM节点属性
* EventTarget：提供对事件的支持
* 最后他继承了 Object 的方法（纯对象），如 hasOwnProperty

**主要的DOM节点属性**：

1. **nodeType**：用于判断节点类型（如 判断一个节点是文本节点还是元素节点）。
2. **nodeName / tagName**：tagName 只用于元素节点，对于非元素节点使用nodeName来描述。
3. **innerHTML**：获取HTML元素内容（包含元素标签）。
4. **outerHTML**：获取元素完整的 HTML 内容。若修改其内容将导致元素自身被替换。
5. **nodeValue/data**：非元素节点的内容（文本、注释）。这两个几乎一样。
6. **textContent**：获取元素的文本内容，基本上是减去HTML所有的标签。它也具有写入性，可以将文本内容翻入元素中， 所有特殊的字符和标记都被精确的处理为文本。

**几个重要的节点的nodeType值**：

| 节点类型 | 字符常量 | 数值常量 |
| :---: | :---: | :---: |
| **元素**节点 | Node.ELEMENT\_NODE | 1 |
| **属性**节点 | Node.ATTRIBUTE\_NODE | 2 |
| **文本**节点 | Node.TEXT\_NODE | 3 |
| **文档**节点 | Node.DOCUMENT\_NODE | 9 |
| **注释**节点 | Node.COMMENT\_NODE | 8 |



