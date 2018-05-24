---
description: 元素在文档中的位置、元素在当前视窗中的位置、元素自身的尺寸信息
---

# 元素在文档中尺寸与位置相关信息汇总

### **概览**

![&#x56FE;1.&#x5143;&#x7D20;&#x5728;&#x6587;&#x6863;&#x4E2D;&#x5C3A;&#x5BF8;&#x4E0E;&#x4F4D;&#x7F6E;&#x5173;&#x7CFB;&#x56FE;&#xFF08;MSDN&#xFF09;](../.gitbook/assets/image%20%284%29.png)

图1说明：页面中主要包含3个元素：红色的div元素、蓝色div元素\(红色div的父元素\)、黑色轮廓的html元素。蓝色div主要目的是定义构成元素布局的不同级联样式表（CSS）框，以及显示如何计算**offsetTop**属性。视口是由**html**元素表示。在图中html元素没有显示任何边距或边框。但是，添加边距或边框不会改变任何测量结果。

由于[**div**](https://msdn.microsoft.com/en-us/library/ms535240%28v=vs.85%29.aspx)的[**overflow**](https://msdn.microsoft.com/en-us/library/ms530824%28v=vs.85%29.aspx)属性已设置为“滚动”，并且它包含的内容数量超过了可在其有限的客户端区域内显示的内容，因此会显示滚动条。请注意，所示的值都是面向_垂直_的属性。水平取向的属性是相似的; 只需将“左”替换为“顶”，将“宽”替换为“高”，等等。

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

获取文档滚动高度

```javascript
/*document.body.scrollTop 在页面不存在DTD声明时有用*/
document.documentElement.scrollTop || document.body.scrollTop
```

获取视窗（浏览器窗口）大小



获取文档尺寸

```javascript
Math.max(document.docuemntElement.scrollHeight,document.body.scrollHeight)
```

scrollHeight

一个元素内容高度的度量，包括溢出导致的视图中不可见内容（如：限制height，出现滚动条的内容高度）。 没有垂直滚动条的情况下，scrollHeight值与元素视图填充所有内容所需要的最小值clientHeight相同。包括元素的padding，但不包括元素的border和margin。scrollHeight也包括 [`::before`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::before) 和 [`::after`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::after)这样的伪元素。

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



