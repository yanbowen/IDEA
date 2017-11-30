# JavaScript与DOM1  

<hr>

## JavaScript函数调用的方式  
	    <script type="text/javascript">
        <!--
        /*
            函数定义：
                1.采用关键字function来定义
                2.采用匿名函数的方式（采用function作为名字）
                3.(了解)采用new Function（）
                        小括号最后一个参数是函数体，之前所有的参数都是形参

            函数的调用：
                调用函数时：是利用函数名来寻找，（定义函数的时候不要使用相同的名字）
         */

        function fun() {
            alert("大家好");
        }

        fun();

        var a = function () {
            alert("我是匿名函数");
        }
        a();

        var b = new Function("x", "y", "alert(x+y)");
        b(3, 4);

        //-----------------------------------------------------------------------
        function fun1() {
            alert("我是无参的函数");
        }

        function fun1(x) {
            alert("我是带x的参数函数");
        }

        function fun1(x, y) {
            alert("我是带两个参数的函数");
        }

        //-->
    	</script>


<hr>

## JavaScript函数的劫持  
	    <script type="text/javascript">
        <!--
        //函数劫持：改变JavaScript的函数预定好的功能
        window.alert = function (x) {//预定义的功能
            document.write(x);
        }
        alert("abc");
        //-->
    	</script>  

<hr>

## JavaScript全局函数  
	    <script type="text/javascript">
        <!--
        /*
                  NaN : NOT a number
               1. isNaN : 是不是一个数字：返回TRUE 不是数字
               2. parseInt , parsetFloat
               3. eval :
                        a.主要执行字符串。将结果转换为数字
                        b.将json格式的字符串转换为json  “json本质======键值对。map”
               4. escape();编码
               5. unescape();解码
               6. encodeURL()对网址进行编码
               7. decodeURL
         */

        var a = "100";

        //JavaScript只判断内容，不判断类型
        if (isNaN(a)) {
            alert("不是数字");
        } else {
            alert("是数字");
        }

        alert("3" + "2");
        alert(eval("3") + eval("2"));
        alert(eval("3 + 10") + eval("2"));

        var b = "中国";
        var c = escape(b);
        alert(c);
        alert(unescape(c));
        //-->
    	</script>

<hr>

## array对象  
	    <script type="text/javascript">
        <!--
        /*
            数组对象的定义方式：
                    1.采用new Array()的方式
                    2.定义[]来定义，推荐使用

            JavaScript与Java中数组的差别：
                    1.Java中数组有类型。一旦类型确定，则数组中所以的数据都是同一种类型。JavaScript中没有类型,（不推荐)
                    2.Java中数组长度一旦确定不能再更改了，JavaScript可以再次改变数组长度
                            更改方法：1.指定length属性
                                      2.指定某个数组中元素的值
                    3.Java中的数组中的数据引用必须用下标引用，下标必须是整数
                      JavaScript中数组的数据引用可以用任意对象
         */
        var arr = new Array();//定义一个数组arr,初始长度为0
        var arr1 = new Array(4);//定义一个数组arr1.初始长度是4
        arr1[0] = 1;
        arr1[1] = 10;
        alert(arr1[0]);
        alert(arr1[2]); //弹出undefined，没有初始值
        alert(arr1[100]);//弹出undefined，相当于定义了一个变量arr1[100]，没有赋值

        var arr2 = new Array(1, 2, 3, 4, 5);//定义一个数组arr2，初始化数据1,2,3,4,5
        alert(arr2[4]);

        var arr3 = [];//定义一个数组，里面空
        var arr4 = [3, 2, 4, 5];//定义一个数组，同时初始化

        //-----------------------区别----------------------------------
        var arr5 = [1, 2, "4", true, 45.8, false, "abc"];
        alert(arr5[3]);

        alert(arr5.length);
        arr5.length = 100;
        alert(arr5.length);

        arr5[101] = 100;
        alert(arr5.length);

        arr5.length = 2;
        alert(arr5[3]);//弹出undefined

        var arr6 = ["中国", "美国", "日本"];
        arr6["中国"] = ["北京", "上海", "天津"];
        alert(arr6["中国"][0]);

        //-->
    	</script>   

<hr>

