[npm文档](https://www.npmjs.com.cn/)

[npm VS yarn](http://web.jobbole.com/88459/)

# npm

#### 升级npm

```
npm install npm -g
```

windows 上若升级后还是正常使用新版本npm,则进一步进行如下操作：

```
复制C:\Users\{你的Windows用户名}\AppData\Roaming\npm\node_modules\npm下的文件到
你的 NodeJS安装目录下的 \node_modules\npm 中，覆盖掉原有的全部文件
```

#### 几种模式的包安装

```
//全局安装
// install 简写 i
npm install packageName -g

//本地安装，不跟新package.json
npm install packageName

//本地安装，跟新package.json：使用npm install 是会自动安装此包
//--save 简写 -S
npm install packageName --save

//本地安装到开发依赖
//--save-dev 简写 -D 
npm install packageName --save-dev
```

#### 查看已安装包信息

```
//查看全局安装包信息
npm list -g

//查看某个模块的版本号
npm list vue
```

#### 升级已安装的包

```
npm update packageName
```

#### package.json

[属性详解](https://www.cnblogs.com/tzyy/p/5193811.html)

#### **npm scripts**

npm 默认提供了一些钩子，当使用这些钩子命令时，可以省略run，如：npm start。若不属于钩子内的命令，则需使用run，如：npm run bundle。script 内可以直接使用模块名作为命令（而不用引模块路径），这是npm公共约定的内部实现。

