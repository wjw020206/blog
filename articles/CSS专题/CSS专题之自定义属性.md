# CSS专题之自定义属性



## 前言

> 石匠敲击石头的第 12 次

CSS 自定义属性是现代 CSS 的一个强大特性，可以说是前端开发需知、必会的知识点，本篇文章就来好好梳理一下，如果哪里写的有问题欢迎指出。



## 什么是 CSS 自定义属性

CSS 自定义属性英文全称是 **CSS Custom Properties**，简称自定义属性，也被称为 **CSS 变量**，是允许开发者样式表中定义和重复使用值的一种机制，类似于其它编程语言（如 JavaScript 等）中的变量。



## 为什么需要 CSS 自定义属性

CSS 语言是一种声明式语言，不像其它语言有变量、条件和逻辑等特性，导致在**维护、复用、动态控制**方面存在不少局限。

正因如此，社区中诞生了各种 CSS 预处理器，如 Sass（Scss）、Less、Stylus 等。它们通过引入变量、运算、条件语句等机制，弥补了原生 CSS 的不足，大大提高了样式开发的效率与可维护性。

其中，**变量**功能尤其重要，它让我们可以在多个地方复用相同的值，一旦需要修改，只需改一处，大幅降低了维护成本，但预处理器的变量是在**编译阶段**生效的，无法在浏览器中运行时动态更新，也不能与 DOM 或 JavaScript 交互。

为了解决这一问题，CSS 自定义属性应运而生。



## 基础语法



### 变量声明

CSS 变量的声明由 `--` 开头，便于浏览器区分**自定义属性**和**原生属性**。

```css
.box {
  --color: red;
  color: red;
}
```

上述代码中 `color` 是原生属性，`--color` 则是自定义属性。

自定义属性支持各种值。

```css
:root {
  --link: 'link';
  --color: #f00;
  --back-ground: red;
  --height: 68px;
  --padding: 10px 20px;
  --line-height: 1.5;
  --transition-duration: 0.5s;
  --margin-top: calc(2vh + 20px);
}
```

**⚠️ 注意：** 

- 变量名命名规则比较松散，可以是任何有效的字符，比如：`中文`、`大写字母`、`驼峰命名`、`中距线`、`emoji` 和`HTML` 实体等

  ```css
  :root {
    --COLOR: #f00;
    --color: #f00;
    --内边距: 10px;
    --backGround: red;
    --calc: 10px;
    --🤪: '哈哈哈';
  	--©: '版权';
  }
  ```

- **变量名大小写敏感**，`--color` 和 `--COLOR` 是两个不同的变量

- **变量是和选择器是强绑定的，只能在声明块中声明变量**

  ```css
  --color: red; /* 无效声明 */
  
  :root {
    --color: red; /* 有效声明 */
  }
  ```



### 变量使用

通过使用 `var()` 函数来使用变量。

```css
.box {
  color: var(--color);
}
```

`var()` 函数**可以接受两个值**，第一个值是 CSS 自定义属性，第二个值是一个**回退值**，回退值在第一个值（CSS 自定义属性）无效时保证 `var()` 函数有值。

```css
.box {
  color: var(--color, #fff);
}
```

上述代码中如果 `--color` 不存在，则使用回退值 `#fff`。

**⚠️ 注意：** 

- **`var()` 函数第二个参数不处理内部的逗号或空格**，都视为参数的一部分

  ```css
  .box {
    padding: var(--pad, 10px 15px 20px);
  }
  ```

- 变量值只能用作属性值，**不能用作属性名**

  ```css
  .box {
    var(--margin): 20px; /* 无效 */
  }
  ```

- 如果变量值是字符串，可以与其它字符串拼接

  ```css
  .box {
    --string: 'hello';
    --string2: var(--string)' world';
  }
  ```

- 如果变量值是数值，不能与数值单位拼接使用

  ```css
  .box {
    --height: 20;
    height: var(--height)px; /* 无效 */
  }
  ```

  **必须使用 `calc()` 函数**将它们连接起来。

  ```css
  .box {
    --height: 20;
    height: calc(var(--height) * 1px); /* 有效 */
  }
  ```

- 如果变量值带单位，则不能写成字符串

  ```js
  /* 无效 */
  .box {
    --height: '20px';
    height: var(--height); 
  }
  
  /* 有效 */
  .box {
    --height: 20px;
    height: var(--height); 
  }
  ```

- 如果变量值对于 CSS 属性来说是一个无效值时，会做降级处理

  ```css
  .box {
    --height: 20px;
    color: var(--height);
  }
  ```

  上述代码中，`color` 属性不支持 `20px`，会被降级为 `initial`（在 Chrome 浏览器中是一个 `#000` 的颜色值），如果 `var()` 函数中有第二个参数，并且第二个参数值是有效值，则降级为第二个参数值。

  ```css
  .box {
    --height: 20px;
    color: var(--height, red); /* 等同于 color: red; */ 
  }
  ```
