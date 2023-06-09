<!--
 * @Author: 夏朝辉 lesslessmore@163.com
 * @Date: 2023-05-30 14:17:10
 * @LastEditors: 夏朝辉 lesslessmore@163.com
 * @LastEditTime: 2023-05-30 14:57:13
-->
# Google V8引擎

<aside>
💡 系统性学习一门技术，花费的时间也是最短的，也可以说是性价比最高的。

所谓技术栈，应该是在某一领域，从底层的基础知识到上层的应用技术有一个完整体系。

</aside>

> 当我们进入一个领域时，应该如何建立适合自己的技术栈呢？
如果你进入的是一个成熟的领域，那么一般都有比较完整的技术栈的资料，我们需要花些时间分析资料，系统性地了解这一领域知识的宏观架构、它的过往历史、它的优缺点，然后结合现有资料和我们自身的特点来建立我们自己的技术栈。
如果你所在的领域还在高速发展中，并没有人总结出完整的技术栈，那么为了更好地理解技术的发展脉络，我们需要花更多一些的时间去整理出该领域的技术栈。
>

![Untitled](/assets/web/概念体系/v8-knowledge-graph.png)

# 概念

**V8 是由 Google 开发的开源 JavaScript 引擎，也被称为虚拟机，模拟实际计算机各种功能来实现代码的编译和执行。**

我们可以简单地把 JavaScript 虚拟机理解成是一个翻译程序，将人类能够理解的编程语言 JavaScript，翻译成机器能够理解的机器语言。V8 的主要功能，就是结合 JavaScript 语言的特性和本质来编译执行它

V8关键词：即时编译（JIT）、惰性编辑、内联缓存、隐藏类

JavaScript设计思想

![Untitled](/assets/web/概念体系/v8-2-javascript-design-idea.png)

为了实现函数是一等公民的特性，JavaScript 采取了**基于对象**的策略；再比如为了实现原型继承，V8 为每个对象引入了**`__proto__`** 属性。

## V8是如何执行Js代码的

从一个高层的宏观视角来解释什么是 V8，以及 V8 又是怎么执行一段 JavaScript 代码的

### 涉及的概念和特性

- JIT
- 作用域
- 词法环境
- 执行上下文

执行代码流程

1. 编译（将js代码编译成字节码或机器码）
2. 执行

处理器只能识别机器码，任何高级语言执行时都要先经过编译。处理器处理高级语言有两种方式，分别是**解释执行**（解析器解析源码为中间代码，解释器直接执行中间代码并输出结果，不编译为二进制代码）和**编译执行**（解析器解析源码为机器码-二进制代码，编译器执行机器码并输出结果）。

对于Java和JavaScript之类的高级语言，需要有虚拟机来模拟计算机的编译执行过程，V8就是一个可以编译Js代码的虚拟机。

![Untitled](/assets/web/概念体系/v8-3.png)

![Untitled](/assets/web/概念体系/v8-4.png)

V8 作为 JavaScript 的虚拟机的一种，执行JavaScript代码时并没有采用单一的技术，而是混合编译执行和解释执行这两种手段，这种技术称为JIT（Just In Time）技术。

至于V8为什么要采用这样一种技术去执行JavaScript代码，其实是出于一种权衡策略。在启动过程中采用了解释执行的策略，但是如果某段代码的执行频率超过一个值，那么 V8 就会采用优化编译器将其编译成执行效率更加高效的机器代码。

> 原因在于二种执行方式各有利弊，解释执行启动速度快，但是执行速度慢；编译执行执行速度快，但是启动速度慢。
>

V8在启动执行JavaScript代码前，需要先准备一些基础环境，其中包括“**堆/栈空间**”、“**全局执行上下文**”、“**全局作用域**”、“**事件循环系统**”等。

V8在接收到源代码时，首先会对其进行结构化，使其变成抽象语法树（**AST**），便于V8去理解。同时在生成AST时，会生成相关的作用域，存放一些变量。

有了AST和作用域后，就可以生成**字节码**（字节码介于AST和机器代码之间，可以直接被解释器执行输出结果，也可以通过编译器编译后变成二进制的机器码，由处理器执行并输出结果）

> 在解释执行字节码的过程中，如果发现了某一段代码会被重复多次执行，那么监控机器人就会将这段代码标记为热点代码。当某段代码被标记为热点代码后，V8 就会将这段字节码丢给优化编译器，优化编译器会在后台将字节码编译为二进制代码，然后再对编译后的二进制代码执行优化操作，优化后的二进制机器代码的执行效率会得到大幅提升。如果下面再执行到这段代码时，那么 V8 会优先选择优化之后的二进制代码，这样代码的执行速度就会大幅提升。
>

### 总结

V8 是由 Google 开发的开源 JavaScript 引擎，也被称为虚拟机，模拟实际计算机各种功能来实现代码的编译和执行。

因为计算机只能识别二进制指令，所以要让计算机执行一段高级语言通常有两种手段，第一种是将高级代码转换为二进制代码，再让计算机去执行；另外一种方式是在计算机安装一个解释器，并由解释器来解释执行。

解释执行和编译执行都有各自的优缺点，解释执行启动速度快，但是执行时速度慢，而编译执行启动速度慢，但是执行速度快。为了充分地利用解释执行和编译执行的优点，规避其缺点，V8 采用了一种权衡策略，在启动过程中采用了解释执行的策略，但是如果某段代码的执行频率超过一个值，那么 V8 就会采用优化编译器将其编译成执行效率更加高效的机器代码。

V8 执行一段 JavaScript 代码所经历的主要流程：

- 初始化基础环境；
- 解析源码生成 AST 和作用域；
- 依据 AST 和作用域生成字节码；
- 解释执行字节码；
- 监听热点代码；
- 优化热点代码为二进制的机器代码；
- 反优化生成的二进制机器代码。

> JavaScript 是一门动态语言，在运行过程中，某些被优化的结构可能会被 V8 动态修改了，这会导致之前被优化的代码失效，如果某块优化之后的代码失效了，那么编译器需要执行反优化操作。
>