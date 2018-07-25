剔除模块中无用（没使用）代码

使用tree shaking的三个条件：

1. 使用es6 模块语法 （提供静态优化前提）
2. package.json中添加 “sideEffect” 入口 （排除副作用文件，如css）
3. 引入能删除未引用代码（dead code）的压缩工具（如UglifyJSPlugin）



