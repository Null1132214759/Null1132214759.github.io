---
title: JS表单校验实例
date: 2018-05-13 15:41:51
tags: [前端]
---

### JS表单校验实例

  表单也算是一个系统中必不可少的组建，当然，对于表单提交的数据必然的要进行一些验证。

而表单数据验证，一般来说是两道屏障。

1. 前端校验
2. 后端校验

  而前端校验主要就是通过JS或者jQuery来操作了，下面给出一些前端数据校验实例：

~~~


/*是否带有小数*/
function isDecimal(strValue ) {
var objRegExp= /^\d+\.\d+$/;
return objRegExp.test(strValue);
}

/*校验是否中文名称组成 */
function ischina(str) {
var reg=/^[\u4E00-\u9FA5]{2,4}$/; /*定义验证表达式*/
return reg.test(str); /*进行验证*/
}

/*校验是否全由8位数字组成 */
function isStudentNo(str) {
var reg=/^[0-9]{8}$/; /*定义验证表达式*/
return reg.test(str); /*进行验证*/
}

/*校验电话码格式 */
function isTelCode(str) {
var reg= /^((0\d{2,3}-\d{7,8})|(1[3584]\d{9}))$/;
return reg.test(str);
}

/*校验邮件地址是否合法 */
function IsEmail(str) {
var reg=/^([a-zA-Z0-9_-])+@([a-zA-Z0-9_-])+(\.[a-zA-Z0-9_-])+/;
return reg.test(str);
}

~~~

  所谓校验主要还是通过正则表达式来匹配一系列字符，而对于正则表达式的理解还是处于 ‘ 知道有有这么个东西 ’ 的层面，虽然也看过一些关于正则表达式使用的一些语法，但在真正使用的时候还是感觉力不从心。关于正则，有时间还是要看一下的，日常多留心去使用，学会慢慢积累！