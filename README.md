# Go+ 开发者指南

## 概述

1年前，看到老许对[Go+](https://github.com/goplus/gop)的介绍，对Go+如何实现双引擎非常感兴趣，于是就抽出了一些业余时间参与了一些Go+的开发。语言类的开发其实跟其他项目的开发上，还是有很大的区别的。他必须有一些语言类开发的背景知识，否则在开发过程中经常会找不到正确的姿势去解决问题。我也是经过了1年多的实战，总结了一些经验，也希望通过本开发指南，能够帮助更多的人加入到Go+开发者的阵营中。

目前网上有关介绍语言开发的文章并不是很多，并且也都不够深入，基本上都是点到为止，篇幅不大，本开发指南争取系统一些，涵盖面更广一些，干货更多一些。

我们所熟知的编程语言，比如 Java，Python，Golang以及C语言，他们被称为通用编程语言(General Purpose Language，GPL) 而与通用编程语言相对的就是领域特定语言（Domain Specific Language，DSL），通用编程语言使用更广泛一些，而领域特定语言是为了解决某一类特定语言而开发出来的语言，语言偏小众一些。但无论是哪种语言，都需要经过 词法分析 -> 抽象语法树构建 -> 编译 三个步骤，对于解释性语言，编译器将会生成字节码 （ByteCode）来执行。对于编译性语言，编译器将对生成机器码（二进制）来执行。但目前大多数高级语言的编译器，都不是直接生成机器码，比如 C 编译器是将 C 代码翻译为汇编语言。汇编编译器获取这些内容编译为机器码。C# 和 Java 会翻译为字节码。字节码在虚拟机运行的时候才会被转换为机器码。Go语言也是把Go源码编译为汇编语言，然后通过汇编编译器获取这些内容编译为机器码。

本指南将会涉及一下知识点：

* [第1章 词法分析](chapter1/README.md)
* [第2章 表达式](chapter2/README.md)
* [第3章 语句](chapter3/README.md)
* [第4章 通用声明](chapter4/README.md)
* [第5章 函数声明](chapter5/README.md)
* [第6章 抽象语法树](chapter6/README.md)
* [第7章 编译器概念](chapter7/README.md)
* [第8章 中间文件](chapter8/README.md)
* [第9章 GO+ 编译器](chapter8/README.md)
* [第9章 Go 编译器](chapter9/README.md)
* [第10章 CGO 编译原理](chapter10/README.md)
* [第11章 import Python 实现](chapter11/README.md)

## 版权

版权归 Goplus开发者团队所有，未经许可，禁止转载。
