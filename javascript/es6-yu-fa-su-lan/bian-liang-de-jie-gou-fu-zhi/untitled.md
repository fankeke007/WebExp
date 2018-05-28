# 函数参数的解构赋值



```javascript
//eg1
function add([x,y]){
    return x + y;
}
add([1,3]);//4

//eg2
[[1,2],[3,4]].map(([a,b])=>a+b);//[3,7]

//eg3.函数参数解构默认值
//为参数指定默认值
var move=({x=0,y=0}={})=>[x,y];
move({x:3,y=8});//[3,8]
move();//[0,0]

//eg4.对比上一条，弄清两者区别
//为变量指定默认值
var move = ({x,y}={x:0,y:0})=>[x,y];

```

{% hint style="danger" %}
注意：为参数指定默认值和为变量指定默认值的区别（**eg3 VS eg4**）
{% endhint %}



