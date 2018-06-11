# Class 基本语法

es5中生成实例对象的传统方法是通过构造函数：

```javascript
function Point(x,y){
    this.x = x;
    this.y = y;
};
Point.prototype.toString = function(){
    return '('+this.x+', '+this.y+')';
};
```

