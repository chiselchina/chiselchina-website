---
layout: post
title: BOOM项目介绍
date: 2019-06-11 15:29:01
category: "项目"
author: "chiselchina"
tags:
- 项目
thumbnail: http://iph.href.lu/400x300?text=BOOM&bg=EEEEEE
lede: "BOOM是伯克利乱序执行机器（Berkeley Out-of-Order Machine）的缩写，采用Chisel硬件构造语言编写，是一款开源的，可综合，参数化的RV64GC RISC-V核心（core）的实现。"
featured: true
---


BOOM是伯克利乱序执行机器（Berkeley Out-of-Order Machine）的缩写，采用Chisel硬件构造语言编写，是一款开源的，可综合，参数化的RV64GC RISC-V核心（core）的实现。


Github上的位置在：[https://github.com/riscv-boom/riscv-boom](https://github.com/riscv-boom/riscv-boom)。一般通过[boom-template](https://github.com/riscv-boom/boom-template)来编译和生成SoC。

<div class="small text-center">
{% img /asset/img/boom-pipeline.svg %}

默认参数的BOOM流水线 (图片来自[BOOM文档](https://docs.boom-core.org/en/latest/sections/intro-overview/boom-pipeline.html))
</div>

BOOM是一个超标量，乱序执行的核心，具有当代CPU的大部分特征。建构在Rocket Chip SoC之上，大约有1万6千行Chisel代码。可以用来学习现代CPU设计，研究安全问题，甚至可以拿来tape out芯片。目前还是一个活跃的项目，并在持续更新之中。

微架构文档的位置：https://docs.boom-core.org/en/latest/

从概念上讲，BOOM流水线分为10个阶段：指令读取（Fetch），指令解码（Decode），寄存器重命名（Register Rename），调度（Dispatch），发射（Issue），读取寄存器（Register Read），执行（Execute），内存操作（Memory），写回（Writeback）和提交（Commit）。但是，许多这些阶段在当前的实现中可以合并起来，实际上是七个阶段。

<div class="small text-center">
{% img /asset/img/boom-tile.jpg %}

BOOM复用了Rocket Chip的SoC
</div>

如上图所示，BOOM将Rocket Chip SoC当做模块库来使用，并且提供了BOOM tile来替换了原来的Rocket Tile。
