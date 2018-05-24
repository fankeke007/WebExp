---
description: 元素在文档中的位置、元素在当前视窗中的位置、元素自身的尺寸信息
---

# 元素在文档中尺寸与位置相关信息汇总

### **概览**

![&#x56FE;1.&#x5143;&#x7D20;&#x5728;&#x6587;&#x6863;&#x4E2D;&#x5C3A;&#x5BF8;&#x4E0E;&#x4F4D;&#x7F6E;&#x5173;&#x7CFB;&#x56FE;&#xFF08;MSDN&#xFF09;](../.gitbook/assets/image%20%284%29.png)

图1说明：页面中主要包含3个元素：红色的div元素、蓝色div元素\(红色div的父元素\)、黑色轮廓的html元素。蓝色div主要目的是定义构成元素布局的不同级联样式表（CSS）框，以及显示如何计算**offsetTop**属性。视口是由**html**元素表示。在图中html元素没有显示任何边距或边框。但是，添加边距或边框不会改变任何测量结果。由于蓝色div的**overflow**属性已设置为“滚动”，并且它包含的内容数量超过了可在其有限的客户端区域内显示的内容，因此会显示滚动条。请注意，所示的值都是面向**垂直**的属性。水平取向的属性是相似的; 只需将“left”替换为“top”，将“width”替换为“height”。

> 涉及的属性与方法
>
> * getClientRects\(\)
> * getBoundingClientRects\(\)
> * getComputedStyle\(\)
> * scrollTop
> * offsetTop
> * scrollHeight
> * clientHeight
> * offsetHeight
> *

获取文档滚动高度\(即浏览器窗口滚动高度\)

```javascript
/*document.body.scrollTop 在页面不存在DTD声明时有用*/
document.documentElement.scrollTop || document.body.scrollTop
```

获取视窗（浏览器内容区窗口）大小

```text
document.documentElement.clientHeight
document.documentElement.clientWidth

//document.body.clientHeight 会获取整个文档的高度其值和document.documentElement.scrollHeight值接近
//存在的差异主要在于margin
```



获取文档尺寸

```javascript
Math.max(document.docuemntElement.scrollHeight,document.body.scrollHeight)
```

**scrollHeight**

一个元素内容高度的度量，包括溢出导致的视图中不可见内容（如：限制height，出现滚动条的内容高度）。 没有垂直滚动条的情况下，scrollHeight值与元素视图填充所有内容所需要的最小值clientHeight相同。包括元素的padding，但**不包括元素的border和margin**。scrollHeight也包括 [`::before`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::before) 和 [`::after`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::after)这样的伪元素。

![&#x4E0D;&#x5305;&#x542B;border&#x548C;margin&#x503C;](../.gitbook/assets/image%20%283%29.png)



document.documentElement  和 document.body 的尺寸在什么时候不一样？存在么？

**判断有滚动条的元素是否滚动到底部**

```javascript
//el:dom元素
//return:Boolean
//TODO：新增distance参数，判断距离底部多远
function isBottom(el){
    return el.scrollHeight - el.scrollTop === el.clientHeight
}
```

使用示例：（MDN）[判断用户是否阅读过文本](https://codepen.io/pen/)

**getBoundingClientRects VS** **getClientRects**

#### **getBoundngClientRects** : \(IE8+\)

![getBoundingClientRects&#x8FD4;&#x56DE;&#x503C;&#x793A;&#x610F;&#x56FE;&#xFF08;MDN&#xFF09;](../.gitbook/assets/image%20%285%29.png)

top/left/right/bottom都是**基于视窗**的值（与滚动相关），width/height元素自身的宽与高\(含border，不含margin\)。要想知道元素基于文档的位置只需加上相应的视窗滚动的位置（**window.scrollY/window.scrollX** ; **window.pageYOffset/window.pageXOffset** ; **document.documentElement.scrollTop/document.documnetElement.scrollLeft**）即可。

#### **getClientRects**:

对于块状元素使用与getBoundingRects一致。对于行内元素，若跨多行则每一行都会返回一个DOMRect 对象，最终返回的是一个DOMRect集合。一般推荐使用getBoundingRects来获取元素相对于视窗的位置属性。

#### **getComputedStyle**：**\(IE9+\)**

其返回值中width和height属性，只包含内容的宽与高，不包含padding、border、margin

```text
//使用方法
window.getComputedStyle(domObj)
```

参考链接：

{% embed data="{\"url\":\"https://developer.mozilla.org/zh-CN/docs/Web/API/CSS\_Object\_Model/Determining\_the\_dimensions\_of\_elements\",\"type\":\"link\",\"title\":\"Determining the dimensions of elements\",\"description\":\"当想要确认元素的宽高时有几种属性可以选择，但是我们很难确认使用哪个属性才是最适合的。本文将帮助你做出正确的选择。\",\"icon\":{\"type\":\"icon\",\"url\":\"https://developer.mozilla.org/static/img/favicon144.e7e21ca263ca.png\",\"width\":144,\"height\":144,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://developer.mozilla.org/static/img/opengraph-logo.72382e605ce3.png\",\"width\":600,\"height\":600,\"aspectRatio\":1}}" %}

{% embed data="{\"url\":\"https://msdn.microsoft.com/en-us/library/hh781509\(VS.85\).aspx\",\"type\":\"link\",\"title\":\"Measuring Element Dimension and Location with CSSOM in Windows Internet Explorer 9 \(Internet Explorer\)\",\"icon\":{\"type\":\"icon\",\"url\":\"https://msdn.microsoft.com/favicon.ico\",\"aspectRatio\":0}}" %}



