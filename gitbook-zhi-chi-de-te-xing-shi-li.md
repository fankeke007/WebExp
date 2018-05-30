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

![&#x56FE;&#x7247;&#x9ED8;&#x8BA4;&#x53EA;&#x80FD;&#x5C45;&#x4E2D;&#x663E;&#x793A;](.gitbook/assets/image%20%281%29.png)

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

媒体文件

{% embed data="{\"url\":\"https://codepen.io/sdras/pen/YZBGNp\",\"type\":\"rich\",\"title\":\"Vue-controlled Wall-E\",\"description\":\"I found this dribbble shot of Wall-E that I loved, and wanted to see if I could manipulate him with Vue bindings. https://dribbble.com/shots/2758895-Wa...\",\"icon\":{\"type\":\"icon\",\"url\":\"https://codepen.io/favicons/favicon-192x192.png\",\"width\":192,\"height\":192,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://s3-us-west-2.amazonaws.com/i.cdpn.io/28963.YZBGNp.small.14ebc7ae-6062-44a2-828e-ad7d5fa3242b.png\",\"width\":384,\"height\":225,\"aspectRatio\":0.5859375},\"embed\":{\"type\":\"app\",\"url\":\"https://codepen.io/sdras/embed/preview/YZBGNp?height=300&slug-hash=YZBGNp&default-tabs=html,result&host=https://codepen.io&embed-version=2\",\"html\":\"<iframe src=\\"https://codepen.io/sdras/embed/preview/YZBGNp?height=300&amp;slug-hash=YZBGNp&amp;default-tabs=html,result&amp;host=https://codepen.io&amp;embed-version=2\\" style=\\"border: 0; width: 100%; height: 300px;\\" allowfullscreen></iframe>\",\"height\":300,\"aspectRatio\":null}}" %}

video

{% embed data="{\"url\":\"http://124.232.155.153/vhot2.qqvideo.tc.qq.com/Am04\_XeEgI\_XEEHLeTuekn36OamvYFmed2N3utKCP0YM/c0662g7xb7u.p712.1.mp4?sdtfrom=v1104&guid=6446fce2ae6a38426b9b941546c56b45&vkey=D6B3BDAC52048C609FEB0FEB346CA5F2E55B5FDFC60CD82C41AC04A93541C266E58C9E512750B0446642883C7FC3D1CD375C3D89C49C0A3DB3BACF1C86CCE4D1F95B357719E38672C11838CB67ECC19294F7FDDE04D8ED2E6908E16CBC8BFADD3F51FB0CB14BF669848276DC0825083955AB726BA7B99C94&locid=99128cbd-a2d6-4c39-b4e6-d682514b37f6&size=17138961&ocid=439031212\",\"type\":\"video\",\"embed\":{\"type\":\"player\",\"url\":\"http://124.232.155.153/vhot2.qqvideo.tc.qq.com/Am04\_XeEgI\_XEEHLeTuekn36OamvYFmed2N3utKCP0YM/c0662g7xb7u.p712.1.mp4?sdtfrom=v1104&guid=6446fce2ae6a38426b9b941546c56b45&vkey=D6B3BDAC52048C609FEB0FEB346CA5F2E55B5FDFC60CD82C41AC04A93541C266E58C9E512750B0446642883C7FC3D1CD375C3D89C49C0A3DB3BACF1C86CCE4D1F95B357719E38672C11838CB67ECC19294F7FDDE04D8ED2E6908E16CBC8BFADD3F51FB0CB14BF669848276DC0825083955AB726BA7B99C94&locid=99128cbd-a2d6-4c39-b4e6-d682514b37f6&size=17138961&ocid=439031212\",\"html\":\"<div style=\\"left: 0; width: 100%; height: 0; position: relative; padding-bottom: 56.25%;\\"><video controls style=\\"top: 0; left: 0; width: 100%; height: 100%; position: absolute;\\">Your browser does not support HTML5 video.<source src=\\"http://124.232.155.153/vhot2.qqvideo.tc.qq.com/Am04\_XeEgI\_XEEHLeTuekn36OamvYFmed2N3utKCP0YM/c0662g7xb7u.p712.1.mp4?sdtfrom=v1104&amp;guid=6446fce2ae6a38426b9b941546c56b45&amp;vkey=D6B3BDAC52048C609FEB0FEB346CA5F2E55B5FDFC60CD82C41AC04A93541C266E58C9E512750B0446642883C7FC3D1CD375C3D89C49C0A3DB3BACF1C86CCE4D1F95B357719E38672C11838CB67ECC19294F7FDDE04D8ED2E6908E16CBC8BFADD3F51FB0CB14BF669848276DC0825083955AB726BA7B99C94&amp;locid=99128cbd-a2d6-4c39-b4e6-d682514b37f6&amp;size=17138961&amp;ocid=439031212\\" type=\\"video/mp4\\"></video></div>\",\"aspectRatio\":0}}" %}





github link

{% embed data="{\"url\":\"https://github.com/fankeke007/css\_secrets/blob/6759abd818981cbce7df8388da8467cbfc055eb0/background.css\",\"type\":\"link\",\"title\":\"fankeke007/css\_secrets\",\"description\":\"css\_secrets - example\",\"icon\":{\"type\":\"icon\",\"url\":\"https://github.com/fluidicon.png\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://avatars0.githubusercontent.com/u/12940581?s=400&v=4\",\"width\":400,\"height\":400,\"aspectRatio\":1}}" %}









