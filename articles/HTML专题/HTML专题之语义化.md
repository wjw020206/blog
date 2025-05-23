# HTML专题之语义化



## 前言

> 石匠敲击石头的第 3 次

有一道经典的前端面试题：如何理解 HTML 语义化？

如果让我自己回答，我会说语义化会让 HTML 代码更利于维护，并且有利于 SEO 的优化。但这样的回答显然不够完整，所以才有了这篇文章来好好记录一下 HTML 语义化，如果哪里写的有问题欢迎指出。



## HTML语义化是什么

HTML 中语义化简单来说就是使用 **“有意义的标签”** 来表示页面上不同的区域。

例如下图中就使用了语义化标签用来表示一个页面的各个区域。

![image-20250207085525440](images/image-20250207085525440.png)



## 为什么要使用HTML语义化

使用 HTML 语义化标签有以下三点好处：

1. **有利于构建清晰的结构，有利于团队的维护和开发。**
2. **有利于搜索引擎爬虫更好的理解页面，以此来提升网页的权重。**
3. **有利于不同设备的解析，如屏幕阅读器、盲人阅读器等设备更好的区分哪些部分是主要内容用于优先阅读。**



## 什么场景下适合使用HTML语义化

**不是所有场景都适合使用 HTML 语义化！，不是所有场景都适合使用 HTML 语义化！，不是所有场景都适合使用 HTML 语义化！**

使用 HTML 语义化标签，**“用对” 比 “不用” 好，“不用” 比 “用错” 好。** 错误的使用语义化标签只会给机器阅读造成混淆、增加嵌套，给 CSS 编写加重负担。

以下几个场景我个人认为就不适合使用 HTML 语义化标签：

- **需要兼容 IE 等上古浏览器：** 原因很简单，根本就不支持 HTML 语义化标签。
- **没有 SEO 需求的项目：** 用 HTML 语义化我认为最主要的目的是 SEO 优化，项目如果不会被搜索引擎检索到，压根就不需要 HTML 语义化。就像微信小程序的页面布局里大多只有 `<view>` 这一种标签，没有那么多语义化标签，因为小程序没有 SEO 的需求。
- **高度自定义组件库：** 使用通用的容器元素（如 `<div>` 和 `<span>`）来提供灵活性，而不是依赖语义化标签。
- **Vue 等单页面应用(SPA)项目：** 这类项目初始加载内容不完整，只有少量的骨架（如一个空的 `<div id="app"></div>`），所以搜索引擎读取不到语义化的标签。如要项目需要 SEO 优化，**推荐使用服务端渲染，如：Nuxt.js、Next.js 等**。
- **软件界面场景：** HTML 语义化的场景更适合 “富文本” 场景，这类场景通常是由文章、博客、新闻等强调内容的结构和语义的部分组成。“软件界面” 场景更多是由 按钮、表单、图表、输入框、状态切换、交互式组件等组成，界面更关注交互，没有明确的内容结构和语义，**这时推荐直接使用 `<div>` 或 `<span>` 标签。**



## HTML语义化使用中的障碍

在平常开发网页的时候我基本上也是使用 `<div>` 和 `<span>` 标签偏多，语义化标签的使用对我存在一定的**心智负担**。基本上想要用好语义化标签存在以下几个方面的障碍：

- **学习成本：** 需要花时间学习每个语义化标签的语义以及使用场景。
- **选择适当标签的困难：** 在一些复杂的布局中选择一个合适的语义化标签不太直观，选择上会犹豫不决，影响开发效率。
- **兼容性和浏览器支持：** 这个问题在现代浏览器上不算什么大的问题，但是在国内还是有部分公司要求兼容 IE 等古老浏览器(不支持语义化标签)。
- **团队维护上的差异：** 每个人对语义化标签的理解和使用方式可能不同，导致部分代码风格不一致，增加了维护的复杂性。

解决方案：

- **实践和经验：** 说白了就是多用、多练和总结经验。
- **合理的折衷：** 不适合的场景下可以适当的使用 `<div>` 和 `<span>` 标签。
- **文档和团队规范：** 制定团队编码规范，确保团队成员对语义化标签有一致的理解。



