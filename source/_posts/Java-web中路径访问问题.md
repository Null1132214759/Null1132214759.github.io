---
title: Java web中路径访问问题
date: 2018-05-13 15:58:04
tags: [Java web]
---

### Java web中Servlet、jsp、html互相访问的路径问题

  在java web学习过程中经常出现 404 not found这种找不到网页的错误，究其原因，还是访问路径不正确。

  在web项目中，访问路径主要分为两类：

1. 绝对路径
2. 相对路径

在写过如此多的demo之后，为防止意外，我个人还是建议使用绝对路径。

一般URL格式都是 http://localhost:8080/myapp/***

`String path = request.getContextPath();` 获取到的就是 /myapp

可以将其放入到request域中，然后在页面请求中添加

~~~
request.setAttribute("APP_PATH",path);
~~~

调用时直接用EL表达式取出值：${APP_PATH}