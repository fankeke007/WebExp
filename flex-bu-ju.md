参考：

1.[A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

2.[Flex 布局教程](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

> **The main idea behind the flex layout** is to give the container the ability to alter its items' width/height \(and order\) to best fill the available space \(mostly to accommodate to all kind of display devices and screen sizes\).

#### 术语

**table 中 '\|' 会被当做党员分隔符，导致布局混乱，因而换做 '/'**

| ![](/assets/flex-container.png) | ![](/assets/flex-items.png) |
| :--- | :--- |
| Properties for the Parent \(**flex cotainer**\) | Properties for the Children \(**flex items**\) |
| **display : **flex / inline-flex; | **order** : &lt;integer&gt;          /\*default value is 0\*/ |
| **flex-direction : **row / column / row-reverse / column-reverse; | **flex-grow** : &lt;number&gt;  /\* default value is 0\*/ |
| **flex-wrap : **nowrap / wrap / wrap-reverse; | **flex-shrink** : &lt;number&gt;   /\*default 1\*/ |
| **flex-flow :** &lt;'flex-direction'&gt; // &lt;'flex-wrap'&gt; | **flex-basis** : &lt;length&gt; / auto;  /\*default auto\*/ |
| **justify-content : **flex-start / flex-end / center / space-between / space-around / space-evenly; | **flex** : none / \[ &lt;'flex-grow'&gt;&lt;'flex-shrink'&gt;&lt;'flex-basis'&gt; \]  /\*default value **0 1 auto**\*/ |
| **align-items** : flex-start / flex-end / flex / center / baseline / strech; | **align-self** : auto / flex-start / flex-end / center / baseline / strech; |
| **align-content** : flex-start / flex-end / center / strech / space-between / space-around; |  |

##### 注意：

1. flex 容器的**align-content** 属性，当（flex items）只有一行时，是无效果的；
2. 对于flex items，float、clear、vertical-align 属性无效。

#### 浏览器前缀

由于flex规范随着时间推移而发生了变化，因而（属性或属性值）需要添加浏览器厂商前缀才能兼容更多的浏览器。一下是通过sass 的@mixin 提供的解决方案

```
@mixin flexbox(){
    display:-webkit-box;
    display:-moz-box;
    display:-ms-flexbox;
    display:-webkit-flex;
    display:flex;
}

@mixin flex($values){
    -webkit-box-flex:$values;
    -moz-box-flex:$values;
    -webkit-flex:$values;
    -ms-flex:$values;
    flex:$values;
}

@mixin order($val){
    -webkit-box-ordinal-group:$val;
    -moz-box-ordinal-group:$val;
    -ms-flex-order:$val;
    -webkit-order:$val;
    order:$val;
}

/*eg*/
.wrapper{
    @include flebox();
}

.item{
    @include flex(1 200px);
    @include order(2);
}
```

#### 应用（example）

[http://fankeke007.github.io/css/common-layout-ways/flex.html](http://fankeke007.github.io/css/common-layout-ways/flex.html)