## array的常用方法介绍  
	    <script type="text/javascript">
        <!--
        /*
            array对象的方法：
                    1.join()：默认情况下用逗号隔开每个数据
                    2.push()：将元素添加到数组的末尾
                    3.reverse()：反转顺序
                    4.shift()：删除并返回第一个元素
                    5.sort()：排序：默认情况下先将能转换为number类型的字符串和number类型的放一起比较（String比较String）

         */

        var arr = ["中国", "美国", "日本"];
        alert(arr.join());//默认用逗号隔开
        alert(arr.join(""));//用空字符串连接
        arr.push("韩国");
        alert(arr.join());
        arr.reverse();
        alert(arr.join());
        alert(arr.shift());

        var arr1 = [3, 4, "23", "34", 124];
        alert(arr1.sort());

        var arr2 = [3, "a", 4, "23", "bc", "34", 124, "ert"];
        alert(arr2.sort());

        alert(arr1.sort(function (a, b) {//传递一个function类型参数，制定我们的比较规则，只适用于数字类型的字符串
            if (a * 1 > b * 1)
                return 1;
            else
                return -1;
        }));

        //-->
    	</script>  

<hr>

## 标题栏的滚动  
	<head>
    <meta charset="UTF-8">
    <title>标题栏的滚动---西南科技大学</title>
    <script type="text/javascript">
        <!--
        function init() {
            //1.拿到标题栏的文本
            var title = document.title;
            //alert(title);
            //2.将文本字符串转换为数组
            var arr = title.split("");
            //3.拿到数组的第一个元素，并从数组中删除
            var first = arr.shift();
            //4.将第一个元素添加到数组的最后
            arr.push(first);
            //5.将数组再组合成一个字符串
            title = arr.join("");
            //6.将字符串再赋值回标题栏
            document.title = title;
            //7.每隔一秒，做一遍前6步
            setTimeout("init()", 1000);

        }

        //-->
    </script>
	</head>
	<body onload="init()">
	</body>  
  
<hr>

## 字符串对象  
	    <script type="text/javascript">
        <!--
        /*
            String对象的方法：
                    1.substr();//截取子字符串,两个参数，第一个是参数下标。第二个是截取的长度
                    2.substring();//截取子字符串,两个参数，代表下标
         */

        function fun() {
            //1.拿到p标签对象
            var p = document.getElementById("p");
            //2.拿到p标签对象的主体内容
            var txt = p.innerHTML;  //innerHTML必须是有开始标签和结束标签的标签对象才能使用
            //3.改变字体内容。在赋值回去
            p.innerHTML = txt.big().big();
        }

        //示例：点击变色按钮，让p标签中的文本的颜色随机变化
        var arr = ["red", "blue", "green", "yellow", "#888888"];

        function fun1() {

            //拿到p标签对象
            var p = document.getElementById("p");
            //随机取得一个整数作为数组的下标
            var index = Math.floor(Math.random() * arr.length);
            //3.给p标签对象的主体改变颜色，并赋值回去
            //var txt = p.innerHTML;
            var txt = p.innerText;
            p.innerHTML = txt.fontcolor(arr[index]);

            setTimeout("fun1()", "3000");
        }

        function fun2() {
            var txt = document.getElementById("h1").innerHTML;
            txt = document.getElementById("h1").innerText;
            alert(txt);
        }

        var s = "abcdefg";
        alert(s.substring(2, 3));
        alert(s.substring(3, 2));
        alert(s.substring(300, -2));
        alert(s.substr(2, 3));
        //-->
    </script>
	</head>
	<body>
	<p id="p">大</p>
	<input type="button" value="变大" onclick="fun()"><br>
	<p></p>
	<input type="button" value="变色" onclick="fun1()">
	
	<h1 id="h1"><font>你好</font></h1>
	<input type="button" value="演示innerH和innerText的区别" onclick="fun2()">
	</body>   
  
<hr>

## Maht对象  
	    <script type="text/javascript">
        <!--
        /*
            Maht对象：
                1.floor（）： 向下取整
                2.ceil（）：向上取整
                3.random（）：0-1之间随机数（左闭右开区间）
                4.round（）：四舍五入取整

         */
        var a = 3.1;
        alert(Math.floor(a));
        alert(Math.ceil(a));
        alert(Math.round(a));
        //-->
    	</script>  
  
<hr>

