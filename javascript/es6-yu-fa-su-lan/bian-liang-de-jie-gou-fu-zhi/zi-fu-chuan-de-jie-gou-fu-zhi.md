# 字符串的解构赋值

字符串的解构赋值中，字符串被转换成一个类数组对象（类数组对象有一个length属性）。

```javascript
const [a,b,c,d,e]='hello';

let {length:s}='hello';
s;//5
```



