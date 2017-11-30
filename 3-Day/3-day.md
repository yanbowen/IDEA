# JavaScript  

<hr>

## 概述  
* 一种基于对象和事件驱动的脚本语言（脚本语言是嵌入在其他语言中的寄生语言）  
* 作用：给页面添加动态效果  
<hr>

## 特点  
* 弱势语言 
* 由浏览器直接执行。（函数需要调用）  
* 交互性
* 安全性（沙箱）
* 跨平台性（跨浏览器） 

### JavaScript与Java的区别：  
* JavaScript是一个解释性语言，Java是编译解释性语言
* JavaScript是一个弱势语言，Java是强势语言
* `在页面上引入的方式不同JavaScript是<Script>引入，Java代码<%>`
* 
* JavaScript是基于对象，Java是面向对象  

## JavaScript语言组成  
* ECMAScript + BOM + DOM
* BOM : Browser object Model 浏览器对象模型
* DOM : Document object Model 文档对象模型  


<hr>

## JavaScript与HTML结合方式  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    	<meta charset="UTF-8">
    	<title>JavaScript与HTML结合方式</title>
    	<script type="text/javascript" src="a.js"></script>
    	<script type="text/javascript">
    	    <!--
    	    alert("12345");
    	    //-->
    	</script>
	</head>
	<body>
	<p onclick="alert(`你好`)">大家好</p>
	</body>
	</html>  

* 采用事件来调用，代码写在字符串中
	* `<p onclick="alert(`你好`)">大家好</p>`
* 采用定义函数的方式:用function来定义函数
* 采用外部js文件
	* 利用`<script type="text/javascript" src="a.js"></script>` 

<hr>

## JavaScript基本语法  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>JavaScript基本语法</title>
    <script type="text/javascript">
        <!--
        /*
            JavaScript中的数据类型：
                a.基本类型
                    1.undefined：没有给变量赋值时的类型
                    2.String
                    3.Boolean
                    4.Number
                    5.function
                    6.null
                b.引用类型
                    object
            判断变量的类型有两种方式：
                    1.采用typeof()：打印的是所有类型的toString方法（所有类型的小写）
                    2.采用instanceof关键字判断：是判断变量是不是由某种类型new出来的
         */
        var a = 10;
        alert(typeof(a));
        alert(a instanceof Number);
        var b = new Number(10);
        alert(b instanceof Number);
        alert(typeof (b) == "number")
        //-->
    </script>
	</head>
	<body>
	<p onclick="alert(`你好`)">大家好</p>
	</body>
	</html>  

<hr>

## JavaScript运算符  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>JavaScript运算符</title>
    <script type="text/javascript">
        <!--
        /*
            1. == 判断的是内容， === （全等号）判断的是内容及类型
         */

        alert(3.6 & 0.8);
        a = "100";
        b = 100;
        alert(a == b);
        //-->
    </script>
	</head>
	<body>
	<p onclick="alert(`你好`)">大家好</p>
	</body>
	</html>  

<hr>

## JavaScript类型转换  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>JavaScript类型转换</title>
    <script type="text/javascript">
        <!--
        /*
            1.把字符串转换为number类型
                a.parseInt.parseFloat
                b.(推荐) * 1
            2.把字符串转换为boolean
                牢记：非零为真，0  null 为假
         */
        var a = "123";
        a = a * 1;
        alert(typeof (a));

        var b = "123";
        if (b)
            alert("true");
        else
            alert("false");

        //-->

        function fun() {
            //拿到文本框对象
            var txt = document.getElementById("age").value;
            //判断内容
            if (txt == 100)
                alert("年龄100")
            else
                alert("年龄不是100")

        }
    </script>
	</head>
	<body>
	年龄：<input type="text" name="" id="age">
	<input type="button" value="弹出年龄" onclick="fun()">
	</body>
	</html>  

