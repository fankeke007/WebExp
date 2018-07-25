### 1.@at-root

@ at-root指令导致在文档的根目录下生成一个或多个规则，而不是嵌套在其父选择器下面。它可以与单个内嵌选择器一起使用

```scss
.parent{
    ...
    @at-root{
        .child1{...},
        .child2{...}
    }
    .step-child{...}

}

//编译为

.parent{...}
.child1{...}
.child2{...}
.parent .step-child{...}
```

#### @at-root\(without:...\) and @at-root\(with:...\)

```scss
@meida print{
    .page{
        width:8in;
    }
    @at-root(without:media){
        color:red
    }
}

//编译为

@media print{
    .page{
        width:8in;
    }
}
.page{
    color:red;
}
```

### 2.@debug

@debug指令将SassScript表达式的值打印到标准错误输出流。这对于调试有复杂SassScript的Sass文件很有用

### 3.指令控制

#### @if  and @else if

```
$type: monster;
p {
  @if $type == ocean {
    color: blue;
  } @else if $type == matador {
    color: red;
  } @else if $type == monster {
    color: green;
  } @else {
    color: black;
  }
}

//编译为

p {
  color: green; 
}
```

#### @for  （to : exclude end）\(through : include end\)

@for 指令可以在限制的范围内重复输出格式，每次按要求（变量的值）对输出结果做出变动。

这个指令包含两种格式：@for $var from &lt;start&gt; through &lt;end&gt;，或者 @for $var from &lt;start&gt; to &lt;end&gt;，区别在于 through 与 to 的含义：当使用 through 时，条件范围包含 &lt;start&gt; 与 &lt;end&gt; 的值，而使用 to 时条件范围只包含 &lt;start&gt; 的值不包含 &lt;end&gt; 的值。另外，$var 可以是任何变量，比如 $i；**&lt;start&gt; 和 &lt;end&gt; 必须是整数值**。

```scss
@for $i from 1 through 3 {
    .item-#{$i}{width:2em*$i}
}

//编译为

.item-1 { width: 2em; }
.item-2 { width: 4em; }
.item-3 { width: 6em; }
```

#### @each

@each 指令的格式是 $var in &lt;list&gt;, $var 可以是任何变量名，比如 $length 或者 $name，而 &lt;list&gt; 是一连串的值，也就是值列表.

```scss
@each $animal in puma, sea-slug, egret, salamander {
  .#{$animal}-icon {
    background-image: url('/images/#{$animal}.png');
  }
}

//编译为
.puma-icon { background-image: url("/images/puma.png"); }
.sea-slug-icon { background-image: url("/images/sea-slug.png"); }
.egret-icon { background-image: url("/images/egret.png"); }
.salamander-icon { background-image: url("/images/salamander.png"); }
```

**多重分配**

```scss
@each $animal, $color, $cursor in (puma, black, default),
                                  (sea-slug, blue, pointer),
                                  (egret, white, move) {
  .#{$animal}-icon {
    background-image: url('/images/#{$animal}.png');
    border: 2px solid $color;
    cursor: $cursor;
  }
}

//编译为

.puma-icon {
  background-image: url('/images/puma.png');
  border: 2px solid black;
  cursor: default; }
.sea-slug-icon {
  background-image: url('/images/sea-slug.png');
  border: 2px solid blue;
  cursor: pointer; }
.egret-icon {
  background-image: url('/images/egret.png');
  border: 2px solid white;
  cursor: move; }
```

**配合map使用**

```scss
@each $header, $size in (h1: 2em, h2: 1.5em, h3: 1.2em) {
  #{$header} {
    font-size: $size;
  }
}

//编译为

h1 { font-size: 2em; }
h2 { font-size: 1.5em; }
h3 { font-size: 1.2em; }
```

**@while**

@while 指令重复输出格式直到表达式返回结果为 false。这样可以实现比 @for 更复杂的循环，只是很少会用到。

```scss
$i: 6;
@while $i > 0 {
  .item-#{$i} { width: 2em * $i; }
  $i: $i - 2;
}

//编译为
.item-6 { width: 12em; }
.item-4 { width: 8em; }
.item-2 { width: 4em; }
```

#### **@content**

向混合样式中导入内容。

```scss
@mixin apply-to-ie6-only {
  * html {
    @content;
  }
}
@include apply-to-ie6-only {
  #logo {
    background-image: url(/logo.gif);
  }
}

//编译为

* html #logo {
  background-image: url(/logo.gif);
}
```

#### @function

函数指令，Sass支持自定义函数，并能在任何属性值或者Sass script中使用。

```scss
$grid-width: 40px;
$gutter-width: 10px;

@function grid-width($n) {
  @return $n * $grid-width + ($n - 1) * $gutter-width;
}

#sidebar { width: grid-width(5); }

//编译为

#sidebar { width: 240px; }
```



