---
title: Java程序员修炼之道总结
date: 2018-06-09 21:47:10
tags: [Java]
---

# Javac程序员修炼之道 总结

  “Java程序员修炼之道”，一次偶然看到了这本书，再一看原来还是图灵系列

此书表皮是这么写的：

***

“涵盖Java 7最新特性”

"全面解读Groovy、Scala和Clojure在JVM上的应用"

”透视函数式编程的的优势“

***

#### 大体粗略的读了一下之后还是决定总结一下书中的内容



## 此书共分为四部分

### 第一部分    用 Java7 做开发

#### 第一章 初识 Java7

1. 语言与平台

   分析讲解了何为 ”Java语言“，何为”Java平台“

    .java------>javac 编译后的.class------>类加载器转换后的.class----->解释器解释为“可执行代码”------> JIT编译器编译为机器码

2.  Coin项目

   为Java7 引入了6个新特性

   - switch语句中的String
   - 更强的数值文本表示法
   - 改善后的异常处理
   - TWR
   - 钻石语法
   - 简化变参方法调用

####第二章 新IO    NIO.2 

1. 文件IO的基石——Path

   Path通常代表文件系统中的位置，在NIO.2 中的Path是一个抽象构造

   主要讲解如何创建Path、从Path中获取信息、移除冗余项、转换Path、以及与原File类

2. 处理目录和目录树

   - 如何在目录树中查找文件
   - 遍历目录树

3. NIO.2的文件系统I/O

   - 创建和删除文件
   - 文件的复制移动
   - 文件的属性
   - 快速读写数据
   - 文件修改通知
   - SeekableByteChannel

4. 异步I/O操作

   - 将来式
   - 回调试

5. Scoket和Channel 的整合

   - NetworkChannel
   - MulticastChannel



### 第二部分 关键技术

#### 第3章 依赖注入

1. 理解IoC和DI

   IoC 控制反转，DI 依赖注入，虽然日常人们不加以区分，但还是有区别的

   IoC是指一种机制，使用这种机制的用力很多，实现方式也很多。而DI只是其中一种具体用例的具体实现方式。 比较流行的IoC容器有Spring、Guice、PiocContainer。

2. Java 中标准化的DI

   - @Inject 注解   可注解 构造器、方法、属性
   - @Qualifier 注解
   - @Named 注解
   - @Scope 注解
   - @Singleton 注解  注入一个不会改变的对象时使用
   - 接口 Provider<T>

3. Java 中的DI参考实现：Guice3

​    

#### 第4章 现代并发

​    其实关于并发，简单的一张确实是讲不出太多东西的，还需继续研读 “图解Java多线程设计模式”







