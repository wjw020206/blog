# CSS 专题之BFC



## 前言

> 石匠敲击石头的第 8 次

在上一篇文章中，如何避免外边距重叠的部分有提到，给容器元素添加 `overflow: auto`（或者非 `visible` 的值），可以避免与内部子元素产生嵌套外边距重叠，出现这个效果的原因是因为 **BFC**。

BFC 也是前端面试中必备的知识点，所以就有了这篇文章来梳理一下，如果哪里写的有问题欢迎指出。



## BFC 是什么

BFC 的全称为**块格式化上下文（Block Formatting Context）**，是页面中一块独立的渲染区域，**内部的子元素不会影响外部的元素，外部的元素也同样无法影响内部的子元素**。



## 如何创建 BFC

有以下方法可以创建块级格式化上下文：

- 根元素 `<html>`
- **浮动元素（元素的 `float` 不是 `none`）**
- **绝对定位元素（元素的 `position` 为 `absolute` 或 `fixed`）**
- **行内块元素（元素的 `display` 为 `inline-block`）**
- **`overflow` 值不为 `visible` 的块级元素**
- **`display` 值为 `flow-root` 的元素**
- **弹性元素（`display` 值为 `flex` 或 `inline-flex` 元素的直接子元素）**
- **网格元素（`display` 值为 `grid` 或 `inline-grid` 元素的直接子元素）**
- 表格单元格（元素的 `display` 为 `table-cell`，HTML 表格单元格默认为该值）
- 表格标题（元素的 `display` 为 `table-caption`，HTML 表格标题默认为该值）

更多的可以参考 [MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_display/Block_formatting_context)，上述加粗的是比较常用的，推荐记忆。

