# async/await

**1.概述**

es2017 标准引入 async 函数，使得异步操作变得更加方便。async 实质上是 Generator 函数的语法糖（类似Class是语法糖一样）。

{% hint style="info" %}
**async 主要对 Generator 函数改进了如下四点：**

1. **内置执行器**：Generator 函数的执行必须靠执行器，所以才有co模块，而async 函数自带执行器。async 函数的执行与普通函数一模一样，只要一行。
2. **更好的语义**：async和await，比起星号和yield，语义更清楚了。**async**表示函数里有异步操作，**await**表示紧跟在后面的表达式需要等待结果。
3. **更广的适用性**：co木块约定，yield命令后只能是Thunk函数或Promise对象，而async函数的await后面，可以是Promise对象和原始类型的值（若为原始类型则等同于同步操作）。
4. **返回值是Promise**：async函数的返回值是Promise对象，这比Generator函数的返回值是Iterator对象方便多了，可以使用then方法指定下一步操作。

事实上：async 函数完全可以看作是多个异步操作，包装成的一个Promise对象，而 await 命令就是内部 then 命令的语法糖。
{% endhint %}

**2.基本用法**

async 函数返回一个Promise对象，可以使用then方法添加回调函数。当函数执行的时候，一旦遇到await 就会先返回，等到异步操作完成，在接着执行函数体内后面的语句。

```javascript
function timeout(ms){
	return new Promise((resolve)=>{
		setTimeout(resolve,ms);
	});
}
//async 函数返回值是Promise对象，可以作为await命令的参数
//所以上述也可以写成如下：
/****************
async funciton timeout(ms){
	await new Promise((resolve)=>{
		setTimeout(resolve,ms);
	});
}
****************/
async funtcion asyncPrint(value,ms){
	await timeout(ms);
	console.log(value);
}
asyncPrint('haha',1000)
```

async 函数的多种写法形式：

```javascript
//函数声明
async function foo{};
//函数表达式
const foo = async function(){};
//对象的方法
let obj = {async foo(){}};
obj.foo().then(...);
//Class 的方法名
class Storage{
    constructor(){
        this.cachePromise = caches.open('avastars');
    }
    async getAvatar(name){
        const cache = await this.cachePromise;
        return cache.match(`/avastars/$(name.jpg)`);
    }
}
const storage = new Storage();
storage.getAvatar('jake').then(...);
//箭头函数
const foo = async ()=>{};
```

3.语法

（1）**async** 函数内部的 **return**语句**返回的值**，会成为**then方法回调函数的参数**。

```javascript
async function f(){
    return 'hello world';
};
f().then(v=>console.log(v))
//"hello world"
```

（2）**async** 函数**内部抛出错误**，会导致**返回的Promise对象变为reject 状态**。抛出的错误对象会被**catch**方法回调函数接收到。

```javascript
async function f(){
    throw new Error('出错了');
}
f().then(
    v => console.log(v),
    e => console.log(e)
);
//Error:'出错了'
```

（3）async 函数返回的**Promise对象**，必须等到内部**所有 await 命令后面的Promise 对象执行完**，才会发生**状态改变**，除非遇到 **return 语句或者抛出错误**。

```javascript
async function getTitle(url){
    let response = await fetch(url);
    let html = await response.text();
    return html.match(/<title>([\s\S]+)</title>/i)[1];
}
getTitle('https://tc39.github.io/ecma262/').then(sonsole.log);

//函数getTitle内部有三个操作：抓取网页、取出文本、匹配页面标题
//只有这三个操作全部完成，才会执行then方法里面的console.log
```



