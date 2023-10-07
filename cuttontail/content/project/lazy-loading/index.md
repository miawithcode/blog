---
title: "如何实现图片懒加载"
date: 2023-10-07T14:56:05+08:00
lastmod: 
tags: [""]
summary: ""
slug: 
draft: true
---

### 8.3 图片懒加载

图片懒加载（lazy loading）有两种方法可以实现，较为简单的方法是在`<img>`标签中加入 Attribute：`loading="lazy"`。

```HTML
<img loding="lazy" />
```

在 Demo 中用到的是较复杂的方法。