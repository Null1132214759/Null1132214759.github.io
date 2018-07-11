---
title: 用JRebel和LiveRebel执行热部署
date: 2018-06-03 18:08:06
tags: [Java web]
---

# 用JRebel和LiveRebel执行热部署

## 前言

​    有人问：Java是解释型语言还是编译型语言？你可以毫不犹豫的告诉他：都是！Java是一种静态类型、动态编译、面向对象的语言”。

当然，这里所谓的编译可不是 .java 源文件编译为 .class 文件的过程，而是 .class 文件被JVM解释后会被即时编译（JITing）。当然，这不是今天要讨论的重点。



   由于Java是编译型语言，也就是说没次修改代码之后都必须重复下列步骤：

- 重新编译Java代码
- 停止web服务器
- 将改动过的应用重新部署到服务器
- 启动web服务器

因此浪费很多的时间，而我们首先应该想到的应该就是 “热部署”！



## [JRebel](https://zeroturnaround.com/software/jrebel/)

https://zeroturnaround.com/software/jrebel/

  JRebel处于IDE和Web服务器之间，当源代码发生变化时能自动将这些变化反映到正在运行的Web服务器上（LibeRebel用于生产环境的不熟）。这种热部署没有什么问题，并且这些工具实际上是解决热部署问题的行业标准。

### 安装IDEA JRebel插件

![图片](/img/JRebel1.png)

1.  当然是先去网站注册了，注册可以获得 14 天的免费使用，14天之后。。。。。。。

   ![图片](/img/JRebel2.png)

2.  注册完成后就来IDEA 插件仓库下载JRebel插件吧

   ![图片](/img/JRebel3.png)

3. 插件安装完成后，在IDEA导航栏的help菜单下会看到 JRebel 选项，选择后去激活插件

   ![图片](/img/JRebel4.png)

4. 插件激活后你就会看到多了两个绿色的小按钮，前面是run  后面是debug

   ![图片](/img/JRebel5.png)

5. 在IDEA窗口左侧勾选要运行的项目

6. ![图片](/img/JRebel7.png)

7. 调整一下tomcat设置

8. ![图片](/img/JRebel6.png)

9. 最后，就可以愉快的debug了！  

## 最后

  哈哈，你会发现，当你修改java代码后，他会自动热部署，再也不需要手动去restart server 了！！！