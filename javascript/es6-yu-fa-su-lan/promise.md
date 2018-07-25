# Promise

1.概述

Promise 是异步编程的一种解决方案，比传统的解决方案--回调函数和事件--更合理与强大。

所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise是一个对象，从它可以获取异步操作的消息。Promise 提供统一的API，各种异步操作都可以用同样的方法进行处理。

{% hint style="info" %}
**Promise 对象的两个特点**

1. 对象的状态不受外界影响。Promise对象代表一个异步操作，有三种状态：**pending（进行中）**、**fulfilled（已成功）**、**rejected（以失败）**。只有异步操作的结果可以决定当前是哪种状态，任何其他操作都无法改变这个状态。
2. **一旦状态改变，就不会再变，任何时候都可以得到这个结果**。Promise对象的状态的改变只有两种情况：从pending变为fulfilled和从pending变为rejected。只要这两种情况发生，状态就凝固了，不会再改变了，会一直保持这个结果，这时就称为resolved（已定型）。**如果改变已经发生了，你再对Promise对象添加回调函数，也会立即得到这个结果**。**这与事件（event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的**。

Promise提供了统一的接口，是的控制异步操作流程更容易。Promise可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。

**Promise的几个缺点：**

1. 无法取消Promise，一旦新建它就会立即执行，无法中途取消
2. 不过不设置回调，Promise内部抛出错误，不会反应到外部
3. 当处于pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）

 如果某些事件不断地反复发生，一般来说，使用 [Stream](https://nodejs.org/api/stream.html) 模式是比部署`Promise`更好的选择。
{% endhint %}

```javascript
//Promise建立后会立即执行，其then方法指定
//的回调得当前脚本所有同步任务执行完后才会执行
let promise = new Promise(function(resolve,reject){
    console.log('Promise');
    resolve();//立即变更状态
});
promise.then(function(){
    console.log('resolved.');  //同步脚本执行完后最后输出
});
console.log('Hi!');
//Promise
//Hi!
//resolved
```

```javascript
//异步加载图片
function loadImageAsync(url){
    return new Promise(function(resolve,reject){
        const image = new Image();
        image.onload = function(){
            resolve(image);
        };
        image.onerror = function(){
            reject(new Error('Could not load image at '+url));
        };
        image.src=url;
    });
}
```

```javascript
//没调试通，稍后尝试
//Promise 实现 Ajax 的例子
const getJSON = function(url){
    const promise = new Promise(function(resolve,reject){
        const handler = function(){
            if(this.readyState !==4){
                return;
            }
            if(this.status === 200){
                resolve(this.response);
            }else{
                reject(new Error(this.statusText));
            }
        };
        const client = new XMLHttpRequest();
        client.open('GET',url);
        client.onreadystatechange = handler;
        client.responseType = 'json';
        client.setRequestHeader('Accept','application/json');
        client.send();
    });
    return promise;
};
getJSON('').then(function(){
    console.log('Contents: '+json);
},function(error){
    console.log('出错了',error);
});
```



