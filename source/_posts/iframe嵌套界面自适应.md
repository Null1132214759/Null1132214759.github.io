---
title: iframe嵌套界面自适应
date: 2018-05-17 20:41:20
tags: [前端]
---

## iframe嵌套界面自适应

###  前言

  在web开发过程中，遇到页面嵌套页面的时候，第一首先想的的当然是iframe这个玩意，虽然很不推荐用这玩意（也是由很多坑的），但是在某些特定情况下用起来还是非常方便的。

  ### 问题

  日常我们习惯去这样用：`<iframe scrolling="no" frameborder="0" id="main_frame"></iframe>`，在确定页面大小的情况下(数据分页显示)这样是没什么问题的，隐藏iframe滚动条。但是在某些页面内容不确定情况下，隐藏其滚动条后会导致页面高度定死，页面下面数据显示不全问题。

### 解决

  ~~~
    <script>  
      // 计算页面的实际高度，iframe自适应会用到  
      function calcPageHeight(doc) {  
          var cHeight = Math.max(doc.body.clientHeight, doc.documentElement.clientHeight)  
          var sHeight = Math.max(doc.body.scrollHeight, doc.documentElement.scrollHeight)  
          var height  = Math.max(cHeight, sHeight)  
          return height  
      }  
      //根据ID获取iframe对象  
      var ifr = document.getElementById('main_frame')  
      ifr.onload = function() {  
          //解决打开高度太高的页面后再打开高度较小页面滚动条不收缩  
          ifr.style.height='0px';  
          var iDoc = ifr.contentDocument || ifr.document  
          var height = calcPageHeight(iDoc)  
          if(height < 850){  
            height = 850;  
          }  
          ifr.style.height = height + 'px'  
      }  
    </script>  
    
    引用自：https://blog.csdn.net/ron03129596/article/details/68947375 
  ~~~

直接copy这段代码进parent页面分分钟搞定，使frame页面自适应，切不显示滚动条！