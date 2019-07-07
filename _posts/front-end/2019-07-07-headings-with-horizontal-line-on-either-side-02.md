---
layout: post
title: 如何在HTML标题两侧添加横线（方法2）
tags: HTML CSS
categories: front-end
comments: true
last-modified: 2019-07-07 23:47:00 +0800
---
在[上一篇文章]({{ site.baseurl }}{% post_url /front-end/2019-07-06-headings-with-horizontal-line-on-either-side-01 %})中，我们使用其中一种方法实现了在HTML标题两侧添加横线的目的，并且总长度固定的。这次我们看看如何让横线的总长度随标题的长度而变化。

* TOC
{:toc}

## 目标效果
可以参考我自己的博客网站[https://victor2code.github.io/blog](https://victor2code.github.io/blog)，其中的博客文章就是采用这种方式

![title]({{ "/images/2019-07-07-title.png" | relative_url }})

## 实现代码

### html
```html
<body>
  <div class="">
    <h3>This is a title</h3>
    <p>test test test test test test test test test test test test test test test test test test</p>
  </div>
</body>
```

### css
```html
<head>
  <style media="screen">
    div{
      width: 60%;
      margin: 0 auto;
    }
    h3,p{
      text-align: center;
    }
    h3::after{
      content: "";
      border: 1px grey solid;
      width: 30px;
      display: inline-block;
      position: relative;
      top: -5px;
      left: 20px;
    }
    h3::before{
      content: "";
      border: 1px grey solid;
      width: 30px;
      display: inline-block;
      position: relative;
      top: -5px;
      left: -20px;
    }
  </style>
</head>
```

## 实现效果
看效果和方法1的效果没有区别。不过在标题的宽度变化的时候，标题的左右两侧的横线一直维持在30px的宽度。

## 代码分析
方法1中是在HTML中新添加了一个元素并利用其边框做为横线，这里并没有在HTML中添加新的元素，而是利用了`:before`和`:after`选择器在标题的前后分别插入了一些空内容，然后利用它们的边框做为横线

* `::after`和`:after`都可以达到目的，但是为了兼容性，推荐使用两个冒号。`::before`也是同理

* `width: 30px;`将每段横线的宽度固定住了，但是使用宽度的前提是`display: inline-block`，因为默认情况下插入的内容是`display: inline;`的，不可以调节宽度和位置

* 这里没有`z-index: -1;`的必要，因为横线和标题的文字没有重叠的部分


## 总结
这种方式比起方式1更容易理解，实现起来也更容易，我个人也觉得更美观，所以在自己的博客中采用了本方法。

欢迎在下面留言进行讨论和交流。
