---
title: "Html Element"
date: 2021-03-16T20:09:57+08:00
draft: false
---

## a 标签

当点击一个链接或按钮时，打开一个新的电子邮件发送信息而不是连接到一个资源或页面，这种情况是可能做到的。这样做是使用<a>元素和mailto：URL的方案。
其最基本和最常用的使用形式为一个mailto:link （链接），链接简单说明收件人的电子邮件地址。例如:

`<a href="mailto:nowhere@mozilla.org">向 nowhere 发邮件</a>`

真实案例：
每个字段的值必须是URL编码的。 也就是说，不能有非打印字符（不可见字符比如制表符、换行符、分页符）和空格 percent-escaped. 同时注意使用问号（?）来分隔主URL与参数值，以及使用&符来分隔mailto:中的各个参数。

```html
<a href="mailto:nowhere@mozilla.org?cc=name2@rapidtables.com&bcc=name3@rapidtables.com&subject=The%20subject%20of%20the%20email&body=The%20body%20of%20the%20email">
  Send mail with cc, bcc, subject and body
</a>
```

a标签的超链接还可以设置链接到QQ、迅雷、：

```
tencent://temp-chat?QQ=XXX?
thunder://...
```

href值还可以为空：当使用a标签来做按钮，不需要跳转时，href值即为空。

#### a标签的download属性 (HTML5)
此属性指示浏览器下载 URL 而不是导航到它，因此将提示用户将其保存为本地文件。如果属性有一个值（可以没有值），那么此值将在下载保存过程中作为预填充的文件名（如果用户需要，仍然可以更改文件名）。

如果同时有target="_blank"与download="result.jpg" 只会跳转到新的网页（只有target生效）

## img 标签

img的src为空：当前地址

img的属性`<usemap="#">`用来做选座页面

usemap 属性将图像定义为客户端图像映射(图像映射image-map指带有可点击区域的图像)。
usemap 属性与 `<map>` 元素的 name 或 id 属性相关联，以建立`<img>` 与`<map>` 之间的关系。那么指定的区域用map包裹的area标签来指定

## table 标签

### table属性

* border：线宽，指定宽度
* caption：标题
* thead：table head的行，里面的单元格可以变成 th
* tbody：表体，里面用
    * tr：table row
    * td：单元格 table data
* tfoot：表尾 ，定义了一组表格中各列的汇总行。里面用td（推荐）、th都行。

#### th、td的跨列、跨行：标签增加属性。
colspan=2，跨2列
rowspan=2 跨2行

可以给行名和列名字设定标签 `id=""`（不许有空格），对应的单元格可以使用headers=“标签一 标签二”。来标识单元格数据。

表格：跨行只能在旁边有行的情况才能跨（列也一样）。thead不能跨到tbody去，反过来也一样。也就是说，跨行不能跨tr的父元素。跨行后旁边的行会被挤的离开原来文字
