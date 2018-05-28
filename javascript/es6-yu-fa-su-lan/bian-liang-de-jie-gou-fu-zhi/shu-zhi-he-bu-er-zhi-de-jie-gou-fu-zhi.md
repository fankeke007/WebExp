# 数值和布尔值的解构赋值

解构赋值是，若等号右边是数值和布尔值，则会先转为对象。

```javascript
let {toString:s}=123;
s===Number.prototype.toString; //true
```



