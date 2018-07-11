---
title: 关于ajax异步请求的使用
date: 2018-05-15 17:00:55
tags: [Java web,前端]
---

## 关于java web开发中ajax一部请求使用的注意事项   

  在web开发当中，原生的ajax异步使用还是较少的，因为jQuery为我们提供了更好的封装：`jQuery.ajax(url,[settings])`。

通过http请求加载远程数据，可以使浏览器在不刷新页面的情况下来进行局部页面数据的改变，所以ajax还是很有那必要了解并学习一下的。

  jQuery 底层 AJAX 实现。简单易用的高层实现见 `$.get, $.post` 等。`$.ajax()` 返回其创建的 XMLHttpRequest 对象。大多数情况下你无需直接操作该函数，除非你需要操作不常用的选项，以获得更多的灵活性。 

#### ajax回调函数

  如果要处理$.ajax()得到的数据，则需要使用回调函数。beforeSend、error、dataFilter、success、complete。  而一般日常使用的是处理成功后返回的信息，主要还是使用success

#### 数据类型

  可以处理的主要数据类型有xml、html、就送、jsonp、script、text，通过dataType选项还指定不同数据处理方式 。其中，text和xml类型返回的数据不会经过处理。数据仅仅简单的将XMLHttpRequest的responseText或responseHTML属性传递给success回调函数。

### 发送数据到服务器

  默认情况下，Ajax请求使用GET方法。如果要使用POST方法，可以设定type参数值。 

#### 实例

1. 加载并执行一个js文件

   ~~~
   $.ajax({
     type: "GET",
     url: "test.js",
     dataType: "script"
   });
   ~~~

   2. 保存数据到服务器，成功时显示信息

      ~~~
      $.ajax({
         type: "POST",
         url: "some.php",
         data: "name=John&location=Boston",
         success: function(msg){
           alert( "Data Saved: " + msg );
         }
      });
      ~~~

      3. 装入一个html网页最新版

         ~~~
         $.ajax({
           url: "test.html",
           cache: false,
           success: function(html){
             $("#results").append(html);
           }
         });
         ~~~

  #### 拿json来说

- 而后台处理请求时，若使用的是SSM，只需添加jackson jar包，在Controller上添加@Responsebody，这样就会自动将返回数据封装为json对象，并在前端success函数中进行解析。
- 若是使用原生servlet处理请求，为更好的对数据进行封装，须引入json相关的jar包，将数据封装为JSONObject对象或JSONArray对象，设置response.setCharacterEncoding("utf-8")，调用 response.getWriter().write(jsonObject.toString())将数据返回到前端，后在success中进行解析。

#### 高层方法

[$.get(url,[data\],[fn],[type])](http://jquery.cuishifeng.cn/jQuery.get.html) 

[$.getJSON(url,[data\],[fn])](http://jquery.cuishifeng.cn/jQuery.getJSON.html) 

[$.post(url,[data\],[fn],[type])](http://jquery.cuishifeng.cn/jQuery.post.html) 