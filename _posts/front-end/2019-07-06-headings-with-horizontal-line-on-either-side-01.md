---
layout: post
title: 如何在HTML标题两侧添加横线（方法1）
tags: HTML CSS
categories: front-end
comments: true
last-modified: 2019-07-06 21:47:00 +0800
---
网页文章的标题元素，也就是`<h1>`一直到`<h6>`，对于一篇网页文章的重要性是不言而喻的。它们在视觉上对网页进行了分段，配合上文章的导航标签(Table of Content)可以让读者整体上对文章有个清晰的结构认知。通过在标题两侧添加横线，可以将这种网页分段进一步加深，这篇文章我们就来看看如何去实现。

* TOC
{:toc}

## 目标效果
可以参照一个我很喜欢的网站[Interneting Is Hard](https://internetingishard.com/)，例如其中一个段落

![Interneting Is Hard]({{ "/images/2019-07-06-title-demo.png" | relative_url }})

## 实现代码

### html
```html
<body>
  <main>
    <h2>This is a title</h2>
    <span></span>
    <p>bluh bluh bluh bluh bluh bluh bluh bluh bluh bluh bluh bluh bluh bluh bluh bluh bluh bluh bluh bluh bluh bluh bluh bluh bluh</p>
  </main>
</body>
```

### css
```
<head>
  <style media="screen">
    main{
      width: 60%;
      margin: 0 auto;
    }
    h2,p{
      text-align: center;
    }
    h2{
      background-color: white;
      width: 30%;
      margin: 0 auto;
    }
    span{
      margin: 0 auto;
      display: block;
      border: 1px black solid;
      width: 80%;
      position: relative;
      top: -15px;
      z-index: -1;
    }
  </style>
</head>
```
## 实现效果
![title final]({{ "/images/2019-07-06-title-final.png" | relative_url }})

## 代码分析
这里实现的效果是不管你的标题多长，横线的总长度都是固定的
* 横线就是标题下面添加的那个`<span>`标签，当然用`<div>`也是可以，如果是用`<div>`那么这里的`display: block;`就可以省略了

* `<span>`标签的长度是固定的，为`<main>`元素的80%，而`<main>`本身也只有整个屏幕的60%

* `position: relative;`让我们能在不影响上下元素的情况下移动这个横线，例如这里的`top: -15px;`，具体移动的距离根据自己情况去判定。如果是要居中，需要用`margin: 0 auto;`

* `<h2>`的背景色我设置为白色，具体设置什么颜色需要和你`<main>`的背景色一致

* `z-index:-1;`是将横线往下移，只有设置了position的元素才可以使用，数字越大越往上。具体的图层移动也是需要自己去灵活把握

## 总结
这次我们一起探索了如何给标题添加长度固定的横线，下次我们来看看如何让横线随着标题的长度去跟随变化，就好像我的这篇文章一样。欢迎在下面留言进行讨论和交流。
