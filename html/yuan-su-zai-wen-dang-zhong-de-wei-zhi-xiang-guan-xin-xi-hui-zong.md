---
description: 元素在文档中的位置、元素在当前视窗中的位置、元素自身的尺寸信息
---

# 元素在文档中的位置相关信息汇总

> 涉及的属性与方法
>
> * getClientRects\(\)
> * getBoundingClientRects\(\)
> * scrollTop

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

判断有滚动条的元素是否滚动到底部

```javascript
//el:dom元素
//return:Boolean
//TODO：新增distance参数，判断距离底部多元
function isBottom(el){
    return el.scrollHeight - el.scrollTop === el.clientHeight
}
```