## Maht对象  
    <script type="text/javascript">
        <!--
        /*
            Date对象：
                1.拿到当前时间：new Date();
                2.拿到年月日，时分秒：getXXX();

         */
        var d = new Date();
        alert(d.toLocaleString());
        alert(d.getYear() + 1900);//从1900年开始计算
        alert(d.getMonth())
        alert(d.getDate());
        alert(d.getDay());//星期
        //-->
    </script>  

<hr>

## 正则表达式  
	    <script type="text/javascript">
        <!--
        /*
            正则表达式：

         */
        var reg = /.../;
        var s = "abcde";

        alert(reg.test(s));//测试字符串中是否包含正则表达式中所匹配的字符串，返回的是Boolean类型
        alert(reg.exec(s));//以数组的形式返回匹配的正则表达式的字符串
        //-->
    	</script>  

<hr>

## Bom:浏览器对象模型  
	    <script type="text/javascript">
        <!--
        /*
            Window对象的属性：
                1.innerHeight：返回文档显示区的高度
                2.innerWidth：返回文档显示区的宽度     IE不支持
                        通用写法：
                3.outerheight   包括工具栏、菜单栏的高度
                4.outerwidth    包括滚动条的宽度
         */

        function init() {
            var x = window.document.body.clientWidth;
            var y = window.document.body.clientHeight;
            alert(x + ":" + y);
        }

        //-->
    </script>
	</head>
	<body onload="init()">
	<p>你好</p>
	</body>  
  
<hr>

## Window对象：opener和parent属性  

<hr>

### opener属性  
opener.html页面  

	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>Window对象：opener属性</title>
    <script type="text/javascript">
        <!--
        /*
            Window对象的属性：
                1.opener属性：代表父窗口
                        应用：必须要求两个窗口拥有父子关系
                                1,超链接（设置target属性为_blank）
                                2.window.open()打开窗口
                2.parent属性：代表父窗口
                        使用地方 1.框架中
                                 2.内嵌框架
                3.frames[]：拿到子窗口
         */
        function fun() {
            window.open("sub.html")
        }

        //-->
    </script>
	</head>
	<body>
	<input type="text" name="" id="txt">
	<input type="button" value="打开sub.html页面" onclick="fun()">
	<a href="sub.html" target="_blank">打开sub.html页面</a>
	</body>
	</html>   
  
sub.html页面  
  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>传递子窗口的值到父窗口</title>
	</head>
	<script type="text/javascript">
    <!--
    //示例：将子窗口中的文本框中的数据传递到父窗口中的文本框中显示
    function fun() {
        //1.拿到文本框中填写的数据
        var v = document.getElementById("txt").value;
        //2.拿到父窗口对象
        var w = window.opener;
        //3.拿到父窗口中的文本框对象
        var txt = w.document.getElementById("txt");
        //4.将内容赋值给父窗口中的文本框对象的value属性
        txt.value = v;
    }

    //-->
	</script>
	<body>
	<input type="text" name="" id="txt">
	<input type="button" value="传递子窗口的值到父窗口中的文本框" onclick="fun()">
	</body>
	</html>

<hr>

### parent属性  
parent.html页面  
  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>Window对象：parent属性</title>
    <script type="text/javascript">
        <!--
        /*
            Window对象的属性：
                1.opener属性：代表父窗口
                        应用：必须要求两个窗口拥有父子关系
                                1,超链接（设置target属性为_blank）
                                2.window.open()打开窗口
                2.parent属性：代表父窗口
                        使用地方 1.框架中
                                 2.内嵌框架
                3.frames[]：拿到子窗口
         */
        function fun() {
            //1.拿到文本框中填写的数据
            var v = document.getElementById("txt").value;
            //2.拿到子窗口对象
            var w = window.frames[0];
            //3.拿到子窗口中的文本框对象
            var txt = w.document.getElementById("txt");
            //4.将内容赋值给父窗口中的文本框对象的value属性
            txt.value = v;
        }

        //-->
    </script>
	</head>
	<body>
	姓名<input type="text" name="" id="txt">
	<input type="button" value="传递数据到子窗口" onclick="fun()">
	<iframe src="sub1.html"></iframe>
	</body>
	</html>  
  
