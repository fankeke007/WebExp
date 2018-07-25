### 1.变量

Sass 为css 引入了变量，可以将反复使用的css属性值定义成变量，然后通过变量名来引用它们。

#### 变量声明语法

```css
//变量声明以 $ 符开头
$highlight-color : #F90;
$basic-boder : 1px solid black;
```

#### 变量的作用域

变量可以定义在规则块（大括号）之内也可以定义在规则块之外。定义的位置决定了其作用域也不一样。定义在规则块之内的只能在规则块之内使用。

#### 变量的引用

凡是css标准值可以存在的地方，都可以使用变量。编译.scss文件时，变量所在的位置会被它们的值所替代。改变变量的值后，所有引用此变量的地方生成的值会随之改变。

```css
$highlight-color : #F90;
.selected {
    border : 1px solid $highlight-color;
}
//编译后

.slected {
    border : 1px solid #F90;
}
```

#### 变量名中的中划线和下划线

在 sass 中，变量名的**中划线**和**下划线**可**相互替代**。见下：

```css
$link-color : blue;
a{
    color:$link_color;
}
//编译后
a{
    color:blue;
}
```

### 2.嵌套CSS规则

```css
/*正常css代码*/

#content article h1{color:#333}
#content article p{margin-bottom:1.4em}
#content aside{background-color:#EEE}
```

上述代码使用Sass的嵌套写法后：

```css
#content{
    article{
        h1{ color:#333 }
        p{ margin-bottom:1.4em }
    }
    aside{ background-color:#EEE }
}

//经Sass编译后为上述正常css代码，可以看出sass的写法更简洁更具表现力
```

#### 父选择器的标识符 &

使用方式一：（注意对比不使用** & **的效果）

```scss
article a{
    color:blue;
    &:hover{ color:red }
}
//编译后
article a{ color:blue }
article a:hover{ color:red }
```

使用方式二：

```scss
#content aside{
    color:red;
    body.ie & {color:green}
}
//编译后
#content aside{ color: red}
body.ie #content aside {color:green}
```

#### 群组选择器的嵌套

```scss
.container{
    h1,h2,h3{margin-bottom:0.8em}
}
//编译后
.container h1,.container h2,.container h3{margin-bottom:.8em}
```

#### 子组合选择器和同层组合选择器：&gt;、+ 和 ~

```scss
article{
    ~ article{border-top:1px solid #ccc}
    > section{background:#eee}
    dl > {
        dt{color:#333}
        dd{color:#555}
    }
    nav + & {margin-top:0}
}

//编译后
article ~ article {border-top:1px solid #ccc}
article > section {background:#eee}
article dl dt {color:#333}
article dl dd {color:#555}
nav + article { margin-top:0 }
```

#### 属性嵌套

Sass中除了css选择器嵌套，属性也可以嵌套。

属性嵌套的规则：把属性名从中划线-的地方断开，在根属性后边添加一个冒号** : **，紧跟一个**{ }**块，把子属性部分写在这个{ }块中。

```scss
nav {
    border:{
        style:solid;
        width:1px;
        color:#ccc;
        left:0;
        right:0;
    }
}

//编译后

nav { 
    border:1px solid #ccc;
    border-left:0;
    border-right:0; 

}
```

### 3.导入Sass 文件

有些Sass文件主要用于导入，你并不希望为每个这样的文件单独地生成一个css文件，Sass通过一个特殊的约定来解决。

#### 使用Sass部分（局部）文件 @import

Sass局部文件的**文件名以下划线开头**。这样，Sass就不会在编译时单独编译这个文件输出css，而只把这个文件用于导入。

当使用@import导入一个局部文件时，可以不用写全文件名，即可以省略文件名开头的下划线。

如导入themes/\_night-sky.scss这个局部文件，可以这样写：

```scss
@import "themes/night-sky";
```

#### 默认变量值 !default

通过@import导入sass文件时，希望可以修改被导入文件中的某些值，使用sass的** !default **标签可以实现这个目的。

```scss
//_a.scss
$fancybox-width:400px !default;
.fancybox{
    width:$fancybox-width;
}
```

若在导入\_a.scss之前声明了一个$fancybox-width变量，那么局部文件中的相同变量失效而启用用户声明的变量。否则，使用默认变量。

#### 嵌套导入

与原生css不同，sass允许@import命令写在css规则内，局部文件会被直接插到css规则内导入它的地方。

如，有一个\_blue-theme.scss的局部文件：

```scss
aside{
    background:blue;
    color:white;
}
```

将其导入到一个css规则内：

```scss
.blue-theme {@import "blue-theme"}

//编译后

.blue-them{
    aside{
        background:blue;
        color:#fff;
    }
}
```

#### 原生的css导入

在下列三种情况下会造成原生的CSS@import：（尽量避免，因为效率较低）

1. 被导入文件的名字以 .css 结尾
2. 被导入文件的名字是一个URL地址
3. 被导入文件的名字是css的url\(\)值

### 4.静默注释

```scss
body{
    color:#333;   //这种注释不会出现在生成的css文件中
    padding:0;    /*这种注释内容会出现在生成的css文件中 */
}
```

将 ! 作为多行注释的第一个字符表示在压缩输出模式下保留这条注释并输出到 CSS 文件中，通常用于添加版权信息。

> 目前为止，了解的保持sass条理性和可读性的最基本的三个方法：嵌套、导入和注释。

### 5.混合器 @mixin

变量不适合大段样式的重复使用，因而需要混合器。使用混合器可以把样式中的通用样式抽离出来，然后轻松的使用在其它地方。

