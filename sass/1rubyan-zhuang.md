Sass 依赖 ruby 编译，首先安装ruby。

### **安装ruby**

下载：[RubyInstaller for Windows](https://rubyinstaller.org/downloads/)

傻瓜式安装后，新添加的环境变量没生效：重启电脑后生效。（有无不重启的方式？）

### **安装sass和compas**

```
gem install sass
gem install compass
```

### 编译sass

#### 命令行编译

```
//单文件编译
sass input.scss output.css

//单文件监听与编译
sass --watch input.scss:output.css

//多个文件编译监听整个目录
sass --watch app/sass:public/stylesheets
```

#### 命令行编译配置选项

常用的两个配置选项为：

1. --style：sass 内置四中编译格式，**nested、expanded、compact、compressed**
2. --sourcemap：开启sourcemap调试

```
//编译格式（紧凑）
sass --watch input.scss:output.css --style compact

//编译格式+添加调试map
sass --watch input.scss:output.css --style expanded --sourcemap

//开启debug信息
sass --watch input.scss:output.css --debug-info
```

#### **四种内置编译格式**

nested：编译之后通过缩进显示类似原文件的nested样式

expanded：常见的css文件样式，每个属性单独一行

compact：每个选择器控制的样式一行显示

compressed：紧凑型，整个文案一行

软件编译方式：[koala](https://www.sass.hk/skill/koala-app.html)

