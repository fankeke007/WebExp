## 详情参考webpack官网 [webpack.config.js](https://www.webpackjs.com/configuration/ "webpack配置文档详情") 说明即可。

弄清楚五个重要的概念：

### 1.entry （入口）

指定使用哪个模块来作为构建其内部依赖图的开始。进入入口起点后webpack会找出有哪些库和模块时入口起点（直接或间接）依赖的。

默认值：'./src'

### 2.output （出口）

指定在哪里输出打包后的文件，以及如何命名这些文件。

默认值：'./dist'

### 3.loader （加载器）

loader 让 webpack 能够处理那些非 JavaScript 文件（**webpack 自生只能理解JavaScript**）。loader 可以将所有类型的文件转换为 webpack 能够处理的有效模块，然后利用 webpack 的打包能力进行处理。

**注意**：在 webpack 配置中定义 loader 时，要定义在 **module.rules** 中，而不是rules。

### 4.plugins （插件）

loader 被用于转换某些类型的模块，而插件则可以用于执行范围更广的任务。插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量。插件接口功能及其强大，可以用来处理各种任务。

想要使用一个插件，需要先 **require\(\) **它，然后把它添加到** plugins **数组中。多数插件可以通过** option （选型）**自定义。可以在一个配置文件中因为不同的目的而多次使用同一个插件。这时需要通过使用 new 操作符来创建它。

### 5.mode （模式）

通过不同的 mode 参数，可以启用相应模式下的 webpack 内置优化。

mode的三个参数类型：'development'、'production'、'none'



