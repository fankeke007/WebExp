### 创建节点

1. createElement\(\)
2. createTextNode\(\)
3. node.textContent    （ie9+）\(ie8 [Ployfill](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/textContent#Polyfill_for_IE8)\)
4. node.innerHTML      （**innerText **IE6+）

### 插入节点

1. node.**appendChild**\(\)

2. node.**insertBefore**\(newNode,refrenceNode\)

3. node.**replaceChild**\(new,old\)          （replaceWith 和 replaceNode）

4. insertAdjacentHTML\(\)     \(stage：WD\)

新的DOM API（IE 不支持）

* append\(\)
* prepend\(\)
* before\(\)
* after\(\)
* node.replaceWith\(\)

### 删除节点

1. node.removeChild\(\)：删除指定子节点
2. node.remove\(\)：把自身从所属的DOM树删除（IE、Safri 未实现）

### 克隆节点

1. **node.cloneNode**\(deep\)：克隆节点   \(deep 是否深度克隆，为true则该节点的所有后代节点也都会被克隆；为false则只会克隆节点本身\)（克隆一个节点会拷贝它所有的属性即属性值，但是通过js动态绑定的事件不会被拷贝）

### 可靠地DOM 属性与方法汇总：

来源[ Can I Use](https://caniuse.com/#search=replaceChild)

![](/assets/DOM Well Suported.png)

### 查找节点

**参考**大漠[《getElement\* 和 querySelector\*》](https://www.w3cplus.com/javascript/searching-elements-dom.html)、[《querySelectAll 和 getElementsByTageName 区别》](https://www.w3cplus.com/javascript/querySelectorAll-vs-getElementsByTagName.html)、[《动态集合》](https://www.w3cplus.com/javascript/dom-dynamic-collection.html)

1. document.getElementById\(\)
2. document.getElementsByClassName\(\)
3. document.getElementsByTagName\(\)
4. document.getElementsByName\(\)
5. document.querySelector\(\)
6. document.querySelectorAll\(\)

以下兼容性不高：

1. elem.matches\(\)：检查elem是否匹配指定的css选择器

2. elem.closest\(\)：查找指定css选择器最近的祖先
3. elemA.contains\(elemB\)：检查elemA 是否包含 elemB,若包含就返回true

**DOM中获取元素或节点六中常用方法汇总**：

| 方法 | 参数 | 是否调用一个元素 | 返回结果**是否动态** |
| :--- | :--- | :--- | :--- |
| document.getElementById\(\) | id |  |  |
| document.getElementsByName\(\) | name |  | √ |
| document.getElementsByTagName\(\) | tag 或 \* | √ | √ |
| document.getElementsByClassName\(\) | class | √ | √ |
| document.querySelector\(\) | CSS selector | √ |  |
| document.querySelectorAll\(\) | CSS selector | √ |  |

**动态集合 VS 静态集合**

DOM 中的集合：节点结合（NodeList）、元素属性集合（NameNodeMap）（动态）、HTML元素集合（HTMLCollection），三者均为类数组对象。

动态集合：会随着DOM的变化而变化

静态集合：选定之后保存当前快照（需要存储当前状态），不会随DOM修改而变化。

返回动态集合和静态集合的两个典型代表：

document.getElementsByTagName\(\) ：返回动态结合，速度较快

document.querySelectorAll\(\)：返回静态集合，速度较慢



