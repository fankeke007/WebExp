# 字符串的扩展

第1-10点，只需了解

[**1.字符的Unicode表示法**](http://es6.ruanyifeng.com/#docs/string#%E5%AD%97%E7%AC%A6%E7%9A%84-Unicode-%E8%A1%A8%E7%A4%BA%E6%B3%95)

es5 之前可以使用'\uxxxx'表示一个字符\(xxxx为**码点**\)，但有范围限制**‘\u0000’--'\uFFFF'**.超出范围的字符得用两个双字节表示才能真确解析。es6提供了一种方法只需将超出范围的码点用大括号括起来就可以正确解析，如es6中 **'\u{20BB7}'** \(汉字"𐮷" \),es5中得用 **'\uD842\uDFB7'** 表示。

```javascript
'\z'==='z'
'\172'==='z'
'\x7A'==='z'
'\u007A'==='z'
'\u{7A}'==='z'
```

2.codePointAt\(\)

3.String.fromCodePoint\(\)

4.字符串的遍历接口

5.at\(\)

6.normalize\(\)

7.includes\(\)/startWith\(\)/endWith\(\)

8.repeat\(\)

9.padStart\(\)/padEnd\(\)

10.matchAll\(\)

11.模板字符串

模板字符串（template string）是增强的字符串，用反引号（**\`**）标识。他可以当做**普通字符串**使用，也可以用来定**义多行字符串**，或者**在字符串模板中嵌入变量**。

```javascript
//普通字符串
`In JavaScript '\n' id a line-feed .`

//多行字符串，所有的缩进和空格都会保存在输出之中
`In es5 this is 
not legal`

//字符传中嵌入变量
let name = 'Bob',title = 'today';
`Hello ${name},how are you ${time}`  


```

**模板字符串中嵌入变量**，要将变量名写在**${ }**之中。在大括号内部可以放置任意 **js** 表达式。若大括号中（表达式所求的值）的值不为一个字符串，如为Object，则会调用对象的toString方法。

**嵌套的模板字符串**

```javascript
//嵌套的模板字符串
const tmpl = addrs =>`
    <table>
    ${addrs.map(addr => `
        <tr><td>${addr.first}</td></tr>
        <tr><td>${addr.last}</td></tr>
    `).join('')}
    </table>
`;

//使用
const data = [
    {first:'<Jane>',last:'Bond'},
    {first:'Lars',last:'<Croft>'}
];
console.log(tmpl(data));

/********** result ***********

    <table>
    
        <tr><td><Jane></td></tr>
        <tr><td>Bond</td></tr>
    
        <tr><td>Lars</td></tr>
        <tr><td><Croft></td></tr>
    
    </table>
********** result ***********/
```

**引用模板字符串本身**

```text
// 写法一
let str = 'return ' + '`Hello ${name}!`';
let func = new Function('name', str);
func('Jack') // "Hello Jack!"

// 写法二
let str = '(name) => `Hello ${name}!`';
let func = eval.call(null, str);
func('Jack') // "Hello Jack!"
```

**12.模板编译**

```javascript
//模板编译实例（便于理解模板原理）

//template
let template = `
<ul>
    <% for(let i=0;i<data.supplies.length;i++){ %>
    <li><%= data.supplies[i] %></li>
    <% } %>
</ul>
`;

//如何编译template
//思路1：利用正则转换为js表达式字符串
/****************************
echo('<ul>');
for(let i=0;i<data.supplies.length;i++){
    echo('<li>');
    echo(data.supplies[i]);
    echo('</li>');
};
echo('</ul>');
****************************/

function compile(template){
    const evalExpr = /<%=(.+?)%>/g;
    //const expr = /<%(\s\S+?)%>/g;//无法完成匹配
    const expr = /<%(\s+?.+?)%>/g;
    
    template = template
    .replace(evalExpr,'`); \n echo($1); \n echo(`')
    .replace(expr,'`); \n $1 \n echo(`');
    
    template = 'echo(`'+template+'`);';
    console.log(template);
    
    let script =
    `(function parse(data){
        let output = '';
        function echo(html){
            output += html;
        }
        ${template}
        return output;
    })`;
    return script;
}


let parse = eval(compile(template));div.innerHTML = parse({ supplies: [ "broom", "mop", "cleaner" ] });
```

{% hint style="danger" %}
注意：**template.replace\(expr,$1\);  与  template.replace\(expr,\`$1\`\);的区别**

第二个也可以写为**template.replace\(expr , '$1'\)，这是replace使用括号内容的标准形式**
{% endhint %}

**13.标签模板**

标签模板其实不是模板，本质是函数调用的一种特殊形式。“标签”指的就是函数，紧跟在其后的模板字符串就是他的参数。其一个重要应用：过滤HTML字符串，防止用户恶意输入。

```javascript
/***************************//先熟悉标签模板的参数规则alert`123`// 等同于alert(123)----------------------------let a = 5;let b = 10;tag`Hello ${ a + b } world ${ a * b }`;// 等同于tag(['Hello ', ' world ', ''], 15, 50);***************************/let message =  SaferHTML`<p>${sender} has sent you a message.</p>`;function SaferHTML(templateData) {  let s = templateData[0];  for (let i = 1; i < arguments.length; i++) {    let arg = String(arguments[i]);    // Escape special characters in the substitution.    s += arg.replace(/&/g, "&amp;")            .replace(/</g, "&lt;")            .replace(/>/g, "&gt;");    // Don't escape special characters in the template.    s += templateData[i];  }  return s;}
```

14.String.raw

功能类似于python中的字符串前缀 **r** 和 C\# 中的字符串前缀**@**，用来获取一个模板字符串的原始字面量。

```javascript
//两种用法，但一般只用第二种
String.raw(callSite,...substitutions);//一般不会用到这种形式
String.raw`templateString`;
//示例
String.raw `Hi\u000A!`;             // "Hi\\u000A!"
```

15.模板字符串的限制

在es6模板字符串中一般会将'\u...' 和 '\x...' 转换为Unicode和十六进制字符串，若不合法就会报错（如：\```\unicode）。es2018对这个限制做了放松，使得String.raw`\unicode`返回'\\unicode'而不是报错，此外对解析不了的返回undefined，也不报错。``



