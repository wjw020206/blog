# HTML专题之DOCTYPE


## 前言

>  石匠敲击石头的第 1 次

有一道经典的前端面试题：**DOCTYPE 是什么？**

这个问题在网上一搜有很多相关的文章，如果让我自己回答竟然让我脑子里一片空白，我的印象里加了 `<!DOCTYPE html>` 就表示这个网页的版本是 HTML5，但是这样的回答在面试时肯定是不行的，看了很多网上的文章，决定写一篇文章来梳理一下，第一次写文章，如果有哪里讲的不对或者不完整，欢迎大家指出错误。



## DOCTYPE是什么

DOCTYPE 翻译成中文的话表示 **“文档类型”**，在一个 HTML 网页结构中是除了注释外所需要的第一行代码，告诉浏览器用什么方式解析和渲染文档。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <!-- 主体内容 -->
</body>
</html>
```



## 为什么需要DOCTYPE

在 HTML 刚开始发展的时候，Web 标准没有达成一致，各个厂商的浏览器都按照自己的意愿创造浏览器特性，这就导致各个浏览器显示 HTML 存在差异，导致开发者开发的网页可能在别的浏览器上无法正常显示，于是 W3C 组织制定了一套 Web 标准，由于该标准会导致现有的不符合标准的网页无法正常显示，于是浏览器厂商们开始支持在浏览器中设置渲染模式，通过在 HTML 文档的顶部添加 DOCTYPE 声明，用来告诉浏览器使用哪种渲染模式。

不过一开始的 DOCTYPE 声明并非是现在这样的 `<!DOCTYPE html>` 声明，在 HTML5 版本之前的 HTML 是定义为基于 SGML 的语言，需要对 DTD 进行引用，才能告诉浏览器使用什么渲染模式，浏览器通常支持三种渲染模式：

- **标准模式（Standards mode）：** 根据 W3C 组织制定的 Web 标准来渲染页面
- **怪异模式（Quirks mode）：** 又称混杂模式，兼容模式，按浏览器厂商自己的方式来渲染页面，通常用于模拟老式浏览器来兼容老站点
- **准标准模式（Almost standards mode）：** 接近于标准模式，但却具有少量怪异的特性



## 如何设置标准模式



### HTML4.01

在 HTML 4.01 中提供了三种 DOCTYPE 类型
- 严格型（Strict ）

  ```html
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
  ```

- 过渡型（Transitional ）

  ```html
  <!DOCTYPE HTML PUBLIC “-//W3C//DTD HTML 4.01 Transitional//EN” “http://www.w3.org/TR/html4/loose.dtd”>
  ```


- 框架型（Frameset ）

  ```html
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">	
  ```

这三种模式的区别如下：

| 模式       | 用途                                         | 特点                                                         | 支持的标签                                               |
| ---------- | -------------------------------------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| 严格模式   | 面向完全符合标准的页面                       | 不支持表现性或已废弃的 HTML 标签（如 `<font>`），鼓励使用 CSS 进行样式控制 | 仅支持结构性标签，不支持如 `<center>` 和 `<font>` 等标签 |
| 过渡模式   | 兼容旧版 HTML，适用于过渡阶段的开发 | 支持部分表现性标签（如 `<font>` 和 `<center>`)，可同时使用旧式和新式语法 | 支持严格模式的标签，也支持已废弃的表现性标签             |
| 框架集模式 | 专门用于多框架页面                           | 支持 `<frameset>`，用于定义页面的框架布局。不允许使用 `<body>` 标签 | 支持 `<frameset>` 和 `<frame>`，但不支持 `<body>`        |



### XHTML1.0

在 XHTML1.0 中也提供了三种 DOCTYPE 类型

- 严格型（Strict ）

  ```html
  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
  ```

- 过渡型（Transitional ）

  ```html
  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
  ```


- 框架型（Frameset ）

  ```html
  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
  ```

这三种模式的区别如下：

| 模式       | 用途                                         | 特点                                                         | 支持的标签                                               |
| ---------- | -------------------------------------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| 严格模式   | 面向完全符合标准的页面                       | 强调语义化和结构化，不支持表现性标签（如 `<font>` 和 `<center>`）， 必须遵循严格的 XML 规则 | 仅支持结构性标签，不支持如 `<center>` 和 `<font>` 等标签 |
| 过渡模式   | 兼容旧版 HTML 和 XHTML，适用于过渡阶段的开发 | 支持部分表现性标签（如 `<font>` 和 `<center>`)， 必须遵循 XML 语法规则（如标签必须闭合） | 支持严格模式的标签，也支持已废弃的表现性标签             |
| 框架集模式 | 专门用于多框架页面                           | 支持 `<frameset>`，用于定义页面的框架布局。不允许使用 `<body>` 标签 | 支持 `<frameset>` 和 `<frame>`，但不支持 `<body>`        |



### HTML5

HTML5 不再基于 SGML，因此不需要对 DTD 进行引用，使用最简单的声明方式

```html
<!DOCTYPE html>
```

**在日常开发中推荐使用这种声明方式**



## 如何设置怪异模式

1. 省略第一行的 `DOCTYPE` 声明

   ```html
   <!-- No DOCTYPE -->
   <html>
   <head>
       <title>怪异模式示例</title>
   </head>
   <body>
       <p>这是怪异模式下的页面。</p>
   </body>
   </html>
   ```

2. 使用了非标准的 HTML 4.01 声明，例如此处省略了 `URL` 部分

   ```html
   <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
   ```

**以上两种方式实测都可以设置怪异模式，但是不推荐**



## 如何判断网页用的是什么模式

可以打开浏览器的控制台，在控制台中执行以下代码

```js
alert(document.compatMode);
```

- 出现 BackCompat 表示怪异模式
- 出现 CSS1Compat 表示标准模式



## 怪异模式和标准模式的区别

| 特性           | 标准模式（Standards Mode）                               | 怪异模式（Quirks Mode）                                |
| -------------- | -------------------------------------------------------- | ------------------------------------------------------ |
| CSS盒模型      | 采用现代盒模型（`width` 和 `height` 不包括边框和内边距） | 采用旧版盒模型（`width` 和 `height` 包括边框和内边距） |
| 浏览器行为     | 严格遵循 HTML 和 CSS 标准，保持一致性                    | 为兼容旧网页，可能会采取不同的渲染方式，表现不稳定     |
| 网页渲染一致性 | 更加一致，不同浏览器间渲染结果接近                       | 渲染结果可能因浏览器而异，可能导致布局问题             |
| 兼容性         | 只支持现代网页标准，可能不支持老旧的特性                 | 兼容老旧网页，支持过时的 HTML 和 CSS 特性              |



## 总结

- `<!DOCTYPE html>` 是用于声明文档类型，告诉浏览器用标准模式渲染网页
- HTML5 因为不再基于 SGML，因此不需要对 DTD 进行引用，使用最简单的声明方式



## 参考文章

- [Don't forget to add a doctype - Quality Web Tips](https://www.w3.org/QA/Tips/Doctype)
- [HTML Standard](https://html.spec.whatwg.org/multipage/syntax.html#the-doctype)
- [文档类型声明 - MDN Web 文档术语表：Web 相关术语的定义 | MDN](https://developer.mozilla.org/zh-CN/docs/Glossary/Doctype)
- [怪异模式和标准模式 - HTML（超文本标记语言） | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Quirks_Mode_and_Standards_Mode)
- [HTML 中的 DOCTYPE 声明是什么？](https://www.freecodecamp.org/chinese/news/what-is-the-doctype-declaration-in-html)
- [浏览器与兼容性兼容性产生原因： 因为不同浏览器使用内核及所支持的HTML等网页语言标准不同；以及用户客户端的环境不同（如 - 掘金](https://juejin.cn/post/7031741176713576485)
- [html篇--这可能是目前较为全面的html面试知识点了吧也不知道有没有跟小编有同感的童鞋，随着技术的逐(ri)渐(yi - 掘金](https://juejin.cn/post/6844904180943945742)
- [DOCTYPE是什么，有何作用、 使用方式、渲染模式、严格模式和怪异模式的区别？DOCTYPE是HTML5的文档声明，通 - 掘金](https://juejin.cn/post/7323271640996691977)