## 常用的语义化标签

### `<header>`

`<header>` 标签既可以表示整个网页的头部，也可以表示一篇文章或者一个区块的头部。

- 表示整个网页的头部(页眉)。

  ```html
  <header>
    <h1>网页标题</h1>
    <nav>
      <ul>
        <li><a href="#">首页</a></li>
        <li><a href="#">关于</a></li>
        <li><a href="#">更多</a></li>
      </ul>
    </nav>
  </header>
  ```

  通常包含**网页 Logo、网页标题、导航链接**等信息。

- 表示文章的头部。

  ```html
  <article>
    <header>
      <h2>文章标题</h2>
      <p>CodePencil，发表于2025年2月12日</p>
    </header>
    <p>文章内容...</p>
  </article>
  ```

  通常包含**文章标题、作者、发布时间**等信息。

**⚠️ 注意：**

- 由于很多区块都可以有头部，所以一个页面可能包含多个 `<header>` 标签。
- 一个具体的场景中只能包含一个 `<header>` 标签，例如整个页面只能有一个页眉，一个文章只能有一个头部区域。
- `<header>` 标签中不能再包含另一个 `<header>` 或 `<footer>` 标签。



### `<footer>`

`<footer>` 标签既可以表示整个网页的尾部，也可以表示一篇文章、一个章节或者一个区块的尾部。

- 表示整个网页的尾部(页尾)。

  ```html
  <footer>
    <p>&copy; 2025 我的公司 | 版权所有</p>
    <ul>
      <li><a href="#privacy">隐私政策</a></li>
      <li><a href="#terms">服务条款</a></li>
      <li><a href="#contact">联系我们</a></li>
    </ul>
  </footer>
  ```

  通常包含**版权信息、联系信息、相关链接**等信息。

- 表示文章的尾部。

  ```html
  <article>
    <header>
      <h2>文章标题</h2>
    </header>
    <p>文章内容...</p>
    <footer>
      <p>作者：CodePencil | 日期：2025-02-12</p>
      <p>阅读更多文章：<a href="#">下一篇</a></p>
    </footer>
  </article>
  ```

  通常包含**文章的作者、日期和链接到下一篇文章的链接**等信息。

**⚠️ 注意：**

- 由于很多区块都可以有尾部，所以一个页面可能包含多个 `<footer>` 标签。
- 一个具体的场景中只能包含一个 `<footer>` 标签，例如整个页面只能有一个页尾，一个文章只能有一个尾部区域。
- `<footer>` 标签中不能再包含另一个 `<header>` 或 `<footer>` 标签。



### `<main>`

`<main>` 标签表示页面的主体内容，**一个页面只能有一个 `<main>` 标签**。

```html
<body>
  <header>页眉</header>
  <main>
    <article>文章</article>
  </main>
  <aside>侧边栏</aside>
  <footer>页尾</footer>
</body>
```

通常包含页面的核心内容，比如**文章、博客内容、商品列表、用户资料**等信息。

比如导航栏、页脚、广告、侧边栏、搜索栏等，通常不应该放在 `<main>` 中，因为它们不属于页面的核心内容。

**⚠️ 注意：** `<main>` 标签不能放置在 `<header>`、`<footer>`、`<article>`、`<aside>`、`<nav>` 等标签中。



### `<article>`

`<article>` 标签表示一段完整的内容，可以有自己的标题（`<h1>` 到 `<h6>`）。

```html
<article>
  <h2>文章标题</h2>
  <p>文章内容</p>
</article>
```

通常用于表示博客文章、新闻条目、产品描述等独立的内容单元，一个网页可以包含一个或多个 `<article>` 标签。



### `<aside>`

`<aside>` 标签用来表示与网页或者文章主要内容相关但不属于主要内容的部分。

- 在网页级别中的 `<aside>` 可以用来放置侧边栏，**具体位置不一定要在页面的侧边，可以出现在页面的任意位置**。

  ```html
  <body>
    <main>主体内容</main>
    <aside>侧边栏</aside>
  </body>
  ```

  通常用于表示**侧边栏、推荐文章、广告、相关链接**等信息。

