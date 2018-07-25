##### 参考文档：

[javascript模块化之CommonJS、AMD、CMD、UMD、ES6](/javascript模块化之CommonJS、AMD、CMD、UMD、ES6)

[CommonJS 规范](https://www.cnblogs.com/littlebirdlbw/p/5670633.html)\[1\]     [CommonJS规范](/CommonJS规范)\[2\]

1. ##### amd
2. ##### cmd
3. ##### umd
4. ##### commonjs
5. ##### es6

## CommonJS

**CommonJS** ，一个偏向于服务端的规范，NodeJS 采用此规范。其**一个模块就是一个脚本文件**，**require** 命令第一次加载该脚本时就会**执行整个脚本**，然后再内存中生成一个对象。

```js
//使用形式
//a.js

exports.log=function(a){
    console.log(a);
}


//b.js
var log = require('a');
log('a');
//'a'
```

CommonJS有如下几个特性：

* 一个文件就是一个模块，拥有单独的作用域
* 普通方式定义的变量、函数、对象等都属于模块内部
* 通过require来加载模块
* 通过exports 和 module.exports 来暴露模块中的内容，exports其指向module.exports，因而其只是一个简写。可给exports添加属性，但不能直接给exports赋值，因为这会切断exports和module.exports之间的联系
* 模块可以多次加载但是初次加载时会被缓存，因此后续加载时都是初次缓存的结果。若此期间对模块做过更改，其变更不会体现在后续的模块加载中

CommonJS 是同步加载模块的，这对于服务端来说不是一个问题，因为所有的模块都在本地硬盘。等待模块时间就是硬盘的读取时间，几乎可忽略不计。但是对于浏览器而言，他需要从服务器加载模块，一旦等待时间过长，浏览器将处于“假死”状态，会严重影响用户体验。所以在浏览器端不适合使用CommonJS规范，因而在浏览器端出了一个AMD规范。

## AMD

代表：[require.js](https://requirejs.org/)

AMD 规范采用异步方式加载模块，模块的加载不影响其后的语句的运行，是一种非堵塞式的，且允许指定回调函数。

ADM也采用require命令来加载模块，但是不同于CommonJS，它要求两个参数：

```js
//加载模块
//第一个参数是一个数组，里面是要加载的模块
//callback 是加载完后的调
require([module],callback);

//示例
require(['math'],function(math){
    math.add(2,3);
});
```

```js
//定义模块 语法
//id 模块名，可选
//dependency 依赖模块数组，可选
//function 必须
define(id?,[dependency]?,function)


//定义模块 示例
define(['package/lib'],function(lib){
    function foo(){
        lib.log('hello world');
    }
    return {
        foo:foo
    }

});

//兼容CommonJS 示例
define(function(require,exports,module){
    var someModule = reqire('someModule');
    var anotherModule = require('anotherModule');
    someModulel.doTheAwesome();
    anotherModule.doTheAwesome();
    exports.asplode = function(){
        someModule.doTheAwesome();
        anotherModule.doTheAwesome();
    }
})
```

AMD加载模块的方式是**前置依赖**的，即加载模块时先加载所有的模块依赖。这不同于CMD规范，它是就近依赖的，不管代码写到哪，需要哪个模块了直接引入就行。

## CMD

代表：[sea.js](https://www.zhangxinxu.com/sp/seajs/)

```js
//CMD 定义模块
define(function(require,exports,module){
    var a = require('./a');
    a.doSomething();
    var b = require('./b');
});

//等价的AMD写法  （从此可以看出二者的不同）
define(['a','b'],function(a,b){
    a.doSomething();
    b.doSomething();
});
```

从CMD和AMD可以看出，两者其实可以归为一大类，以区别与CommonJS。

## UMD

UMD 不是一种规范，只是统一CommonJS、AMD 的一种形式。

```js
(function(roor,factory){
        if(typeof define === 'function' && define.amd){
            //AMD
            define(['jquery','underscore'],factory);
        }else if(typeof exports === 'object'){
            //node,CommonJS
            module.exports = factory(require('jquery'),require('underscore'));
        }else{
            //window
            root.returnExports = factory(root.jquery,root._); 
        }
    }(this,function($,_){

        function a(){};
        function b(){};
        function c(){};

        return {
            b:b,
            c:c
        };
}))
```

## ES6 module

es6 模块的设计思想是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS 和AMD模块都只能在运行时确定这些东西，这样导致没法做静态优化。因而webpack4 推荐 es6 module 加载模块，这样才可以利用静态优化做tree shaking ， 去除不必要代码，减少代码体积。

```js
//CommonJS VS es6 module

//CommonJS:会先完全加载fs生成一个对象,然后从生成对象上找出这3个方法
let {stat,exists,readFile} = require('fs');

//es6 module
import {stat,exists,readFile} from 'fs';
```

> es6 模块不是对象，而是通过export 命令指定输出的代码，在通过import命令输入。上面es6 module 的实质是只从fs模块加载3个方法，其他的方法不加载。



