# CSS（层叠样式表）  
<hr> 

## CSS概述  

### HTML缺陷  
* <font face = "楷体" size = "4">不能够适应多种设备</font>
* <font face = "楷体" size = "4">要求浏览器必须智能化足够庞大</font>
* <font face = "楷体" size = "4" color = "0000FF">数据和显示没有分开</font>
* <font face = "楷体" size = "4">功能不够强大</font>

### CSS优点  
* <font face = "楷体" size = "4">使数据和显示分开</font>  
* <font face = "楷体" size = "4">降低网络流量</font>
* <font face = "楷体" size = "4">使整个网站视觉效果一致</font>
* <font face = "楷体" size = "4">使开发效率提高</font>  
<hr>

## CSS语法   

	<head>
    	<meta charset="UTF-8">
    	<title>CSS</title>
    	<style type="text/css">
        	p {
        	    font-weight: bold;
        	    font-style: italic;
        	}
    	</style>
	</head>
	<body>
	<p>你好</p>
	<p>你好</p>
	<p>你好</p>
	</body>  

* p称为<b>选择器</b>，后面必须跟着大括号。
* 里面为键值对；属性和冒号间不要打空格，有时会报bug。  
![](http://i.imgur.com/Sjk0omA.jpg)
<hr>  
 
## CSS和HTML结合方式  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    	<meta charset="UTF-8">
    	<link rel="stylesheet" type="text/css" href="a.css">
    	<title>CSS</title>
    	<style type="text/css">
    	    /*
    	        CSS和HTML的结合方式：
    	            1.行集样式表：采用style属性完成；可以写在开始标签里：如：你好3；
    	            2.内部样式表：采用style标签完成；在style里写的都是CSS代码；
    	            3.外部样式表：采用外部css文件完成
    	     */
    	    p {
    	        font-weight: bold;
    	        font-style: italic;
    	    }
    	</style>
	</head>
	<body>
	<p>你好</p>
	<p>你好</p>
	<p style = "color:red">你好3</p>
	</body>
	</html>  
![](http://i.imgur.com/KuLrvte.jpg)
![](http://i.imgur.com/90rLXra.jpg)   

<hr>   

## CSS的基本选择器  

	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <link rel="stylesheet" type="text/css" href="a.css">
    <title>选择器</title>
    <style type="text/css">
        /*
            选择器：
                1.基本选择器
                        a.标签选择器：就是选择了页面上一类标签
                        b.类选择器：规定用圆点.来定义,比标签选择器方便
                        c.ID选择器：规定用#来定义：针对特定的一个标签使用
                        d.通用选择器：用*来定义
         */
        div {
            border: 1px solid red;
        }

        .one{
            border: 1px solid red;
        }

        #two{
            border: 3px dashed green;
        }

        *{
            padding: 0px;
            margin: 0px;
        }
    </style>
	</head>
	<body>
	<div>你好</div>
	<div class="one">你好</div>
	<p class="one">你好</p>
	<h1 class="one">nihao</h1>
	<h2 id="two">你好</h2><!id 是唯一 不能相同>
	</body>
	</html>

内部样式表一般写在head中  

* <font face = "楷体" size = "4">基本选择器</font>
	* 标签选择器：选择了页面上一类标签
	* 类选择器：规定用圆点.来定义
	* ID选择器：规定用#来定义：针对特定的一个标签使用
	* 通用选择器：用*来定义  

![](http://i.imgur.com/HM2dcpf.jpg)  

## CSS的扩展选择器  
	<head>
    	<meta charset="UTF-8">
    	<link rel="stylesheet" type="text/css" href="a.css">
    	<title>选择器</title>
    	<style type="text/css">
    	    /*
    	        选择器：
    	            2.扩展选择器
    	                    a.组合选择器：用逗号隔开多个选择器
    	     */
    	    div, p, h1, .one, #two {
    	        border: 5px double blue;
    	    }
    	</style>
	</head>
	<body>
	<div>你好</div>
	<p>你好</p>
	<h1>nihao</h1>
	<h4 class="one">nihao</h4>
	</body>  
  
![](http://i.imgur.com/NGk8U2G.jpg)  
  
## 关联选择器  

	<head>
    	<meta charset="UTF-8">
    	<link rel="stylesheet" type="text/css" href="a.css">
    	<title>扩展选择器</title>
    	<style type="text/css">
    	    /*
        	    选择器：
        	        2.扩展选择器
        	                a.组合选择器：用逗号隔开多个选择器
        	                b.关联选择器（后代选择器）：用空格隔开
        	 */
        	h3 b i {
        	    color: red;
        	}
    	</style>
	</head>
	<body>
	<h3>西南<b>科技<i>大学</i>>计算机</b>>学院</h3><br>
	<i>大学</i>
	</body>  
  
## 伪类选择器  
	<head>
    	<meta charset="UTF-8">
    	<link rel="stylesheet" type="text/css" href="a.css">
    	<title>扩展选择器</title>
    	<style type="text/css">
    	    /*
    	        选择器：
    	            2.扩展选择器
    	                    a.组合选择器：用逗号隔开多个选择器
    	                    b.关联选择器（后代选择器）：用空格隔开
    	                    c.伪类选择器
    	                        1）：静态伪类：    ：link（点击前）, :visited（点击后）,   只能用于超链接
    	                        2）：适用于各种标签
    	                                ：onfocus 控件获得焦点
    	                                ：active  点击控件的时候
    	                                ：hover   当鼠标移动到某个控件上方的时候
    	     */
    	    div, p, h1, .one, #two {
    	        border: 5px double blue;
    	    }
	
    	    h3 b i {
    	        color: red;
    	    }
	
    	    a:link {
    	        color: red;
    	    }
	
    	    a:visited {
    	        color: yellow;
    	    }
	
    	    input：focus {
    	        border: 1px solid red;
    	        color: green;
    	        background-color: aqua;
    	    }
	
    	    p:active {
    	        color: blue;
    	    }
	
    	    label:horizontal {
    	        cursor: hand;
    	    }
    	</style>
	</head>
	<body>
	<div>你好</div>
	<p>你好</p>
	<h1>nihao</h1>
	<h4 class="one">nihao</h4>
	<h3>西南<b>科技<i>大学</i>>计算机</b>>学院</h3><br>
	<i>大学</i><br>
	<a href="http://www.baidu.com">搜猫s</a><br>
	<input type="text" name=""><br>
	<labe1>北京，你好</labe1>
	</body>  
