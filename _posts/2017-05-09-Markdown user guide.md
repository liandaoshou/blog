---
layout: post
title:  "md的常用语法"
date:   2017-05-09 10:08:00 +0800
categories: md markdown
tag: Java
---

下面列举了一些常用的方法
链接

 [淘宝网](http://www.taobao.com/)
 
图片

 ![图片标题](http://shuju.taobao.ali.com/images/web/tsj_main_dirc_img.png)

标题
 # 一级标题
 ## 二级标题
 ### 三级标题
 #### 四级标题
 ##### 五级标题
 ###### 六级标题
 
tips：几个 # 就是几级标题，最小到六级

斜体

 *这是斜体*
 
 *[这是斜体链接](http://www.taobao.com)*
 
 *斜体,[这是斜体链接](http://www.taobao.com)*
 
tips：斜体和链接可以混用

为字体加颜色 <br>
 这是<label style="color:red">红色</label>字体<br>
 这是<label style="color:green">绿色</label>字体<br>
 这是<label style="color:yellow">黄色</label>字体<br>
 这是<label style="color:blue">蓝色</label>字体<br>
<label style="color:red">tips:修改color为对应的颜色英文字母即可，复杂的颜色不要想了，况且大家也用不到</label>

为自体加粗<br>

 **加粗**字体
 
Email
Email:<test@test.com><br>
 
无序排列
 * list1
 * list2
 * list3
 
有序排列
 1. list1
 2. list2
 3. list3
 
分割线
```
***

---

- - - -
```
tips: 三种都一样

内容框

在上一行内容缩进的基础上再缩进四个空格

换行

需要换行<br>这是换行后的下一行

中划线

~~中划线~~

添加脚注

这是脚注[^1]

[^1]: 这是脚注说明，会在文章的末尾显示. <br/>

表格
默认表格：

First Header | Second Header | Third Header
------------ | ------------- | ------------
Content Cell | Content Cell  | Content Cell
Content Cell | Content Cell  | Content Cell

左右浮动表格：

First Header | Second Header | Third Header
:----------- | :-----------: | -----------:
Left         | Center        | Right
Left         | Center        | Right

tips:默认向左对齐

内容块

> 这里的内容在内容块中
