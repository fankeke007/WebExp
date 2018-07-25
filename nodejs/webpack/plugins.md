常用插件：

[html-webpack-plugin](#html-webpack-plugin)

## html-webpack-plugin

#### [文档](https://github.com/jantimon/html-webpack-plugin "html-webpack-plugin 文档")

html-webpack-plugin 会默认生成 index.html 文件，包含打包的js文件。其配置属性（参见文档）可以帮助我们定制所需页面。

#### 生成多个html，只需多次调用

```js
plugins:[
    new HtmlWebpackPlugin({
        title:'Home Page',
        chunks:['home'] //要包含的js
    }),
    new HtmlWebpackPlugin({
        title:'Contact Us',
        chunks:['contact']
    })
]
```

上面chunks的含义配合以下两张图来理解：

![](/assets/html-webpack-plugin-chunks.png)

![](/assets/html-webpack-plugin-config.png)

## clean-webpack-plugin

#### [文档](https://github.com/johnagan/clean-webpack-plugin)

#### 每次构建前清零\(/dist\) build folders

```js
plugins:[
    new CleanWebpackPlugin(
        ['dist'],        //构建前清空dist里所有文件
        {                //更精细化的控制清理特定文件
            root:'absolutePath/to/root',
            exclude:['shared.js','files_to_ignore'],
            verbose:true,
            dry:false
        }
    ),
]
```