sub1.html页面    
  

	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>传递子窗口的值到父窗口</title>
	</head>
	<script type="text/javascript">
    <!--
    //示例：将子窗口中的文本框中的数据传递到父窗口中的文本框中显示
    function fun() {
        //1.拿到文本框中填写的数据
        var v = document.getElementById("txt").value;
        //2.拿到父窗口对象
        var w = window.parent;
        //3.拿到父窗口中的文本框对象
        var txt = w.document.getElementById("txt");
        //4.将内容赋值给父窗口中的文本框对象的value属性
        txt.value = v;
    }

    //-->
	</script>
	<body>
	<input type="text" name="" id="txt">
	<input type="button" value="传递数据到父窗口中" onclick="fun()">
	</body>
	</html>  
  
<hr>

## status属性  
	<script type="text/javascript">
    <!--
    /*
     */
    function init() {
        //拿到当前时间
        var d = new Date();
        //设置状态栏的文本
        self.status = d.toLocaleString();//self 等价于 window
    }

    //-->
	</script>  
  
<hr>

## window对象三种对话框  
	<script type="text/javascript">
    <!--
    /*
    三种对话框：
        1.消息对话框：alert();
        2.确认框：confirm():返回Boolean类型的值
        3.输入框：prompt():返回输入的字符串

     */
    //window.alert("你好");

    while (true) {
        if (confirm("你爱我吗？") == false)
            continue;
        break;
    }

    var a = prompt("请输入年龄", 27);
    alert(a);
    window.close();
    //-->
	</script>  
  
<hr>

## window对象的open方法   
	<script type="text/javascript">
    <!--
    function fun() {
        window.open("sub.html", "", "width=200,height=200,status=no,titlebar=no,menubar=no,toolbar=no,resizable=0");

    }

    //-->
	</script>
	<body>
	<input type="button" value="打开sub.html页面" onclick="fun()">
	</body>  
  
<hr>

## window对象的计时器方法   
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>window对象的计时器</title>
	</head>
	<script type="text/javascript">
    <!--
    /*
        window对象的计时器：
                1.setTimeout()：隔一段时间调用某个函数一次（只调用一次）,返回的是一个计时器，调用函数后自动销毁
                    clearTimeout()：销毁有setTimeout产生的计时器
                2.setInterval()：每隔一段时间调用某个函数（多次调用）
                    clearInterval()：销毁由setInterval()产生的计时器

     */
    var t;
    var t1;

    function fun() {
        //拿到p标签的主体内容
        var p = document.getElementById("p");
        var v = p.innerHTML;
        //将主体内容转换为number，转换后赋值回去
        p.innerHTML = v * 1 - 1;
        t = setTimeout("fun()", 1000);

    }

    function fun1() {
        //拿到p标签的主体内容
        var p = document.getElementById("p2");
        var v = p.innerHTML;
        //将主体内容转换为number，转换后赋值回去
        p.innerHTML = v * 1 - 1;

    }


    function fun2() {
        clearTimeout(t);

    }

    t1 = setInterval("fun1()", 1000);//一直存在，直到被销毁
    function fun3() {
        clearInterval(t1);
    }

    function fun4() {
        t1 = setInterval("fun1()", 1000);

    }

    //-->
	</script>
	<body>
	<p id="p">10</p>
	<p id="p2">100</p><br>
	<input type="button" value="演示setTimeout方法" onclick="fun()">
	<input type="button" value="演示clearTimeout方法" onclick="fun2()">
	<input type="button" value="演示setInterval方法" onclick="fun4()">
	<input type="button" value="演示clearInterval方法" onclick="fun3()">
	</body>
	</html>  
  