- 在文章级别中 `<aside>` 可以用来放置文章的**补充信息、评论或注释**等信息。

  ```html
  <p>第一段</p>
  <aside>
    <p>本段是文章的重点</p>
  </aside>
  ```



### `<section>`

`<section>` 标签表示一个含有主题的独立部分，通常用于表示页面的不同章节。

```html
<article>
  <header>
    <h1>学习 HTML 和 CSS</h1>
    <p>作者：CodePencil | 日期：2025-02-12</p>
  </header>

  <section>
    <h2>HTML 基础</h2>
    <p>HTML 是网页的结构语言...</p>
  </section>

  <section>
    <h2>CSS 基础</h2>
    <p>CSS 是网页的样式语言...</p>
  </section>

  <footer>
    <p>文章结尾信息...</p>
  </footer>
</article>
```

**⚠️ 注意：** 

- `<section>` 标签总是多个一起使用，一个页面不能只有一个 `<section>` 标签。
- `<section>` 标签应该包含 `<h1>` ~ `<h6>` 标签。
- 多个 `<section>` 可以放在同一个 `<article>` 标签中，一个 `<section>` 也可以包含多个 `<article>`，如何使用取决于在页面中具体的含义。



### `<nav>`

`<nav>` 标签用于放置页面或文章的导航信息。

```html
<nav>
  <ul>
    <li><a href="#">商品 A</a></li>
    <li><a href="#">商品 B</a></li>
    <li><a href="#">商品 C</a></li>
  </ul>
</nav>
```

**⚠️ 注意：** 

- `<nav>` 标签通常放置在 `<header>` 里面，不适合放入 `<footer>` 标签中。
- `<nav>` 标签中通常是列表，也可以放置其它标签。
- 一个页面可以有多个 `<nav>` 标签，例如一个页面既有站点导航也有文章导航。



### `<h1>` ~ `<h6>`

该标签用来表示文章的标题，按照标题的等级，一共分成六级。

- `<h1>`：一级标题
- `<h2>`：二级标题
- `<h3>`：三级标题
- `<h4>`：四级标题
- `<h5>`：五级标题
- `<h6>`：六级标题

其中 `<h1>` 标签是最高级别的标题，`<h6>` 是最低级别的标题，下一级标题都是上一级标题的子标题。

```html
<body>
  <h1>基础</h1>
    <h2>概述</h2>
    <h2>基本概念</h2>
      <h3>网页</h3>
      <h3>链接</h3>
    <h2>主要用法</h2>
</body>
```

**⚠️ 注意：** 

- 标题不应该越级，比如 `h1` 标签之后直接写 `h3` 标签。
- 最好只使用一个 `<h1>` 来表示特定区域的主标题。



### `<hgroup>`

`<hgroup>` 标签通常用于标题(`<h1> ~ <h6>`)元素与一个或多个 `<p>` 标签组合在一起，表示标题和与标题相关联的内容。

```html
<hgroup>
  <h1>HTML：现行标准</h1>
  <p>更新于 2022 年 7 月 12 日</p>
</hgroup>
```

![image-20250212132636223](images/image-20250212132636223.png)

### `<address>`

`<address>` 标签用于表示联系信息的元素

```html
<address>
  联系人: 张三<br>
  地址: 北京市朝阳区 XXX 路<br>
  电话: 123-456-7890<br>
  <a href="mailto:example@example.com">example@example.com</a>
</address>
```

通常用于描述与某个网站、公司、作者或页面相关的联系信息，比如地址、电话号码、电子邮件等。

**⚠️ 注意：** 

- `<address>` 标签通常放在 `<footer>` 标签中。
- `<address>` 标签应该只包含联系信息，不要滥用。



### `<strong>`

`<strong>` 标签用于表示这部分文本具有更高的重要性， 默认情况下会使文本加粗。

```html
<p><strong>请注意：</strong>这是一条非常重要的消息。</p>
```

通常用于强调某些非常重要的内容，或者特别关键的文本。

