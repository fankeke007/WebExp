### 根节点

**document 和 document.documentElement ?**

document：文档接口表示加载在浏览器中的网页，并充当网页内容\(DOM树\)的入口点。DOM树包括许多元素，如&lt;body&gt;和&lt;table&gt;等。它为文档提供全局功能，比如如何获取页面的URL并在文档中创建新元素。

```js
document.nodeType;        // 9 : document_node , 指代文档
document.documentElement; // 8 : element_node , 指代 html 根元素
```

### 父节点

1. **parentNode   **        
2. parentElement     （老版ie,DOM4）（注意element是一个限制\)

### 子节点

[**HTMLCollection VS NodeList**](https://www.jianshu.com/p/f6ff5ebe45fd "HTMLCollection 和 NodeList的区别")** **&&** node.children VS node.childNodes  && **[**element VS node**](https://blog.csdn.net/kkkkkxiaofei/article/details/52608394 "element 和 node 的区别")

先关参考[大漠《动态集合》](https://www.w3cplus.com/javascript/dom-dynamic-collection.html)

HTMLCollection ：只包含元素节点。相较 NodeList 多了一个namedItem方法

NodeList ： 可以包含所有节点。

1. **childNodes：**返回所有子节点，返回结果为NodeList（包括文本节点）（缩进会造成空白的文本节点）
2. **firstChild**
3. **lastChild**
4. **children：**返回所有元素子节点，返回结果为HTMLCollection（不包括元素子节点）
5. firstElementChild
6. lastElementChild

### 兄弟节点

1. previousSibling
2. nextSibling
3. previousElementSibling
4. nextElementSibling

### **节点之间的关系总结图**（大漠《理解DOM》）

![](/assets/understander-dom-41.png)

### 深度优先与广度优先

参考[《querySelectorAll 和 getElementsByTagName区别》](https://www.w3cplus.com/javascript/querySelectorAll-vs-getElementsByTagName.html)、[《深度优先遍历与广度优先遍历》](https://kurobane.me/2018/03/09/DFS-BFS/)

![](/assets/querySelectorAll-getElementsByTagName-1.png)![](/assets/querySelectorAll-getElementsByTagName-2.png)

供遍历测试的html结构：

```html
    <div class="root">
        <div class="container">
            <section class="sidebar">
                <ul class="menu">
                    <li> <a>深度遍历</a> </li>
                    <li> <a>广度遍历</a> </li>
                </ul>
            </section>
            <section class="main">
                <article class="paragraph"></article>
                <p class="note"></p>
            </section>
        </div>
    </div>
```

深度优先遍历：

```js
function dfs(node){
    if(!node){
        return;
    }
    var deep = arguments[1] || 1;
    console.log(node.nodeName,node.classList,deep);
    if(!node.children.length){
        return;
    }
    var children = node.children;
    var length = children.length;
    if(!length){
        return;
    }
    for(var i=0;i<length;i++){
        dfs(children[i],deep+1);
    }
}
```

广度优先遍历：

```js
function bfs(node){
    if(!node){
        return;
    }
    var deep = arguments[1]||1;
    var queen = [
        {
            item:node,
            deepth:1
        }
    ];
    while(queen.length){
        var node = queen.shift();
        console.log(node.item.nodeName,node.item.classList,node.deepth);
        var children = node.item.children;
        var length = children.length;
        if(!length){
            continue;
        }
        for(var i=0;i<length;i++){
            queen.push({
                item:children[i],
                deepth:node.deepth+1
            })
        }
    }
}
```



