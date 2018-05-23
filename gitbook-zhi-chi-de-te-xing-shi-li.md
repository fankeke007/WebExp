---
description: gitBook 特性示例
---

# gitBook 支持的特性示例

排版相关

## 一级标题

### 二级标题

#### 三级标题  （最多只支持到三级标题）



**段落**：我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容我是段落内容

**无序列表**：

* 我是无序列表item1
* 我是无序列表item2
* 我是无序列表item3
  * 我是二级无序列表item1，我可以通过一级无序列表tab得到

有序列表：

1. 我是有序列表1
2. 我是有序列表2
3. 我可以通过1. 开头来得到

任务列表：

* [ ] 我是任务列表1
* [ ] 我是任务列表2

代码示例：

{% code-tabs %}
{% code-tabs-item title="example.js" %}
```javascript
var m1 = new Vue({
    el:'#m1',
    data:{
        a:'hello Vue',
        b:'good job'
    },
    method:{
        /* you can define some function here*/
    }
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

引用示例：

> ### 我是引用的内容哦；我是引用的内容哦
>
> 我是引用的内容哦

图片示例：图片默认只能居中显示，且只能是块状显示，不能行内显示（后续版本会改进行内显示）

![&#x56FE;&#x7247;&#x9ED8;&#x8BA4;&#x53EA;&#x80FD;&#x5C45;&#x4E2D;&#x663E;&#x793A;](.gitbook/assets/image.png)

表格示例：（remove 操作时要注意会删掉整个表格）

| 表格头 | 表格头 | 表格头 |
| --- | --- | --- | --- | --- |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

Hint 示例：（提示示例4种）

{% hint style="info" %}
建议
{% endhint %}

{% hint style="danger" %}
注意
{% endhint %}

{% hint style="warning" %}
warning
{% endhint %}

{% hint style="success" %}
推荐
{% endhint %}

页面链接示例：

{% page-ref page="gitbook-zhi-chi-de-te-xing-shi-li.md" %}



API 示例：

{% api-method method="get" host="" path="" %}
{% api-method-summary %}
获取宠物信息列表  
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-query-parameters %}

{% api-method-form-data-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=302 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=304 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

table切换示例：

{% tabs %}
{% tab title="First Tab" %}
first tab contents
{% endtab %}

{% tab title="Second Tab" %}
second tab conten
{% endtab %}
{% endtabs %}



