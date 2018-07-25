### file-loader

#### 安装

```
npm install -D file-loader
```

#### 使用

```js
/*webpack.config.js*/
module.exports = {
    module:{
        rules:[
            {
                test:/\.(png|jpg|gif)$/,
                use:[
                    {
                        loader:'file-loader',
                        options:{
                            name:"[path][name].[ext]",

                        }
                    }    
                ]
            }
        ]
    }

}
```

```js
/*index.js*/
/*
|-src
|--index.js
|--file.png
*/
import img form './file.png'
```

运行 webpack 打包后\(若不在options中配置name\)，会在output配置的目录\(假设为“path.resolve\(\_\_dirname,'dist'\)下生成\(文件名就是文件内容的 MD5 哈希值并保留所引用资源的原始扩展名\)文件。

#### options.name

```js
//不配置name的情况
/*
|-dist
|--0dcbbaa7013869e351f.png
*/

//配置options.name 为'[name].[ext]'的情况
//这中情况下会保留图片原名
/*
|-dist
|--file.png
*/


//配置options.name 为'[path][name].[ext]'
//这种情况下会保留文件目录
/*
|-dist
|--src
|---file.png
*/
```

#### options.outputPath

outputPath 所设置的路径时相对于output中设置的路径的。

假设name为上述带\[path\]的第三中情况

```js
//options.outputPath 设置为：'images'
/*
|-dist
|--images
|---src
|----file.png
*/

//options.outputPath 设置为：'../images'
//此时images和dist同级
/*
|-dist
|-images
|--src
|---file.png
*/
```

> 注意：设置name:'\[path\]\[name\].\[ext\]' 和 设置name:'\[name\].\[ext\]' + outputPath:'src'  是有区别的：
>
> 假设publicPath为‘/assets’，同一‘file.png’文件，最终前者url为"/assets/src/file.png"，后者为"/assets/file.png"
>
> 故要想生成"/assets/images/file.png"得使用name:'images/\[name\].\[ext\]'，
>
> 而不能使用后者将outputPath设置为"images"

#### options.publicPath

options.name 设置为\[name\].\[ext\]

??当设置了publicPath 时，所用用到图片的url将会用publicPath路径指代的url

```js
//设置options.publicPath 为 '/assets'
html中img的src='/assets/file.png'

//设置options.publicPath 为 'http://xxx.com'
html中img的src='http://xxx.com/file.png'
```

从上面示例代码可以看出，publicPath选项主要用来配置最终路径。对于配置最终绝对路径很有用。

