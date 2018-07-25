1.xampp

2.http-server \(node\)

3.express 自行搭建

## http-server

#### 安装、配置、使用

```
#创建并进入node-server路径，初始化
mkdir node-server
cd node-server
npm init -y

#创建服务文件夹
mkdir public
```

```
#安装 http-server 
npm i http-server -D
```

```
#npm scripts（package.json） 添加启动命令
"scripts":{
    "start":"http-server public"
}
```

```
#启动服务（node-server 路径下）
npm start
```

将会看到如下，至此服务器已经配置并启动了

![](/assets/node-server.png)

可选配置项：参见[官方文档](https://github.com/indexzero/http-server)

