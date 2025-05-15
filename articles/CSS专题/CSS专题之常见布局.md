# CSS专题之常见布局



## 前言

> 石匠敲击石头的第 13 次

作为一名前端开发，在日常开发中，写页面是必不可少的工作，但有时候发现很多的页面结构都是类似的，所以打算写一篇文章来梳理一下日常开发中常见的布局，如果哪里写的有问题欢迎指出。



## 单列布局

单列布局日常开发中常见的有以下两种：

![image-20250515073441444](images/image-20250515073441444.png)

- **一栏布局：** `header`、`content`、`footer` 区域单列等宽，都居中显示
- **一栏布局（通栏）：** `header`、`footer` 区域与视口宽度等宽，仅中间 `content` 区域固定宽度，并居中显示

下面我们来分别看看两种单列布局的实现方式。



### 一栏布局

这个布局结构比较简单，`header`、`content`、`footer` 都居中显示。

**使用场景：** 如博客文章详情页等。

```html
<div class="container">
  <div class="header">header</div>
  <div class="content">content</div>
  <div class="footer">footer</div>
</div>
```

```css
.container {
  max-width: 1000px;
  margin: 0 auto;
}
/* ...其它样式 */
```

这里使用了 `max-width: 1000px;` 为三个区域的父级容器设置最大宽度，以此来确保三个区域等宽。

**⚠️ 注意：** 这里也可以使用 `width: 1000px;`，效果是差不多的，唯一的区别就是当屏幕小于 `1000px` 的时候表现不一样（`width: 1000px;` 会出现横向滚动条，`max-width: 1000px` 则不会，宽度会收缩）。



### 一栏布局（通栏）

`header`、`footer` 区域宽度设置为 `100%`，也可以不设置宽度，因为这两个区域都是块级元素，默认在·会占满整个视口宽度。不过 `header`、`footer` 区域中的内容区域的宽度要和 `content` 区域的宽度保持一致。

**使用场景：** 如企业官网等。

```html
<div class="header">
  <div class="header-content">header</div>
</div>
<div class="content">content</div>
<div class="footer">
	<div class="footer-content">footer</div>
</div>
```

```css
.header,
.footer {
  width: 100%;
}

.header-content,
.footer-content {
  max-width: 1000px;
  margin: 0 auto;
}

.content {
  margin: 0 auto;
  max-width: 1000px;
}

/* ...其它样式 */
```



## 两列布局

两列布局也是日常开发中常见的布局，通常由**一个固定宽度的侧边栏（`sidebar`）** 和 **一个自适应宽度的主内容（`main`）**区域组成。

**使用场景：** 如后台管理页面、文档导航页面、博客主页等。

![image-20250515075046855](images/image-20250515075046855.png)

### Float 实现

在过去，没有 Flex 和 Grid 的时候，通常使用 Float 实现两列布局。

```html
<div class="container">
  <div class="sidebar">sidebar</div>
  <div class="main">main</div>
</div>
```

```css
.container {
  overflow: hidden; /* 清除浮动，防止高度坍塌 */
  zoom: 1; /* 兼容 IE6/IE7，用来触发 hasLayout, 确保元素正确渲染和包含其内部浮动元素 */
}

.sidebar {
  float: left;
  width: 240px;
  margin-right: 20px;
}

.main {
  overflow: hidden; /* 触发 BFC，使其不会与 sidebar 重叠 */
  height: 100%;
  zoom: 1; /* 兼容 IE6/IE7，用来触发 hasLayout, 确保元素正确渲染和包含其内部浮动元素 */
}

/* ...其它样式 */
```

**⚠️ 注意：** 

- 该代码兼容 IE6 及以上的浏览器版本，对于维护老项目仍存在价值，**对于新项目更加建议优先使用 Flex 或 Grid 来实现两列布局**

- 如果 `sidebar` 区域要放右边，**需要注意渲染顺序，先写侧边栏，后写主内容**

  ```html
  <div class="container">
    <!-- 依旧保证先写侧边栏 -->
    <div class="sidebar">sidebar</div>
    <div class="main">main</div>
  </div>
  ```

  ```css
  .container {
    overflow: hidden;
    zoom: 1;
  }
  
  .sidebar {
    float: right; /* 调整浮动方向 */
    width: 240px;
    margin-left: 20px; /* 调整外边距方向 */
  }
  
  .main {
    overflow: hidden;
    height: 100%;
    zoom: 1;
  }
  
  /* ...其它样式 */
  ```




### Flex 实现

```css
/* html 部分同上 */
.container {
  display: flex;
}

.sidebar {
  width: 240px;
  margin-right: 20px;
}

.main {
  flex: 1;
}

/* ...其它样式 */
```



### Grid 实现

Grid 实现方式相比 Flex 方式代码更加简洁。

```css
/* html 部分同上 */
.container {
  display: grid;
  grid-template-columns: 240px 1fr;
  gap: 20px;
}

/* ...其它样式 */
```



## 三列布局

三列布局通常是由**一个自适应宽度的主内容（`main`）**夹在**左右两个固定宽度的 `left`、`right` 区域**的中间组成。

**使用场景：** 如门户首页、资讯平台、后台系统页面等。

![image-20250515084917371](images/image-20250515084917371.png)



### Float 实现

Float 实现三列布局通常有两种方式，最经典的就是 “圣杯布局” 和 “双飞翼布局”，我们先来看看 “圣杯布局”。



**圣杯布局**

圣杯（Holy Grail）布局最早出自于国外的 Matthew Levine 前辈在 2006 年写的一篇文章 《[In Search of the Holy Grail](https://alistapart.com/article/holygrail/)》中。

在常规情况下，我们都是按从上到下，从左到右的顺序写页面。

```html
<div class="container">
  <div class="left">left</div>
  <div class="main">main</div>
  <div class="right">right</div>
</div>
```

这样布局的效果是没有什么问题，但如果我们希望 `main` 区域的内容优先加载出来，就需要进行布局优化。

**浏览器的渲染引擎在构建和渲染渲染树是异步的（谁先构建好谁先显示）**，所以我们只需要将 `main` 区域放到提前的位置就可以优先渲染。

```html
<div class="container">
  <div class="main">main</div>
  <div class="left">left</div>
  <div class="right">right</div>
</div>
```

所以国外的前辈就提出了 “圣杯” 布局，目的是通过 CSS 的方式配合上面的 DOM 结构，优化 DOM 渲染。
