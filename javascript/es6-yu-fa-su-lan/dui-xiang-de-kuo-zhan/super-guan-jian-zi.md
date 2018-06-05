# super关键字

this关键字总是指向函数所在的当前对象，es6新增了另一个类似的关键字super，指向当前对象的原型对象。

```javascript
const proto = {
    foo:'hello'
};
```

