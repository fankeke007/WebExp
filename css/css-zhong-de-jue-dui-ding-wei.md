---
description: 绝对定位元素的宽度计算，以及没有定位值时的表现状态
---

# CSS中的绝对定位

## 绝对定位元素的宽度计算

绝对定位\(absolute\)与固定定位\(fixed\)元素**具有包裹性**。宽度是由内容撑开，而它的最大自适应宽度则是 **最近的定位属性为非static的父级元素** 的宽度减去定位元素的left或right的剩余宽度。

如图：

![&#x5B9A;&#x4F4D;&#x5143;&#x7D20;&#x7684;left&#x503C;&#x4E3A;40&#xFF0C;&#x7236;&#x7EA7;&#x5185;&#x5BB9;&#x533A;&#x5BBD;&#x5EA6;98&#xFF0C;&#x5B9A;&#x4F4D;&#x5143;&#x7D20;&#x5269;&#x4F59;&#x6700;&#x5927;&#x5BBD;&#x5EA6;&#x6B63;&#x597D;&#x7B49;&#x4E8E;98-40=58](../.gitbook/assets/3.png)

改变left值时：

![&#x73B0;&#x5728;left&#x503C;&#x4E3A;100&#xFF0C;&#x6700;&#x5927;&#x5BBD;&#x5EA6;&#x4E3A;98-100&#x5DF2;&#x7ECF;&#x662F;&#x8D1F;&#x503C;&#xFF0C;&#x6240;&#x4EE5;&#x5BBD;&#x5EA6;&#x5219;&#x4E3A;&#x5B57;&#x4F53;&#x5927;&#x5C0F;&#x7684;&#x5BBD;&#x5EA6;14](../.gitbook/assets/4.png)

添加white-space: nowrap; 样式或固定宽度可让定位元素宽度符合预期。

## 没有定位值时的表现状态

当元素设置absolute定位，但不设置任何偏移属性时。元素相对于**行框顶部**对齐

如图所示：

![&#x5B9A;&#x4F4D;&#x524D;&#xFF1A;&#x4E00;&#x884C;&#x663E;&#x793A;&#xFF0C;&#x57FA;&#x7EBF;&#x5BF9;&#x9F50;&#x3002;](../.gitbook/assets/5.png)

![](../.gitbook/assets/6%20%281%29.png)