```scss
@mixin rounded-corners {
    -moz-border-radius:5px;
    -webkit-border-radius:5px;
    -border-radius:5px;
}
```

可以通过@include来使用混合器

```scss
.notice{
    background-color:green;
    border:2px solid #00aa00;
    @include rounded-conrners;
}

//编译后
.notice{
    background-color:green;
    border:2px solid #00aa00;
    -moz-border-radius:5px;
    -webkit-border-radius:5px;
    -border-radius:5px;
}
```

#### 何时使用混合器

判断一组属性是否应该组合成一个混合器，一条经验法则就是你能否为这个混合器想出一个好的名字。若能找到一个很好的短名字来描述这些属性修饰的样式，比如 rounded-corners、fancy-font、no-bullets，那么往往能构造一个合适的构造器。若找不到，这时构造一个混合器可能并不合适。

#### 混合器中的css规则

混合器中不仅可以包含属性，也可以包含css规则，选择器和选择器中的属性。

```scss
@mixin no-bullets {
    list-style:none;
    li{
        list-style-image:none;
        list-style-type:none;
        margin-left:0px;
    }
    &:hover{
    background-color: #e8e8e8;
    }
    + h2{
    color:green;
    }
}
```

```scss
ul.plain {
    color:#444;
    @include no-bullets;
}

//编译后

ul.plain {
    color:#444;
    list-style:none;
}
ul.plain li{
    list-style-image:none;
    list-style-type:none;
    margin-left:0;
}
ul.plain:hover { 
    background-color: #e8e8e8; 
}
ul.plain + h2 { 
    color: green; 
}
```

#### 给混合器传参

可以通过在@include混合器时传参，来定制混合器生成的精确样式，这种方式和js的function很像。

```scss
@mixin link-colors($normal,$hover,$visited){
    color:$normal;
    &:hover{color:$hover;}
    &:visited{color:$visited;}
}
```

```scss
a{
    @include link-colors(blue,red,green);
}
//另一种（顺序无关的）传参形式
a{
    @include link-colors(
        $normal:blue,
        $visited:green,
        $hover:red
    )
}


//编译后

a{color:blue;}
a:hover{color:red;}
a:visted{color:green;}
```

#### 默认参数值

@mixin 定义混合器时可以使用$name:default-value的形式指定默认参数。

```scss
@mixin link-colors($normal,$hover:$normal,$visited:$normal){    
    color:$normal;
    &:hover{color:$hover;}
    &:visited{color:$visited;}
}
```

### 6.选择器继承 @extend

通过@extend语法可以实现一个选择器继承另一个选择器定义的所有样式。这个理念类似面向对象的css.

```scss
.error{
    border:1px solid red;
    background-color:#fdd;
}
.seriousError{
    @extend .error;
    border-width:3px;
}
```

.seriousError 不仅会继承.error 自身所有样式，任何跟.error有关的组合选择器样式也会被.seriousError 以组合选择器的形式继承。

```scss
//.seriousError 从 .error 继承样式
.error a{  //应用到.seriousError a
    color :red;
    font-weight:100;
}
h1.error{  //应用到h1.seriousError
    font-size:1.2rem;
}
```

#### 何时使用继承

**混合器**主要用于**展示性样式**的重用，**类名**用于**语义化样式**的重用。继承是基于类的，所以继承应该建立在语义化的关系上。当一个元素拥有类（如 .seriousError）表明它基于另一个类（如 .error），这时使用继承再合适不过了。

一个简化重复编码的演进过程：以.error和.seriousError 为例

* 最原始办法：为两个类分别写相同样式
* 改进一：使用选择器组（.error,.seriousError）给这两个选择器写相同的样式
* 改进二：使用混合器为这两个类提供相同的样式
* 改进三：使用@extend继承，使两者之间的关系非常清晰

#### 继承的高级用法

继承一个HTML元素的样式时，浏览器默认样式不会被继承（不属于样式表中的样式），但是用户对HTML元素添加的样式都会被继承。

若一条样式规则**继承了一个复杂的选择器**，那么它只会继承这个复杂选择器**命中的元素所应用的样式**。

#### 继承的工作细节

@extend 背后最基本的思想是，若 .seriousError @extend .error，那么样式表中的任何一处**.error**都用**.error ,.seriousError**这一选择器组进行替换。

关于@extend有两点需要知道：

1. 跟混合器相比，继承生成的css代码相对更少。因为继承仅仅是重复选择器，而不会重复属性，所以使用继承往往会比混合器生成的css体积更小。
2. 继承遵从css层叠规则。通常权重更高的选择器胜出，权重相同，定义在后边的规则胜出。

#### 使用继承最佳实践

1. 尽量不要再css规则中使用后代选择器（.foo .bar）去继承css规则。这样可能会导致选择器数量失控。
2. 继承 nested （选择器）规则会报错。**@extend .mian  .error**
3. 在和@media同时使用时，只能用在同层（都在@media内或外）之间，不能跨层

#### 占位符选择器 %（@extend-only）

有时需要定义一套样式并不是给某个元素用，而是只通过@extend指令使用，尤其是在制作Sass库时希望忽略用不到的样式。这时可以使用占位符选择器%。

```scss
//自身将不会被渲染
#context a%extreme{
    color:blue;
    font-weight:bold;
    font-size:2em;
}
.notice{
    @extend %extreme;
}

//编译为

#context a.notice{
    color:blue;
    font-weight:bold;
    font-size:2em;
}
```



