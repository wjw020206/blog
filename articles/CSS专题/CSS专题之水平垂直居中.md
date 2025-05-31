# CSS专题之水平垂直居中



## 前言

> 石匠敲击石头的第 16 次

在日常开发中，经常会遇到水平垂直居中的布局，虽然现在基本上都用 Flex 可以轻松实现，但是在某些无法使用 Flex 的情况下，又应该如何让元素水平垂直居中呢？这也是一道面试的必考题，所以打算写一篇文章来好好梳理一下，如果哪里写的有问题欢迎指出，不胜感激。



## 分类

实现元素水平垂直居中的方法有很多，大致可以分为以下两类：

- **固定宽高元素**适用的方法
- **不固定宽高元素**适用的方法

我们先实现基础的布局，然后再分别讲每一类具体的方案。
```css
.container {
  border: 1px solid red;
  width: 300px;
  height: 300px;
}

.box {
  background: blue;
  color: #fff;
}

.size {
  width: 100px;
  height: 100px;
}
```

```html
<div class="container">
  <div class="box size">你好，世界</div>
</div>
```

![image-20250531153034788](images/image-20250531153034788.png)



## 固定宽高元素



### absolute + 负 margin

```css
.container {
  /* 其它的基础样式... */
  position: relative;
}

.box {
  /* 其它的基础样式... */
  position: absolute;
  top: 50%;
  left: 50%;
  margin-left: -50px;
  margin-top: -50px;
}
```

该方案的原理非常简单，可以分为两步来看：

1. 先通过**绝对定位**的 `top: 50%` 和 `left: 50%` 使**元素的左上角**定位在 `.container` 容器元素的中心位置

   ![image-20250531154018846](images/image-20250531154018846.png)

2. 再通过 `margin-top` 和 `margin-left` 设置为**负值**，具体值为元素宽度和高度的一半，例如这里元素的宽高都是 `100px`，所以一半就是 `50px`

   ![image-20250531172045155](images/image-20250531172045155.png)

   最终的效果如下

   ![image-20250531172212544](images/image-20250531172212544.png)

[在线查看效果](https://codepen.io/wjw020206/pen/KwpVRYr)

**✅ 优点：** 兼容性好，适用于 IE 等老版本浏览器。

**⚠️ 缺点：** 

- 需要提前知道元素大小，并且需要手动计算元素大小的一半
- 每次修改元素大小都需要同步修改 `margin` 值



### absolute + margin: auto

```css
.container {
  /* 其它的基础样式... */
  position: relative;
}

.box {
  /* 其它的基础样式... */
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
}
```

该方案和前一个方案最终效果是一样，该方案的步骤如下：

1. 通过设置**绝对定位** `top:0; bottom:0; left:0; right:0;`，让浏览器知道元素被限制”在父容器内四边，这样有了一个**明确的空间范围**
2. 再通过设置 `margin: auto`，浏览器就可以根据 `父容器大小 - 元素大小 = 剩余空间`，把剩余空间平分给 `margin: auto`，实现水平垂直方向上的居中

[在线查看效果](https://codepen.io/wjw020206/pen/vEOLrPa)

**✅ 优点：** 

- 兼容性好，适用于 IE 等老版本浏览器
- 每次修改元素大小**不需要同步修改 `margin` 值，无需手动计算元素大小的一半**

**⚠️ 缺点：** 只能用于**固定尺寸**的元素，不适合宽高不确定的情况。



### absolute + calc()

```css
.container {
  /* 其它的基础样式... */
  position: relative;
}

.box {
  /* 其它的基础样式... */
  position: absolute;
  top: calc(50% - 50px);
  left: calc(50% - 50px);
}
```

该方案与**前面的 absolute + 负 margin 方案**原理相同，使用了 `calc()` 函数替代了 `margin` 负值来计算居中的位置。

[在线查看效果](https://codepen.io/wjw020206/pen/pvJgZyb)

**⚠️ 缺点：**

- 该方案依赖 `calc()` 函数的兼容性，具体兼容性可以参考 [Can I use](https://caniuse.com/calc)
-  需要提前知道元素大小，修改元素大小**需要同步修改 `calc()` 函数中减去的值**
- 相比前两个方案，该方案既缺乏兼容性（IE9+），又需要手动计算元素大小的一半，**不推荐使用**



## 不固定宽高元素



### absolute + transform

```css
.container {
  /* 其它的基础样式... */
  position: relative;
}

.box {
  /* 其它的基础样式... */
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
```

该方案与**前面的 absolute + 负 margin 方案**原理相同，使用了 `transform` 替代了 `margin` 负值来计算居中的位置。

因为`translate(-50%, -50%)` 的百分比是**相对于元素本身的宽高**，所以不需要提前知道元素的具体尺寸。

[在线查看效果](https://codepen.io/wjw020206/pen/pvJgZNE)

**✅ 优点：** 无需提前知道元素大小，修改元素大小**不需要同步修改相关的值**

**⚠️ 缺点：** 该方案依赖 `transform()` 函数的兼容性，具体兼容性可以参考 [Can I use](https://caniuse.com/transforms2d)
