参考：

1. [MDN grid](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid)
2. [A Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
3. grid by examples

### Grid VS Flex

Flex ： 主要用于一维布局

Grid ：主要用于二维布局（row，column）

### 术语

**Grid Container**（栅格容器）：display属性设为grid的元素，它是grid items\(栅格元素/项目\)的直接父元素。

**Grid Item**（栅格元素/项目）：栅格容器的直接子元素（孙元素就不属于栅格元素了）。

**Grid Line** ：构成网格结构的分界线，它们可以是水平或者垂直的，并且可以位于行或者列的任一侧。

![](/assets/grid-line.png)

**Grid Track** ：两个相邻网格线之间的空间（类似于网格的行或者列）

![](/assets/grid-track.png)

**Grid Cell **：网格单元（两个相邻行和两个相邻列之间的空间）

![](/assets/grid-cell.png)

**Grid Area** ：网格区域

![](/assets/grid-area.png)

| **Properties for the Grid Container** | Properties for the Grid Items |
| :--- | :--- |
| **display**：grid / inline-grid; |  |
| **grid-templage-columns**：\[line-name\] &lt;track-size&gt; .../ \[line-name\] &lt;track-size&gt; |  |
| **grid-template-rows**：\[line-name\] &lt;track-size&gt; .../ \[line-name\] &lt;track-size&gt; |  |
| **grid-template-areas**："&lt;grid-area-name&gt; / . / none / ..." "..." |  |
| **grid-template** ：none / &lt;grid-template-row&gt; / &lt;grid-template-columns&gt; |  |
| **grid-column-gap** ：&lt;line-size&gt; |  |
| **grid-row-gap**：&lt;line-size&gt; |  |
| **grid-gap **：&lt;grid-row-gap&gt; &lt;grid-column-gap&gt; |  |
| **justify-items** : start \| end \| center \| streach; |  |
| **align-items** : start \| end \| center \| streach; |  |
| **place-items** : &lt;align-items&gt;/&lt;justify-items&gt;; |  |
| **justify-content** : start / end / center / strech / space-around / space-between / space-evenly; |  |
| **align-content** : start / end / center / strech / space-around / space-between / space-evenly; |  |
| **place-content** : &lt;align-content&gt;/&lt;justify-content&gt; |  |
| **grid-auto-columns** : &lt;track-size&gt; |  |
| **grid-auto-rows** : &lt;track-size&gt; |  |
| **grid-auto-flow** : row / column / dense |  |
| grid : |  |
|  |  |
|  |  |

#### 注意

1. 通过嵌套元素（也称为子网格）向下传递网格参数的能力已移至CSS网格规范的第2级

2. 定义Grid Line的名称需要使用\[name\]语法，一条Grid Line 可以有多个名称，中间用空格分开

3. 若定义colunms或rows时是重复内容，可以使用repeat\(\)函数简化写法

4. fr 单位可以允许设置track-size为可用空间（free-space）的一部分

5. 