![](http://i.imgur.com/MHopVNF.jpg)  
  
<hr>

## window的模态窗体   
	<body>
	<script type="text/javascript">
    <!--
    /*
        window的模态窗体：
     */
    window.showModalDialog("你好");
    //-->
	</script>
	</body>  
  
<hr>

## history对象    
### A页面  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>history对象</title>
	</head>
	<script type="text/javascript">
    <!--
    /*
        history对象存储了访问过的页面
     */
    function fun() {
        history.forward();
    }

    //-->
	</script>
	<body>
	西安科技大学AAAAAAAAAAAAAAAAAAAAAA
	<a href="B.html">B.html</a>
	<input type="button" value="前进" onclick="fun()">
	</body>
	</html>  
  
### B页面  
  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>history对象</title>
	</head>
	<script type="text/javascript">
    <!--
    /*
        history对象存储了访问过的页面
     */
    function fun() {
        history.forward();
    }

    function fun1() {
        history.back();
    }

    function fun2() {
        history.go(2);
    }

    //-->
	</script>
	<body>
	西安科技大学BBBBBBBBBBBBBBBBBBB
	<a href="C.html">C.html</a>
	<input type="button" value="前进" onclick="fun()">
	<input type="button" value="后退" onclick="fun1()">
	<input type="button" value="末尾页面" onclick="fun2()">
	</body>
	</html>  

### C页面  
  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>history对象sub3</title>
	</head>
	<script type="text/javascript">
    <!--
    /*
        history对象存储了访问过的页面
     */
    function fun() {
        history.forward();
    }

    function fun1() {
        history.back();
    }

    function fun2() {
        history.go(-2);
    }

    //-->
	</script>
	<body>
	西安科技大学CCCCCCCCCCCCCCCCCCCCCC
	<a href="D.html">D.html</a>
	<input type="button" value="前进" onclick="fun()">
	<input type="button" value="后退" onclick="fun1()">
	<input type="button" value="返回首页" onclick="fun2()">
	</body>
	</html>   

### D页面  
  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>history对象sub3</title>
	</head>
	<script type="text/javascript">
    <!--
    /*
        history对象存储了访问过的页面
     */
    function fun1() {
        history.back();
    }

    function fun2() {
        history.go(-3);
    }

    //-->
	</script>
	<body>
	西安科技大学DDDDDDDDDDDDDDDDDDDDDDDDDDDDDDD
	<input type="button" value="后退" onclick="fun1()">
	<input type="button" value="直接去首页" onclick="fun2()">
	</body>
	</html>  
    

<hr>

## 鼠标的移动事件    
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>鼠标的移动事件</title>
    <style type="text/css">
        div {
            width: 300px;
            height: 300px;
            border: 1px solid red;
        }
    </style>
	</head>
	<script type="text/javascript">
    <!--
    /*
        //示例：当鼠标在div上移动的时候显示鼠标的坐标
     */

    function fun(e) {
        var x = e.clientX;
        var y = e.clientY;

        //显示在文本框中
        var txt = document.getElementById("txt");
        txt.value = x + ":" + y;
    }

    //-->
	</script>
	<body>
	<input type="text" name="id" id="txt">
	<div onmousemove="fun(event)"></div>
	</body>
	</html>  
  
![](http://i.imgur.com/BHxm5dK.jpg)  
  

<hr>

## location对象   
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>鼠标的移动事件</title>
	</head>
	<script type="text/javascript">
    <!--
    /*
        掌握： 1 href 属性
               2 reload() 重新加载本页面
     */
    function fun() {
        //window.location.href = "sub.html";
        window.location = "sub.html";
    }

    function fun1() {

        window.location.reload();
    }

    //-->
	</script>
	<body>
	<input type="button" value="直接去sub.html" onclick="fun()">
	<input type="button" value="重新加载" onclick="fun1()">
	</body>
	</html>  
  
<hr>

## 鼠标的悬停及移出事件   
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>鼠标的移动事件</title>
    <style>
        .one {
            color: red;
            border: 6px solid green;
            cursor: hand;
        }
    </style>
	</head>
	<script type="text/javascript">
    <!--
    /*
        掌握： 1 href 属性
               2 reload() 重新加载本页面
     */
    function fun() {
        //拿到p标签
        var p = document.getElementById("p");
        //定义p的样式
        //p.style.color = "red";
        //p.style.border = "5px dashed green";
        p.className = "one";
    }

    function fun1() {
        //拿到p标签
        var p = document.getElementById("p");
        p.className = "none";
    }

    //-->
	</script>
	<body>
	<p onmouseover="fun()" onmouseout="fun1()" id="p">你好，闫博文！</p>
	</body>
	</html>  
  
<hr>

## onload事件   
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>onload事件</title>
	</head>
	<script type="text/javascript">
    <!--
    /*
    
     */

    var n = 0;

    function init() {

        n++;
        if (n == 4)
            n = 1;
        //拿到图片对象
        var img = document.getElementById("img");
        //改变图片
        img.src = "images/" + n + ".jpg";
        //每隔一秒
        setTimeout("init()", 1000);
    }

    //-->
	</script>
	<body onload="init()">
	<img src="images/1.jpg" width="200" height="200" id="img">
	</body>
	</html>  
  
