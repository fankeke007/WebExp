**下载**：[https://github.com/coreybutler/nvm-windows/releases](https://github.com/coreybutler/nvm-windows/releases)

**官网**：[nvm.sh](https://github.com/creationix/nvm/blob/master/README.md)

**使用**：

1. 将安装目录置于环境变量path下 ，以便全局获取nvm命令
2. 将安装目录下settings.txt内的node\_mirror和npm mirror设置成相应的淘宝镜像（详情见下）
3. 直接命令行 nvm 即可看到相应操作指南，按照执行就行。

settings.txt 配置文件如下：\(最后两个是需要自己配置的行，注意node路径后面的/，无此“/”时会无法安装\)

```txt
root: D:\nvm
arch: 64
proxy: none
originalpath: .
originalversion: 
node_mirror: https://npm.taobao.org/mirrors/node/
npm_mirror: https://npm.taobao.org/mirrors/npm/
```

![](/assets/nvm.png)

