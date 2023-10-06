---
title: "开发一个 Portfolio 网页可以学到什么"
date: 2023-10-03T15:29:32+08:00
# lastmod:
tags: ["html", "css", "javascript", "frontend"]
summary: ""
slug: what-i-learned-after-developing-a-portfolio-website
draft: true
---

## 1. 前言

在练习这个网页之前，我通过文档重新复习了一遍 HTML 和 CSS，有 JavaScript 基础但不多。开发这个网页没有用到任何前端框架。这个网站给我最大的收获是响应式的实际应用，也给了我一个网站的文件结构的初步印象。对于一个刚学过前端基础，不会任何框架，还没有真正实操过的新手来说，这个练习的帮助非常大。我终于知道应该如何移动端的响应式菜单，以及夜间模式的切换原来这么简单。

创建这个网站的过程中使用到的基本工具有 [Node.js](https://nodejs.org/en)、 [Git](https://git-scm.com/)、 [Vite](https://vitejs.dev/)。

这里是[网站 Demo](https://mia-portfolio-website-practice.vercel.app/)，[Github Repo](https://github.com/miawithcode/building-portfolio-website) 和[原视频教程](https://youtu.be/dLDn_k8GmaU?si=qF_sc1m7io16S7cS)。

---

## 2. 工具资源

### 2.1 选择字体

以前需要字体资源时我只知道 [Google Font](https://fonts.google.com/)，通过教程我了解到了另一个字体资源：[Font Share](https://www.fontshare.com/)。  
Font Share 的使用方法和 Google Fonts 类似：在 HTML 的头部导入字体链接，在 CSS 文件中直接通过字体名使用。

### 2.2 选择颜色

自己搭配颜色是一件很困难的事情，但通过这个教程我才知道原来可以直接从[Tailwind 文档](https://tailwindcss.com/docs/customizing-colors) 中提供的颜色中进行颜色搭配。像 Tailwind 这样的前端框架提供的颜色是用特殊的设计模式，且有系统地创建的，对于个人项目的使用已经足够。

当想要找到某一颜色的更深或更浅色时，可以在[W3 School 的 Color Converter](https://www.w3schools.com/colors/colors_converter.asp) 中粘贴该颜色的值，然后点击【**Use this color in our Color Picker**】，就会看到同一色调由浅到深的 HEX 值，并能看到刚刚粘贴的颜色处在有深到浅的哪个位置。

### 2.2 选择 icon

与字体资源同样，有关 icon 资源我只知道 [Font Awsome](https://fontawesome.com/)，通过这个教程我了解到另一个新的 icon 资源： [Heroicons](https://heroicons.com/)。  
使用 Font Awsome 的步骤会更复杂一些，需要注册登陆，获取自己的 Kit，再导入 JavaScript 文件。使用 Heroicons 的话，只需要进入网站，找到想要的 icon ，点击【**Copy SVG**】，再复制到想用的地方，就可以直接使用了。

复制 svg 代码之后有几件事要注意：

1. 在 HTML 中复制 svg 后，先删除 svg 中自带的`class`。
2. 设定了 svg 的 `width` 和 `height` 之后，才能看到图标。

---

## 3. 使用 Vite 创建项目

在刚开始学习前端时，我们通常会在某个文件夹下直接创建`index.html`、`style.css`和`script.js`。但在真正的项目中，一般不会这样从零开始，而是使用 Web 打包工具为我们提前创建好一些基本的文件，这个项目中使用的 Web 打包工具是 [Vite](https://vitejs.dev/)。

### 3.1 用 Vite 创建项目文件夹

在创建这个项目的过程中，只需要知道 Vite 的一些简单特性和命令就足够了。之后可以再花额外的时间去了解 Vite 的全部内容。
接下来：

1. 点开 Vite 首页
2. 找到菜单栏的【**Guide**】
3. 在【**Getting Started**】的文章中找到标题【**Scaffolding Your First Vite Project**】
4. 找到【**npm**】命令并复制：

```bash
npm create vite@latest
```

打开终端，进入想要存放项目的文件夹（如桌面、文档），输入刚刚复制的命令并回车。

```bash
cd Desktop
npm create vite@latest
```

回车后：

1. Vite 会提示输【**Project Name**】，给项目取一个名字然后输入，这会创建一个以【**Project Name**】命名的文件夹。
2. 提示选择【**Framework**】，因为我们在这个项目中没有用到任何框架，所以这里选择`Vanilla`
3. 提示选择【**JavaScript**】还是【**TypeScript**】，这里选择`JavaScript`。
4. 回车之后等待【**done**】的提示

然后继续在终端进入进刚刚创建的项目文件夹：

```bash
cd portfolio
```

1. 用 node 安装包
   ```bash
   npm i
   ```
2. 测试项目是否 work，输入下行代码。如果没有任何报错，则可以`control + c`结束终端。
   ```bash
   npm run dev
   ```

### 3.2 修改部分文件和文件结构

用 VS Code 打开项目文件夹，或者在终端`code .`打开文件夹。
Vite 会自动创建`index.html`，`style.css`和`main.js`，  
（图片）

1. 修改文件
   - 打开`style.css`，删除里面的所有代码
   - 打开`main.js`，删除除了第一行`import './style.css'`之外的所有代码。（通常来说，在 HTML 文件中`<meta link>`标签中导入外部 CSS 文件。但是有了 Vite，只用在`main.js`中导入 css 文件就好了。）
   - 打开`index.html`，更改网页标题，也可以更改 favicon，这项是可选的。删除下行：
     ```html
     <div id="app"></div>
     ```
2. 删除文件
   - 删除`counter.js`文件
   - 删除`javajavascript.svg`文件
3. 创建文件夹

   - 创建`styles`文件夹，并将`style.css`移动到该文件夹中
   - 创建`src`文件夹，并将`main.js`移动到该文件夹中
   - 因为移动了文件夹，所以需要在导入文件的位置修改文件的路径，需要更改的有两个文件，一是`index.html`，二是`main.js`：

   ```html
   <!--
     在 index.html 文件中
     找到<script>标签
     将原来src属性中的“main.js”修改为“./src/main.js”
    -->

   <script type="module" src="./src/main.js></script>
   ```

   ```javascript
   /* 
   在 main.js 文件中
   将 import './style.css' 修改为 import './styles/style.css'
    */

   import "./styles/style.css";
   ```

### 3.3 预览网页

在 VS Code 中打开终端，输入下行命令即可开始预览网页。

```bash
npm run dev
```

（我通常预览网页的方式是使用插件[Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)，但是这次使用 Vite 提供的实时预览。）

---

## 4. HTML 结构与命名

### 4.1 HTML 结构

将一个网页的结构主要分为 3 个部分，header、main、和 footer。main 中包括多个代表网页中的内容部分的 Section。有几部分内容就创建几个`<section>`，且逐个 Section 进行开发，暂未开发到的 Section 可以先注释掉。

以前我只会`<div>`来代表某个网页的一部分，现在我学会了又更有语义化的标签`<section>`来开发网页。

```html
<header>
  <nav></nav>
</header>
<main>
  <section></section>
  <!-- <section></section> -->
  <!-- <section></section> -->
</main>
<footer></footer>
```

### 4.2 BEM 命名法

---

## 5. 添加基本样式

在正式开发页面前先添加一些基本的样式，添加基本样式包括**重置样式**、**定义颜色变量和 Size 变量**、**创建可复用实用类**（如按钮、容器、间距）。

### 5.1 添加 modern normalize

[modern normalize](https://github.com/sindresorhus/modern-normalize) 是一个 Github repo。因为不同的浏览器对各种 HTML 元素都有默认样式，一个浏览器中的默认样式在下一个浏览器中可能会有所不同，所以我们使用 modern nomalize 来重置这些样式，让 HTML 元素在所有浏览器中的显示一致。

1. 虽然 modern normarlize 的`README.md`中有用 Node 安装的命令，但是我们直接找到 `modern-normalize.css`  
   （图片）
2. 打开后点击`Raw`
   （图片）
3. 全选所有代码并复制
4. 回到 VS Code 中，在`styles`文件下创建`modern-normalize.css`，并粘贴刚刚复制的代码
5. 在`main.js`中的第一行导入`modern-normalize.css`，因为我们希望`modern-normalize.css`在我们的项目中的优先级是最低的。
   ```javascript
   import "./styles/modern-normalize.css";
   ```

### 5.2 重置元素样式

通常来说，重置元素样式的第一件事是给全局选择器添加`box-sizing: border-box`。但由于`modern-normalize.css`已经写过了这段代码，所以我们**并不需要再写一遍**。

```css
/* style.css */
*,
::before,
::after {
  box-sizing: border-box;
}
```

以下是需要使用的重置代码块：

```css
/* style.css */
* {
  margin: 0; /* 将所有元素的外边距设置为0 */
  line-height: calc(
    1em + 0.5rem
  ); /* line-height设置成1.5是常见，的，但如果字体太大，行间距也会看起来太大，所以使用calc函数计算行高相对于字体大小的相对值：1个字体大小的值加上0.5倍根元素的大小的值，也就是8px */
}

html {
  scroll-behavior: smooth; /* 跳转到同一页面的不同 Section 时，添加平滑的过渡（Transition）*/
}

body {
  font-family: "General Sans", sans-serif; /* 定义字体样式 */
}

img,
picture,
video,
canvas,
svg {
  display: block; /* 这些元素 display 的默认值是inline ，但其实实际的网页中，很少看到它们是显示在行内的 */
  max-width: 100%; /* 让图片在必要时缩小，但绝不放大到大于其原始尺寸 */
  user-select: none; /* 不让用户选中这些元素 */
}

button {
  display: inline-block; /* 让 button 显示为 inline-block */
  padding: 0; /* 重置 button 的内边距为0 */
  border: none; /* 重置 button 的边框为无 */
  background: none; /* 重置 button 的背景为无 */
  cursor: pointer; /* 设置悬停在 button 上的鼠标为手指符号 */
  color: inherit; /* 继承父元素的颜色 */
}
```

### 5.3 定义颜色变量

下列颜色只是一个示例参考，创造自己的项目的时候要根据实际情况更改，但主要思路是从 Tailwind 选择颜色，并创建颜色变量。

```css
/* style.css */
:root {
  --clr-dark: #070a13; /* 教程中 Tailwind 中最深的颜色 Slate 900 （11%）不够深，所以在 Color Converter 中找到了5%的更深色，但写这篇博客时， Tailwind 已经有了 Slate 950 更深色。但是这个思路依然可以参考。 */
  --clr-light: #f1f5f9; /* light 颜色用的是 Slate 100，夜间模式下主标题的颜色 */
  --clr-slate400: #94a3b8; /* 夜间模式下的副标题文本颜色 */
  --clr-slate600: #475569; /* 链接文本、段落文本的颜色 */
  --clr-slate800: #1e293b; /* 分割线的颜色 */
  --clr-rose: #e11d48; /* 链接色、按钮色等，rose 颜色用的是 Rose 600 */
  --clr-indigo: #4f46e5; /* 文本强调色， ingigo 颜色用的是 Indigo 600*/

  /* rose rgb(225, 29, 72) */
  /* indigo rgb(79, 70, 229) */
}
```

创建好颜色变量后可以继续重置样式，只不过这次重置的主要是和颜色有关的样式，且不同的项目使用的颜色不同，但之前的重置样式是可以通用的。

```css
/* style.css */
a {
  color: var(--clr-rose);
}

strong {
  color: var(--clr-indigo);
}
```

### 5.4 定义 Size 变量

不同 Size 的值参考的也是[Tailwind 设计的值](https://tailwindcss.com/docs/font-size) 。

```css
/* style.css */
:root {
  /* sizes */
  --size-xxs: 0.5rem;
  --size-xs: 0.75rem;
  --size-sm: 0.875rem;
  --size-base: 1rem;
  --size-lg: 1.125rem;
  --size-xl: 1.25rem;
  --size-2xl: 1.5rem;
  --size-3xl: 1.875rem;
  --size-4xl: 2.25rem;
  --size-5xl: 3rem;
  --size-6xl: 3.75rem;
  --size-7xl: 4.5rem;
  --size-8xl: 6rem;
  --size-9xl: 8rem;
  --size-10xl: 10rem;
}
```

### 5.5 创建可复用实用类

可复用的实用类不在`style.css`中定义了，而是在文件名为`utils.css`的文件中定义：

1. 在`style`文件夹下创建`utils.css`
   （图片）
2. 在`main.js`中导入了`utils.css`，并在未来导入其他 CSS 文件时，确保`utils.css`永远是最后一个导入的 CSS 文件，因为它的优先级需要是最高的，否则里面的样式不会生效。
   (图片)

在`utils.css`中定义那些相同样式并经常使用的元素，如按钮、容器、Section。

1.  首先添加按钮的样式：

    ```css
    /* utils.css */
    .btn {
      display: inline-block;
      font-weight: 600;
      text-decoration: none;
      letter-spacing: -0.05em; /* 让字与字之间更紧凑 */
      background-color: var(--clr-rose);
      color: var(--clr-light);
      padding: 0.5em 1em; /* 按钮的上下内边距是按钮字体大小的0.5倍，左右边距是按钮字体大小的1倍 */
      border-radius: 6px;
      /* box-shadow: ; */
      transition: all 0.3s;
    }

    .btn:hover {
      /* 鼠标悬停在鼠标上的样式 */
    }
    ```

2.  添加容器（Container）的样式，且容器是响应式的。响应式容器的媒体查询（Media Query）具体设计见[下一节：响应式设计]() 。  
    然而，有一件事是需要提前了解的，由于这个项目的响应式设计是移动端优先的，所以在`@media`外的所有样式表示的是**在屏幕尺寸小于 475px 的设备上显示的样式**。

        ```css
        /* utils.css */
        .container {
          width: 100%; /* 一般来说，不推荐在容器（container）上使用百分比来设置大小，但在屏幕尺寸小于475px的设备上，没有什么其他选择 */
          margin-left: auto; /* 的确可以用简写margin: 0 auto，但由于utils.css有最高的优先级，如果在这里设置容器（container）的上下外边距为0，那我们将不再能为有类名为container的元素添加上下外边距 */
          margin-right: auto; /* 左右外边距设置为auto将为使容器元素居中 */
          padding-left: 0.5rem; /* 将容器的左内边距设置为根元素的0.5倍 */
          padding-right: 0.5rem; /* 将容器的右内边距设置为根元素的0.5倍 */
        }

        ```

3.  添加 Section 的样式，一个网页的内容分为多个部分，每个部分之间会有一些间距。

    ```css
    .section {
      margin-top: 5rem; /* 顶部外边距为根元素大小的5倍 */
    }

    /* 我们希望在大于1024px的屏幕上，网页每个部分的间距有所增加 */
    @media (min-width: 1024px) {
      .section {
        margin-top: 10rem;
      }
    }
    ```

---

## 6. 响应式设计

Mobile First：从移动端开始设计，再慢慢扩大。
styles outside the media queries are for default styles and for screens smaller than 475px

如果想要 Desktop first 替换所有 media query 中的`min-width`成`max-width`。然后在 media query 外的 styles 应用在屏幕比最后一个 media query 还大的屏幕（1536px）上

标准的方式是 Mobile First

### 6.1 响应式屏幕断点（Breakpoint）

当`max-width`的大小设置为和`min-width`设置的断点尺寸相同时，容器元素会在浏览器窗口碰到它的一瞬间缩小。

```css
/* xs  */
@media (min-width: 475px) {
  .container {
    max-width: 475px;
  }
}

/* sm  */
@media (min-width: 640px) {
  .container {
    max-width: 640px;
  }
}

/* md  */
@media (min-width: 768px) {
  .container {
    max-width: 768px;
  }
}

/* lg  */
@media (min-width: 1024px) {
  .container {
    max-width: 1024px;
  }
}

/* xl  */
@media (min-width: 1280px) {
  .container {
    max-width: 1280px;
  }
}

/* 2xl  */
@media (min-width: 1536px) {
  .container {
    max-width: 1536px;
  }
}
```

### 6.2 响应式导航菜单

由于开始开发时默认在小于 475px 的屏幕上开发，我们可以先媒体查询外开发完整的导航栏代码，完成后再将代码移动到`@media (min-width: 768px){}`中。然后再在媒体查询外设置导航栏菜单的容器`<ul>`的属性`display: none`。

这样可以保证只有浏览器窗口放大到大于 768px 时，导航栏才会出现。

```css
.header__menu {
  display: none;
}

/* md */
@media (min-width: 768px) {
  .header__menu {
    display: flex;
    /* ... */
  }

  /*
  ...
  */
}
```

导航栏显示的问题解决后，接下来解决小屏幕上图标的问题：

1. 在导航栏的`<ul>`无序标签后加上图标按钮：

   ```html
   <!-- index.html -->

   <header class="header">
     <nav>
       <ul class="header__menu">
         <li>...</li>
         <li>...</li>
         <li>...</li>
       </ul>

       <button class="header__bars">
         <svg>...</svg>
       </button>
     </nav>
   </header>
   ```

2. 设置图标的大小，并设置图标的属性`display: block`，再在大于 768px 的屏幕上隐藏这个菜单图标：`display: none`。

   ```css
   /* header.css */

   /*
   ...
   */

   .header__bars {
     width: var(--size-2xl);
     height: var(--size-2xl);
     display: block;
     /* ... */
   }

   /* md */
   @media (min-width: 768px) {
     .header__bars {
       display: none;
     }
   }
   ```

### 6.3 从一列布局响应到两列布局(文本 + 图片)

```html
<section class="about container section">
  <div class="about__content"></div>
  <div class="about__img"></div>
</section>
```

开发时因为以移动端优先，所以默认都是一行布局，一般在大于 1024px 的屏幕上开始显示两行布局。

```css
.about {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

@media (min-width: 1024px) {
  .about {
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }
}
```

### 6.3 从一列布局响应到两列布局(图片 + 图片)

在共有 6 张图片的情况下，两行布局呈现 2x3，此时用 Grid 较好。
当空间足够展示 2 张图时，允许图片成连行布局

```html
<div class="img-container">
  <img src="" alt="" />
  <img src="" alt="" />
  <img src="" alt="" />
  <img src="" alt="" />
  <img src="" alt="" />
  <img src="" alt="" />
</div>
```

```css
.img-container {
  display: grid;
  grid-template-column: repeat(autofit, minmax(300px, 1fr)) /* autofit的意思是不再重复固定的值，而是只要空间足够，能重复几次就重复几次，minmax()第一个值的意思是我们允许图片大小的最小值是多少，第二个值是我们允许图片能放大的最大值是多少，当空间放大到可以容纳2x300px，图片会停止增长而展示2列图片*/
  grid-gap: 1rem;
}

/* sm */
@media (min-width: 640px) {
  grid-template-column: repeat(autofit, minmax(500px, 1fr)) /* 因为当最小值设置为300px时，最终autofit会展示4列图片，所以设置在大于640px的屏幕上，图片的最小值是500px，这样能保证一直都是2列图片 */
  grid-gap: 1rem;
}
```

### 6.4 三列响应式布局

当屏幕空间足够大时，显示三列布局，屏幕空间只够 2 列的宽度时，只显示 2 列，屏幕空间不够 2 列的宽度时，只显示一列。

```html
<div class="container">
  <div></div>
  <div></div>
  <div></div>
</div>
```

```css
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}

.container div {
  flex: 1;
  min-width: 250px;
}
```

### 6.5 不同屏幕尺寸下的字体 size 增长

- 在屏幕尺寸**小于 475px(xs)**的屏幕中
  - 链接文本的大小是 xs
  - 图标的大小是 base
  - 导航栏按钮的大小是 xs
  - hero 的按钮是 sm
  - 导航栏汉堡包菜单栏图标是 2xl
  - 段落文本的大小是 sm（所以 xs 的段落文本大小是 base）
  - 正常一个 section 的标题大小是 2xl(xs 的标题尺寸是 3xl and so on)

header 导航栏的第一次大小增长在 lg 上，所有尺寸除了图标向前增加一个 variable。

- 如链接文本的大小是 sm
- 图标的大小是 xs
- 按钮的大小是 sm

Hero（在**小于 475px(xs)**的屏幕中）
Hero 的第一个 media query 是 xs

- 头像的大小在 xs 中，从 6rem 增长到 6.5rem
  第二个 media query 是 lg
- 此时不增加 gap
- 头像从 6.5rem 增长到 8rem
  第三个是 xl
- gap 增加到 2rem
- 头像增加到 10rem

title、subtitl、段落文本只在 xs、lg、xl 有大小变化

### 6.6 什么时候需要增加 gap

在**小于 475px(xs)**的屏幕中，

- hero 中的 gap 是 1rem
  - 在 xs 中设置为 1.5rem
- about 的 gap 是 1rem

在 xs 的屏幕上

- about 的 gap 增加到 1.5rem

在 lg 的屏幕上

- about 的 gap 不增加

在 xl 的屏幕上

- about 的 gap（or margin） 增加到 2rem

---

## 7. 布局

### 7.1 Zigzag 布局

```html
<!-- Project 1 -->
<div class="project__container image1">
  <div class="project__img-wrapper">
    <img src="" alt="" />
  </div>
  <div class="project__content content1">
    <h3 class="project_subtitle"></h3>
    <p class="project_description"></p>
    <a class="project__btn"></a>
  </div>
</div>

<!-- Project 2 -->
<div class="project__container">
  <div class="project__img-wrapper image2">
    <img src="" alt="" />
  </div>
  <div class="project__content content2">
    <h3 class="project_subtitle"></h3>
    <p class="project_description"></p>
    <a class="project__btn"></a>
  </div>
</div>
```

```css
/* sm */
@media min-width(640px) {
  /*在大于640px的屏幕上显示Zigzag布局 */
  .project-container {
    display: grid;
    grid-template-column: 1fr 1fr;
    grid-template-areas:
      "image1 content1"
      "content2 image2";
    place-items: center; /* justify-content和align-items的简写 */
  }

  .project__content {
    padding: 0 1rem;
  }

  .image1 {
    grid-area: image1;
  }

  .image2 {
    grid-area: image1;
  }

  .content1 {
    grid-area: content1;
  }

  .content2 {
    grid-area: content2;
  }
}
```

---

## 8. 功能

### 8.1 移动端菜单

我们在[前面的章节](http://localhost:1313/blog/what-i-learned-after-developing-a-portfolio-website/#62-%E5%93%8D%E5%BA%94%E5%BC%8F%E5%AF%BC%E8%88%AA%E8%8F%9C%E5%8D%95) 创建了响应式的导航菜单，现在菜单在移动端只会显示一个图标，但点击图标什么都不会发生，现在我们来 fix that。

1. 首先在 HTML 文件中添加所有导航菜单中包含的元素。（这里省去了<svg>的具体内容，因为太长了。）

```html
<header>...</header>
<!-- Mobile Navigation -->
<div class="mobile-nav">
  <nav>
    <ul class="mobile-nav__menu">
      <li><a class="mobile-nav__link" href="#about">About</a></li>
      <li><a class="mobile-nav__link" href="#featured">Work</a></li>
      <li><a class="mobile-nav__link" href="#contact">Contact</a></li>
      <li class="mobile-nav__line"></li>
      <li>
        <button id="theme-toggle" class="mobile-nav__sun"><svg></svg></button>
      </li>
      <li><a class="mobile-nav__btn btn" href="#">Resume</a></li>
    </ul>
  </nav>
</div>
<!-- End of Mobile Navigation -->
<main>...</main>
```

### 8.2 夜间模式

### 8.3 图片懒加载

图片懒加载（lazy loading）有两种方法可以实现，较为简单的方法是在`<img>`标签中加入 Attribute：`loading="lazy"`。

```HTML
<img loding="lazy" />
```

在 Demo 中用到的是较复杂的方法。

### 8.4 自定义滚动条

---

## 9. 学到的技巧

### 9.1 组件思想

假设一个页面有 header、hero、about、project、contact、footer 共 6 个部分，每个部分的 css 视作组件（components）的 css。所以在 styles 文件夹中，再创建一个 components 文件夹，添加以每个部分的名字命名的 css，如`header.css`、`about.css`、`contact.css`等。  
（图片）

根据开发的进程，逐步添加每部分的`.css`文件，并导入`main.js`中，导入的组件 CSS 文件要确保在`style.css`之下，在`.utils.css`之上，如：

```javascript
import "../styles/style.css";
import "../styles/components/header.css";
import "../styles/components/about.css";
import "../styles/utils.css";
```

### 9.2 复用的媒体查询断点代码

在`utils.css`的顶部添加注释后的断点代码，当我们需要这些断点时，可以直接复制粘贴。

```css
/* xs  */
/* @media (min-width: 475px) {} */

/* sm  */
/* @media (min-width: 640px) {} */

/* md  */
/* @media (min-width: 768px) {} */

/* lg  */
/* @media (min-width: 1024px) {} */

/* xl  */
/* @media (min-width: 1280px) {} */

/* 2xl  */
/* @media (min-width: 1536px) {} */
```

在导入一个组件的 CSS 文件后，第一件要做的事是复制粘贴上述断点代码。

### 9.3 使用 ch 作为段落文本的宽度的大小单位

用`ch`来设置段落文本的宽度

```css
p {
  max-width: 60ch;
}
```

且不在媒体查询中更改它的大小

### 9.4 使用 emoji 作为列表的样式

如果想用 emoji 作为列表的样式 instead of default disk，直接在 Google 搜索【unicode + emoji 名字】，比如`unicode thumbs up`，得到结果`U+1F44D`，再将`U+`替换成`\`填入`list-style`。

```css
ul {
  list-style-type: "\1F44D"；;
}
```

### 9.5 在列表样式和列表文本间添加间隙

```css
ul li::before {
  content: "";
  margin-left: 0.5em;
}
```

### 9.6 将单位 px 的值转换为单位 rem 的值

出于尽量避免使用固定值的目的，我们需要在设置宽度或高度时将 px 的值转换为 rem 值。

1. 首先可以在 Chrome 的开发者工具中查看图片的具体大小
2. 假设一张图片的大小是 459 x 459，则计算 459/16 = 28.6875
3. 即 459px = 28.6875rem

### 9.7 用 Chrome 进行网页截图

- 在 Chrome 上打开开发者工具，
- `Command + Shift + P`(Mac) Control + Shift + P(Windows)
- screenshot，选择 capture screenshot

### 9.8 添加图片覆盖色

```html
<div class="container">
  <img src="" alt="" />
</div>
```

```css
.container {
  position: relative;
}

.container::after {
  content: "";
  background-color: rgba(79, 70, 229, 0.4);
  width: 100%;
  height: 100%;
  positon: absolute;
  top: 0;
  left: 0;
  z-index: 1;
  transition: background-color 0.3s;
}

.container:hover::after {
  background-color: rgba(79, 70, 229, 0.1);
}
```

### 9.9 善用`margin: 0 auto`居中

---

## 10. 结语

因为有太多细节了，在写这篇记录的时候把 3 个小时的视频又看了一遍，边看边记，历时？天才写完，最后出来有这么多内容。理了一下脑袋果然清醒多了，有了这篇日后也方便回顾。接下来我要开发更多更多的网页！