**⚠️ 注意：** `<b>` 标签与 `<strong>` 标签很相似，但是 `<b>` 标签由于历史原因没有语义，**优先使用 `<strong>` 标签**。



### `<em>`

`<em>` 标签**用于避免歧义**，标识句子中的重点或者这句话的重音，不一定标识出来的东西很重要，默认情况下会使文本倾斜。

拿 winter 老师在[《重学前端》]([HTML语义：div和span不是够用了吗？-重学前端-极客时间](https://time.geekbang.org/column/article/78158)) 文章中举得例子来说，下面同样的这句话在不同的上下文中意思是不同的。

```html
今天我吃了一个苹果。
```

例如：

```htm
昨天我吃了一个香蕉。
今天我吃了一个苹果。
```

```html
昨天我吃了两个苹果。
今天我吃了一个苹果。
```

上面分别展示了两种不同的上下文情况，前者强调的是东西，后者强调的是数量，对于我们人来说容易理解，但是对于机器来说可能就不明白这个两个不同上下文中 `今天我吃了一个苹果。` 的意思有什么区别，这时就可以使用 `em` 标签来避免歧义。

```html
昨天我吃了一个香蕉。
今天我吃了一个<em>苹果</em>。
```

```html
昨天我吃了两个苹果。
今天我吃了<em>一个</em>苹果。
```

**⚠️ 注意：** `<i>` 标签与 `<em>` 标签很相似，但是 `<i>` 标签由于历史原因没有语义，**优先使用 `<em>` 标签**。



## 总结

- HTML 中语义化简单来说就是使用 **“有意义的标签”** 来表示页面上不同的区域。

- 使用 HTML 语义化标签有以下三点好处：

  - **有利于构建清晰的结构，有利于团队的维护和开发。**
  - **有利于搜索引擎爬虫更好的理解页面，以此来提升网页的权重。**
  - **有利于不同设备的解析，如屏幕阅读器、盲人阅读器等设备更好的区分哪些部分是主要内容用于优先阅读。**

- 不是所有场景都适合使用语义化标签，需要根据具体场景来使用。

- HTML 语义化标签使用存在的障碍：

  - **学习成本**：需要花时间了解每个语义化标签的意义和使用场景。

  - **选择标签困难**：在复杂布局中，选择合适的语义化标签可能不直观，导致开发效率降低。

  - **兼容性问题**：虽然现代浏览器支持良好，但仍需考虑兼容 IE 等老旧浏览器。

  - **团队维护差异**：不同开发者对语义化标签的理解不一致，可能导致代码风格不统一，增加维护成本。

- 常用的语义化标签有：`<header>`、`<footer>`、`<main>`、`<article>` 等。



## 参考文章

- [大厂都在”偷偷“用语义化标签，你却还在div？HTML语义化标签，就是那些带有特定含义的标签，它们告诉浏览器和搜索引擎， - 掘金](https://juejin.cn/post/7388056946121113637)
- [我的HTML会说话——从实用出发，谈谈HTML的语义化与同为人类的程序员沟通，帮助程序员快速掌握当前代码。这一点其实是可 - 掘金](https://juejin.cn/post/6844903569590583304)
- [对HTML语义化的一些理解和记录为什么要使用语义化标签？我用DIV+CSS也能做出来一样的效果，确实单纯看效果两者并没有 - 掘金](https://juejin.cn/post/6844903598401257480)
- [停止滥用div! HTML语义化介绍我们喜欢（使用）标签。它们已经存在了几十年，这几十年来，当需要将一些内容包 - 掘金](https://juejin.cn/post/6844903817968893960)
- [1 如何理解HTML语义化 | 前端进阶之旅](https://interview.poetries.top/docs/excellent-docs/1-HTML模块.html#_1-如何理解html语义化)
- [HTML5语义化标签的详细介绍 - 小蓝博客](https://www.8kiz.cn/archives/26261.html)
- [HTML语义：div和span不是够用了吗？-重学前端-极客时间](https://time.geekbang.org/column/article/78158)
- [网页的语义结构 - HTML 教程 - 网道](https://wangdoc.com/html/semantic)





