---
layout: post
title: Rocket Chip介绍
date: 2019-06-10 15:48:28
category: "项目"
author: "chiselchina"
tags:
- 项目
thumbnail: /asset/img/rocket-chip-top_800x600.jpg
lede: "Rocket Chip是基于Chisel开发的一款开源SoC生成器（Generator），它包含了由core，cache以及互连（interconnect）等构成的模块库，以此为基础构成一个完整的SoC，并可以生成可综合的RTL代码。"
featured: true
---

Rocket Chip是基于Chisel开发的一款开源SoC生成器（Generator，生成器的概念请参考本站对于Chisel的介绍），它包含了由core，cache以及互连（interconnect）等构成的模块库，以此为基础构成一个完整的SoC，并可以生成可综合的RTL代码。

该项目可以追溯到2011年，来自于RISC-V和Chisel的两个项目结合，至今为止已经成功的tape out过十几次。

Github上的repo可以在这里找到：https://github.com/freechipsproject/rocket-chip

<div class="small text-center">

![](/asset/img/rocket-chip-top_800x600.jpg)

Rocket Chip生成器包含: A) Core生成器 B) Cache缓存生成器 
C) RoCC协处理器生成器 D) Tile块生成器 E) TileLink生成器 F) 外设

图片来自[Rocket Chip Tech Report](http://www2.eecs.berkeley.edu/Pubs/TechRpts/2016/EECS-2016-17.pdf)
</div>

Rocket Chip有两个主要的用途：

第一个是它可以用来生成RISC-V的RTL实现，该实现具有顺序执行的流水线，符合IEEE标准的浮点运算单元，多级cache，虚拟内存，以及其他相关模块。

另一个用途是把Rocket Chip当做“函数库”来使用，只复用其中的某个部分。例如伯克利的另一个项目BOOM（RISC-V的另一个乱序执行superscalar实现）就把Rocket Chip当做模块库来使用，并只需要重新实现其中的core和cache部分。


Rocket Chip包含两种类型的模块：一种是工具utility，类似helper性质，用来帮助代码实现，并不直接生成硬件；另一种是硬件模块的生成器。（这里需要理解Scala和Chisel的区别，虽然Chisel是嵌在Scala里实现的，但是只有Chisel部分可以实际生成硬件）。这些模块的实现在src目录下。

其中，工具库包括：

- config：用于描述参数的库（参数是指可以调整的一些值，进而可以生成一系列不同的硬件实现），只是为了方便调整生成器的参数。
- diplomacy：在Chisel elaboration并开始生成RTL之前，用来协商模块到共享的interconnect之间的参数。
- regmapper: 用来描述内存映射的寄存器，生成真正的寄存器实现，并连接到diplomacy总线上。
- system: 可以理解为一个跑在JVM上的Scala应用，从而FIRRTL在上面可以跑起来并生成RTL代码。
- unittest: 可综合的单元测试代码的框架。注意，这与Chisel的tester框架完全不同。
- util: 文件系统的输入输出，例如在生成某个设计的时候将一些metadata输出到文件。

模块库（生成器）包括：

- amba：AMBA总线的diplomacy实现。
- devices：内存映射的外设实现，例如RAM，ROM等。
- groundtest：用于内存系统集成测试的流量生成器，可综合。
- interrupts：diplomacy实现的中断信号。
- jtag：JTAG接口的实现。
- rocket：core的流水线实现，L1指令和数据缓存，FPU，RoCC协处理器等。
- scie：用于在core流水线里面添加自定义指令的接口。
- subsystem：公共总线架构的实现，包含master和slave接口。
- tile：可以包含core流水线，FPU，L1缓存，RoCC协处理器等的容器。用来生成多核系统。
- tilelink：共享内存总线协议的实现。
- util：包含ECC，arbiter， mux，随机数生成器等。


Rocket Chip依赖的其他库有：

- chisel3 (https://github.com/ucb-bar/chisel3): 硬件生成语言
- firrtl (https://github.com/ucb-bar/firrtl): RTL的中间语言表示，进而生成Verilog代码，C代码等最终代码。
- hardfloat (https://github.com/ucb-bar/berkeley-hardfloat): Hardfloat holds Chisel code that generates parameterized IEEE 754-2008兼容的浮点数的Chisel实现，包含乘加，和整数类型以及不同精度之间的转换。
- rocket-tools (https://github.com/freechipsproject/rocket-tools): RISC-V的toolchain。已经upstream到了gcc，也可以直接通过官方的gcc获得。
- torture (https://github.com/ucb-bar/riscv-torture): 用于压力测试的随机指令生成器。

