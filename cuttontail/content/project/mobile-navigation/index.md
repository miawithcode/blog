---
title: "如何实现移动端响应式菜单"
date: 2023-10-07T14:49:30+08:00
lastmod: 
tags: [""]
summary: ""
slug: 
draft: true
---

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

### 8.1 移动端菜单

我们在[前面的章节](http://localhost:1313/blog/what-i-learned-after-developing-a-portfolio-website/#62-%E5%93%8D%E5%BA%94%E5%BC%8F%E5%AF%BC%E8%88%AA%E8%8F%9C%E5%8D%95) 创建了响应式的导航菜单，现在菜单在移动端只会显示一个图标，但点击图标什么都不会发生，现在我们来 fix that。

1. 首先在 HTML 文件中添加所有导航菜单中包含的元素。（这里省去了`<svg>`的具体内容，因为太长了。）

```html
<header>...</header>
<!-- Mobile Navigation -->
<div class="mobile-nav">
  <nav>
    <ul class="mobile-nav__menu">
      <li><a class="mobile-nav__link" href="#">About</a></li>
      <li><a class="mobile-nav__link" href="#">Work</a></li>
      <li><a class="mobile-nav__link" href="#">Contact</a></li>
      <li class="mobile-nav__line"></li>
      <li>
        <button id="theme-toggle" class="mobile-nav__sun">
          <svg>...</svg>
        </button>
      </li>
      <li><a class="mobile-nav__btn btn" href="#">Resume</a></li>
    </ul>
  </nav>
</div>
<!-- End of Mobile Navigation -->
<main>...</main>
```

2. style it

```css
.mobile-nav {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 999;
  width: 100%;
  height: 100%;
  background-color: var(--clr-dark);
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.mobile-nav__menu {
  list-style: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 1rem;
}

/* ... */
```

由于此时看不到菜单图标了，所以回到`header.css`

```css
.header {
  position: relative;
  z-index: 9999;
}
```

3. 用 JavaScript 设置点击图标时，移动端菜单打开与关闭。JavaScript 主要要做的是当点击菜单图标时，打开我们刚刚创建的移动端菜单，在菜单打开的情况下点击菜单图标时，会关闭菜单。

- 首先回到`mobile-nav.css`，刚刚在编写移动端菜单时，设置`display: flex`，因为我们要看着菜单才能编写，但现在可以把`display`设置为 none，因为默认情况下，菜单是关闭的。在需要打开时，我们通过 JavaScript 来将`display`设置为`flex`。

```css
.mobile-nav {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 999;
  width: 100%;
  height: 100%;
  background-color: var(--clr-dark);
  display: none;
  justify-content: center;
  align-items: center;
  text-align: center;
}
```

- 在 src 文件夹中创建文件夹`utils`，在`utils`中创建`mobile-nav.js`。在开始写代码前，需要把所有代码包含在一个箭头函数内，再通过 export 导出

```javascript
const mobileNav = () => {};

export default mobileNav;
```

然后在`main.js`内导入，再调用这个函数。之后的 javascript 文件也需要这样做。

```javascript
import mobileNav from "./utils/mobile-nav";

mobileNav();
```

- JavaScript 代码

```javascript
const mobileNav = () => {
  const headerBtn = document.querySelector('.header__bars'); /* 选中菜单图标 */
  const mobileNav = document.querySelector('.mobile-nav'); /* 选中整个移动端菜单 */
  const mobileLinks = document.querySelectorAll('.mobile-nav__link'); /* 选中菜单中的链接 */

  let isMobileNavOpen = false; /* 设置状态变量 */

  headerBtn.addEventListener('click', () => { /* 当菜单图标被点击时 */
    isMobileNavOpen = !isMobileNavOpen; /* 转化状态变量，如果点击前是false，说明菜单没有打开，则设置为true，代表菜单打开；如果点击前是true，说明菜单已经打开，点击是为了关闭菜单，则设置状态变量为false */

    if (isMobileNavOpen) {
      mobileNav.style.display = 'flex'; /* 当菜单打开时，设置display为flex，因为默认情况下是none */
      document.body.style.overflowY = 'hidden'; /* 在菜单打开后，不允许再滑动页面 */
    } else {
      mobileNav.style.display = 'none';
      document.body.style.overflowY = 'auto';
    }
  });

  mobileLinks.forEach((link) => {
    link.addEventListener('click', () => {
      isMobileNavOpen = false;
      mobileNav.style.display = 'none';
      document.body.style.overflowY = 'auto';
    });
  });
};

export default mobileNav;
```
有一个问题，设定`overflow-y = "hidden"`后，在桌面缩小到移动端窗口大小时，屏幕确实不再会滚动，可当我在真正的手机上打开我的demo时，移动端菜单会发生滚动。调查搜索之后，找到了[解决方法](https://markus.oberlehner.net/blog/simple-solution-to-prevent-body-scrolling-on-ios/)。
应用到我们的代码中应该是：
```javascript
  let scrollPosition = 0;

  headerBtn.addEventListener("click", () => {
    isMobileNavOpen = !isMobileNavOpen;

    if (isMobileNavOpen) {
      scrollPosition = window.pageYOffset;
      mobileNav.style.display = 'flex';
      mobileNav.style.position = 'fixed';
      document.body.style.overflow = 'hidden';
      document.body.style.top =  `-${scrollPosition}px`;
    }else {
      mobileNav.style.display = 'none';
      mobileNav.style.position = 'absolute';
      document.body.style.overflow = 'auto';
      document.body.style.top = '0';
      window.scrollTo(0, scrollPosition);
    }
  });
```
