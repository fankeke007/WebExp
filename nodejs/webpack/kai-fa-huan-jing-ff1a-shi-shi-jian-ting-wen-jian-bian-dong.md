webpack 提供了几种选项，可以帮助我们在代码发生变化后自动编译代码。

* webpack's Watch Mode
* webpack-dev-server
* webpack-dev-middleware

### webpack's Watch Mode（观察模式）

缺点：为了能够看到修改后效果需要手动刷新浏览器

```js
//方法一：命令行参数，在npm scripts中启动webpack时带上--watch 参数
//package.json
"scripts":{
    "watch":"webpack --watch"
}

//方法二：webpack.config.js 中配置 watch：true
module:{...},
watch:true,
plugins:[...]
```

### webpack-dev-server

[文档](https://www.webpackjs.com/configuration/dev-server/)

安装：npm install --save-dev webpack-dev-server

使用：

```js
/*webpack.config.js*/
//在配置项中添加
devServer:{
    contentBase:'./dist'
}
```

> 现在，服务器正在运行，你可能需要尝试[模块热替换\(Hot Module Replacement\)](https://www.webpackjs.com/guides/hot-module-replacement)！

### webpack-dev-middleware

webpack-dev-middleware 是一个**容器（wrapper）**，它可以把webpack处理后的文件传递给一个服务器（server）。webpack-dev-server 在内部使用了它，同时，它也可以单独作为一个包来使用，以便进行更多自定义设置来实现更多的需求。

一下是webpack-dev-middleware 配合 express 的示例：

```js
npm install -D express webpack-dev-middleware
```

```js
//webpack.congfig.js
//设置 output.publicPath
//publicPath 也会在服务器脚本中用到
output:{
    filename:'[name].bundle.js',
    path:path.resolve(__dirname,'dist'),
    publicPath:'/'
}
```

```js
//项目目录，新增服务器文件server.js
/*
|-webpack-demo
|--package.json
|--webpack.config.json
|--server.js
|--/dist
|--/src
    |-index.js
    |-print.js
|-node_modules
*/
```

```js
/*server.js*/
const express = require('express');
const webpack = require('webpack');
cosnt webpackDevMiddleware = require('webpack-dev-middleware');

const app = express();
const config = require('./webpack.config.js');
cosnt compiler = webpack('config');

app.use(webpackDevMiddleware(compiler,{
    publicPath:config.output.publicPath
}));

app.listen(3000,function(){
    console.log('Example app listening on port 3000!\n');
})
```

```js
/*package.json*/
"scripts":{
    "server":"node server.js"
}
```



