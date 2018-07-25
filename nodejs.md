# npm

**升级npm**

```
npm install npm -g
```

有时执行上述命令不能彻底解决升级问题，此时可参考：[升级npm](https://app.yinxiang.com/shard/s25/nl/5490567/ce08f460-6627-4f38-9867-653da99e20a9)

**不同模式的包安装**

```
// 全局安装
npm install packageName -g

// 本地安装(不要-g参数)：会安装到本地node_modules中，但是不会更新package.json
npm install packageNme

// 本地安装，并跟新package.json：对于运行时需要的包
npm install packageName --save

//开发环境依赖安装：开发是需要，运行时不需要
npm install packageName --save-dev
```



