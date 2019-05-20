---
title: HackerLaws
date: 2019-05-20 17:40:53
categories: Hacker-Laws
tags:
- hacker laws
- laws
---


# 内容来源

## [GitHUb - hacker-laws](https://github.com/dwmkerr/hacker-laws)

## [GitHUb - hacker-laws-zh](https://github.com/nusr/hacker-laws-zh)

# 介绍

当人们谈论开发时，会聊到许多定律。 这个仓库收录了一些最常见的定律。

❗: 这个仓库包含对一些定律、原则以及模式的解释，但不提倡其中任何一个。它们的应用始终存在着争论，并且很大程度上取决于你正在做什么。

# 定律

## 阿姆达尔定律 (Amdahl's Law)

+ [英文维基百科](https://en.wikipedia.org/wiki/Amdahl%27s_law)
+ [中文维基百科](https://zh.wikipedia.org/wiki/%E9%98%BF%E5%A7%86%E8%BE%BE%E5%B0%94%E5%AE%9A%E5%BE%8B)

> 阿姆达尔定律是一个显示计算任务潜在加速能力的公式。这种能力可以通过增加系统资源来实现，通常用于并行计算中。它可以预测增加处理器数量的实际好处，然而增加处理器数量会受到程序并行性的限制。

举例说明：如果程序由两部分组成，部分 A 必须由单个处理器执行，部分 B 可以并行运行。那么向执行程序的系统添加多个处理器只能获得有限的好处。它可以极大地提升部分 B 的运行速度，但部分 A 的运行速度将保持不变。

下图展示了运行速度的潜能：

![gcheap](/img/hacker-laws/amdahls_law.png)

(图片来源: By Daniels220 at English Wikipedia, Creative Commons Attribution-Share Alike 3.0 Unported, https://en.wikipedia.org/wiki/File:AmdahlsLaw.svg)

可以看出，50％ 并行化的程序仅仅受益于 10 个处理单元，而 95％ 并行化的程序可以通过超过一千个处理单元显著提升速度。

随着摩尔定律减慢，单个处理器的速度增加缓慢，并行化是提高性能的关键。图形编程是一个极好的例子，现代着色器可以并行渲染单个像素或片段。这也是为什么现代显卡通常具有数千个处理核心（GPU 或着色器单元）的原因。

参见：

+ [布鲁克斯法则](#布鲁克斯法则-Brooks's-Law)
+ [摩尔定律](#github---hacker-laws-zhhttpsgithubcomnusrhacker-laws-zh)

## 布鲁克斯法则 (Brooks's Law)

+ [英文维基百科](https://en.m.wikipedia.org/wiki/Brooks%27s_law)

> 软件开发后期，添加人力只会使项目开发得更慢。

这个定律表明，在许多情况下，试图通过增加人力来加速延期项目的交付，将会使项目交付得更晚。布鲁克斯也明白，这是一种过度简化。但一般的推理是，新资源的增加时间和通信开销，会使开发速度减慢。而且，许多任务是不可分的，比如更多的资源容易分配，这也意味着潜在的速度增加也更低。

谚语 **九个女人不能在一个月内生一个孩子** 与布鲁克斯法则同出一辙，特别是某些不可分割或者并行的工作。

这是[《人月神话》](#)的中心主题。

参见：

+ Death March
+ 《人月神话》

## 康威定律 (Conway's Law)

+ [英文维基百科](https://en.wikipedia.org/wiki/Conway%27s_law)
+ [中文维基百科](https://zh.wikipedia.org/wiki/%E5%BA%B7%E5%A8%81%E5%AE%9A%E5%BE%8B)

系统的技术边界受制于组织的结构。改进组织时，通常会提到它。康威定律表明，如果一个组织被分散成许多小而无联系的单元，那么它开发的软件也是小而分散的。如果一个组织更多地垂直建立在特性或其服务周围，那么软件系统也会反映这一点。

参见：

+ [The Spotify Model](#)

## 侯世达定律 (Hofstadter's Law)

+ [英文维基百科](https://en.wikipedia.org/wiki/Hofstadter%27s_law)
+ [中文维基百科](https://zh.wikipedia.org/wiki/%E4%BE%AF%E4%B8%96%E8%BE%BE%E5%AE%9A%E5%BE%8B)

> 做事所花费的时间总是比你预期的要长，即使你的预期中考虑了侯世达定律。

在估计需要多长时间开发时，你可能会听到此定律。软件开发似乎不言而喻，我们往往不能准确地估计需要多长时间才能完成。

语出《哥德尔、艾舍尔、巴赫：集异璧之大成》。

https://www.zhihu.com/question/19554287