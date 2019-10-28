---
layout: post
title: Chisel教程 3.1：生成器-参数
date: 2019-10-25 15:36:15
category: "学习"
author: "chiselchina"
tags:
- Chisel学习
- Chisel Bootcamp
thumbnail: /asset/img/generator_parameters.jpg
lede: "要使Chisel模块成为代码生成器，必须有一些东西可以告诉生成器应该如何处理它的工作。 在本节中，我们将讨论模块的参数化，参数化的各种方法以及Scala语言特性。 能够靠参数传递实现的丰富程度与其生成的电路的丰富程度直接相关。 参数应提供有用的默认值，易于设置，并防止非法或无意义的值。 对于更复杂的系统，如果它们可以在局部被覆盖（override），而不会无意中影响其他模块中的使用，则非常有用。"
featured: true
---

<div>
<script src="/metronic/assets/plugins/jquery.min.js"></script>
{% asset_jupyter python 3.1_parameters.ipynb %}
</div>

> 本系列教程的英文版来自于[Chisel Bootcamp](https://github.com/freechipsproject/chisel-bootcamp)。

> 注意：本文不支持微软的Edge浏览器，请使用Chrome或者Safari，谢谢！
