# HTML 简介

##### 什么是网页

1. 网站是一个网页的集合
2. 网页是网站中的一页 通常是HTML格式
3. 构成网站的基本元素

##### HTML

超文本标记语言 标签语言

##### 常用浏览器

Firefox（Gecko）、Edge、Chrome（blink）、Safari（Webkit）、IE（Trident）

##### 浏览器内核

渲染引擎

##### Web标准

结构HTML、表现CSS、行为JS



#### 文档声明标签

```html
<!DOCTYPE html>
```

##### 

# HTML标签

```html
<html>开始标签 </html>结束标签
双标签
单标签
```

包含 (父子关系)

```html
<head>
<title></title>
<head>
```

并列(兄弟)

```html
<head></head>
<body></body>
```

##### lang语言集

```html
<html lang=""> 
en 代表英文
zh-CN代表中文
```

##### 字符集

```html
<meta charset ="UTF-8">
```

##### 标题标签

```html
<h1>-<h6>
</h1>-</hh6>
<!--每个标签单独占一行-->
```

##### 段落标签

```html
<p> </p>
会根据浏览器大小自动换行
保有空隙
```

##### 换行标签

```html
<br />
单标签
```

##### 文本格式化标签

实现文字设置粗体、斜体、下划线等等

```html
加粗 <strong></strong>或者<b></b>
```

```html
倾斜 <em></em> <i></i>
```

```html
删除线 <del></del> <s></s>
```

```html
下划线 <ins></ins> <u></u>
```

##### div 和span标签(无语义)

```html
<div></div> 独占一行 一行只能放一个 大盒子
<span></span> 跨距 一行可以放多个 小盒子
```

##### 图像标签

```html
<img src=""/>
src 是必须属性
alt 在图片显示不出来时，用文字显示
title 鼠标放置于其上时 提示的文字
width 图像的宽度
height 图像的高度
border 边框
必须以空格隔开
键值对的形式
```

##### 目录文件夹

###### 根目录

##### 路径

- 相对路径 /
- 绝对路径 \

##### 超链接标签

anchor 意为锚

```html
<a ...></a>
href 必须属性 用于指定连接目标的url地址
target 用于指定链接页面的打开方式 _self当前窗口打开 _blank新窗口打开
```

- 外部链接 http

- 内部链接 html名字

- 空链接 用#代替

- 下载链接 地址链接的是文件名

- 网页元素链接  

- 锚点链接 

  ```html
  <a href="#名字"></a>
  <h3 id="名字"></h3>
  ```

##### 注释标签

```html
<!-- -->
```

快捷键

ctrl+/

##### 特殊字符

```html
&nbsp;一个算一个空格
&lt;小于号 &gt;大于号
```



##### 表格标签

显示、表示数据

```html
<table>
    <tr>
        <td>文字</td>
    </tr>
</table>
```

```html
<table></table>表示定义表格的标签
<tr></tr> 行
<td></td> 单元格
必须嵌套在table中
```

##### 表头单元格

```html
<th></th> 加粗居中
```

##### 表格属性

不常用 后面用CSS 必须嵌在table括号里

```html
align left、right、center 规定表格相对周围元素的对齐方式
border “1”、“” 规定表格单元是否拥有边框 
cellpadding  规定单元边沿与其内容之间的空白 默认1像素
cellspacing 规定单元格之间的空白 默认2像素
width 规定表格宽度
height 高度
```

##### 表格结构标签

```html
<thead></thead> 头部
<tbody></tbody> 放置数据本体
```

##### 合并单元格

跨行 rowspan=“个数”

跨列 colspan=“个数”

目标单元格

跨行 最上侧单元格为目标 写合并代码

跨列 最左侧单元格为目标

写在td中

##### 表格总结

```html
table表格标签 tr行标签 td单元格标签 th表格单元格 thead表格头部 tbody 表格主体表格属性
```

