---
title: "如何实现夜间模式"
date: 2023-10-07T14:55:40+08:00
lastmod: 
tags: [""]
summary: ""
slug: 
draft: true
---

### 8.2 夜间模式
有两个按钮需要实现夜间模式，一个是桌面端菜单的小太阳图标，一个是移动端菜单的小太阳图标。因为它们有不同的class name，所以我们给它们添加相同的id：`theme-toggle`（之后可以试着切换夜间模式后，小太阳图标换成月亮图标。）
为了突出重点，示例省略了其他代码
```html
    <header class="header container">
      <nav>
        <ul class="header__menu">
          ...
          <li>
            <button id="theme-toggle" class="header__sun"><svg>...</svg></button>
          </li>
        </ul>
      </nav>
    </header>

    <!-- Mobile Navigation -->
    <div class="mobile-nav">
      <nav>
        <ul class="mobile-nav__menu">
          ...
          <li>
            <button id="theme-toggle" class="mobile-nav__sun"><svg>...</svg></button>
          </li>
        </ul>
      </nav>
    </div>
    <!-- End of Mobile Navigation -->
```
到`style.css`中选中所有颜色变量，并添加`.light-mode`粘贴选中的颜色变量
```css
.light-mode {
  --clr-dark: #070a13;
  --clr-light: #f1f5f9;
  --clr-slate400: #94a3b8;
  --clr-slate600: #475569;
  --clr-slate800: #1e293b;
  --clr-rose: #e11d48;
  --clr-indigo: #4f46e5;
}
```
基本思路是将暗色变量的值换成浅色，把浅色变量的值换成暗色
```css
.light-mode {
  --clr-light: #070a13;
  --clr-dark: #f1f5f9;
  --clr-slate400: #1e293b;
  --clr-slate600: #1e293b;
  --clr-slate800: #1e293b;
}
```
这样做有一个问题，我们在按钮样式`.btn`的定义中
```css
.btn {
  background-color: var(--clr-rose);
  color: var(--clr-light);
}
```
当我们将浅色的值换成暗色，按钮文本的颜色变得很奇怪，这时只需要将`color`的值改成固定值就好了。
```css
.btn {
  background-color: var(--clr-rose);
  color: #f1f5f9;
}
```

在src中的utils文件夹中创建`dark-mode.js`。常见箭头函数`darkMode`，并导入`main.js`
```javascript
const darkMode = () => {
  const themeToggleBtns = document.querySelectorAll("#theme-toggle");

  themeToggleBtns.forEach((btn) => 
    btn.addEventListener('click', () => {
      document.body.classList.toggle('light-mode'); /*  */
      if(document.body.classList.contains('light-mode')) {
        localStorage.setItem('theme', 'light-mode');
      }
      else{
        localStorage.removeItem('theme');
        document.body.removeAttribute('class');
      }
    })
  );
};

export default darkMode;
```

We are almost done，现在我们希望如果用户已经设定了浅色模式，当用户刷新时，网页仍然显示浅色模式。这需要`localStorage`来储存
