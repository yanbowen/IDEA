# JavaScript与DOM2  

<hr>

## 鼠标单击事件  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>鼠标的单击事件</title>
	</head>
	<script type="text/javascript">
    <!--
    //点击按钮，隐藏图片
    function init() {

        //拿到按钮对象
        var btn = document.getElementById("btn");
        var btn1 = document.getElementById("btn1");
        //注册事件
        btn.onclick = function () {
            //拿到图片对象
            var img = document.getElementById("img");
            img.style.display = "none";
            this.disabled = "true";
        }
        btn1.onclick = function () {
            var img = document.getElementById("img");
            img.style.display = "block";
            //删除属性
            var btn = document.getElementById("btn");
            btn.removeAttribute("disabled");
        }

    }

    function fun2(obj) {
        obj.value = "闫博文";
    }

    function fun3() {
        var p = document.getElementById("p");
        p.innerHTML = "<img src= 'images/1.jpg' width='200' height='200' id='img'>";

    }

    function fun4() {
        var btn2 = document.getElementById("btn2");
        btn2.removeAttribute("onclick")

    }

    //-->
	</script>
	<body onload="init()">
	<img src="images/1.jpg" width="200" height="200" id="img"><br>
	<input type="button" value="图片隐藏" id="btn">
	<input type="button" value="图片可见" id="btn1">
	<input type="button" value="西南科技大学" id="btn2" onclick="fun2(this)">
	<input type="button" value="添加一张图片" id="btn3" onclick="fun3()">
	<input type="button" value="去掉西南科大按钮单击事件" id="btn4" onclick="fun4()">
	<p id="p"></p>
	</body>
	</html>  
  
<hr>

## 加载与卸载事件  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>加载与卸载事件</title>
	</head>
	<script type="text/javascript">
    <!--
    function init() {
        alert("你好");
    }

    function fun() {
        alert("西南科技大学");
    }

    function fun2() {
        alert("exit");
    }

    //-->
	</script>
	<body onload="init(),fun()" onunload="fun2()">
	AAAAAAAAAAAA
	</body>
	</html>  
  
<hr>

## 聚焦离焦事件  
	<script type="text/javascript">
    <!--
    function init(obj) {
        obj.style.border = "1px solid red";
        obj.style.backgroundColor = "#FF88FF"
        obj.style.color = "blue";
    }

    function fun1(obj) {
        if (obj.value == "") {
            obj.focus();//获得焦点
        }
    }

    //-->
	</script>
	<body>
	<input type="text" name="" onfocus="init(this)" onblur="fun1(this)">
	</body>  
  
<hr>

## 键盘事件  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>键盘事件</title>
	</head>
	<script type="text/javascript">
    <!--
    /*
            onkeypress :键盘按下再抬起
            onkeydown :键盘按下
            onkeyup :键盘抬起
     */
    function init(obj, e) {

        //按键得到asc码
        var key = e.keyCode;
        obj.value = key;
    }

    //-->
	</script>
	<body>
	<input type="text" name="" onkeypress="init(this,event)">
	</body>
	</html>  
  
<hr>

## 提交与重置事件  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>提交与重置事件</title>
	</head>
	<script type="text/javascript">
    <!--
    /*

     */

    function check(form) {
        //拿到文本框
        var txt = form.username.value;
        //判断内容
        if (txt == "") {
            document.getElementById("sname").innerHTML = "<font color = red>* 姓名必须填写</font>";
            form.username.focus();
            return false;
        }
        return true;
    }

    //-->
	</script>
	<body>
	<form method="post" action="1鼠标的单击事件.html" onsubmit="return check(this)">
    姓名：<input type="text" name="username">
    <span id="sname"></span>
    <br>
    <input type="submit" value="提交">
	</form>
	</body>
	</html>  
  
<hr>

## 提交与重置事件  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>提交与重置事件</title>
	</head>
	<script type="text/javascript">
    <!--
    /*

     */

    function check(form) {
        //拿到文本框
        var txt = form.username.value;
        //判断内容
        if (txt == "") {
            document.getElementById("sname").innerHTML = "<font color = red>* 姓名必须填写</font>";
            form.username.focus();
            return false;
        }
        return true;
    }

    function fun() {
        alert("sss");
        return true;

    }

    //-->
	</script>
	<body>
	<form method="post" action="1鼠标的单击事件.html" onsubmit="return check(this)" onreset="return fun(this)">
    姓名：<input type="text" name="username">
    <span id="sname"></span>
    <br>
    <input type="submit" value="提交">
    <input type="reset" value="重置">
	</form>
	</body>
	</html>   
  
<hr>

## 选择与改变事件  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>选择与改变事件</title>
	</head>
	<script type="text/javascript">
    <!--
    /*
        onchange :改变的同时，必须失去焦点
     */
    function fun(obj) {
        alert(obj.value);
    }

    function fun1(v) {
        alert(v);
    }

    function fun2(v, index) {
        alert(v + ":" + index);

    }

    //-->
	</script>
	<body>
	<input type="text" name="" onselect="fun(this)" onchange="fun1(this.value)">
	<select onchange="fun2(this.value,this.selectedIndex)">
    <option value="china">中国</option>
    <option value="america">美国</option>
    <option value="japan">日本</option>
	</select>
	</body>
	</html>  
  
<hr>

## 省市联动  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>省市联动</title>
	</head>
	<script type="text/javascript">
    <!--
    var arr = ["中国", "美国", "日本"];

    arr["中国"] = ["北京", "上海", "钓鱼岛"];
    arr["美国"] = ["纽约", "华盛顿", "旧金山"];
    arr["日本"] = ["东京", "大阪", "神户"];

    arr["北京"] = ["海淀", "朝阳", "昌平", "丰台"];
    arr["上海"] = ["浦东", "金山", "崇明", "浦西"];
    arr["钓鱼岛"] = ["钓鱼岛东", "钓鱼岛南", "钓鱼岛西", "钓鱼岛北"];

    arr["纽约"] = ["纽约1", "纽约2", "纽约3", "纽约4"];
    arr["华盛顿"] = ["华盛顿1", "华盛顿2", "华盛顿3", "华盛顿4"];
    arr["旧金山"] = ["旧金山1", "旧金山2", "旧金山3", "旧金山4"];

    arr["东京"] = ["东京1", "东京2", "东京3", "东京4"];
    arr["大阪"] = ["大阪1", "大阪2", "大阪3", "大阪4"];
    arr["神户"] = ["神户1", "神户2", "神户3", "神户4"];

    function init1() {

        //填充国家
        for (var i = 0; i < arr.length; i++) {
            //创建option对象
            //第一种
            var option = new Option();
            option.text = arr[i];
            option.value = arr[i];
            //将option添加到国家select
            document.getElementById("country").options.add(option);
        }

        //填充省市
        for (var i = 0; i < arr[arr[0]].length; i++) {
            //创建option对象
            //第一种
            var option = new Option();
            option.text = arr[arr[0]][i];
            option.value = arr[arr[0]][i];
            //将option添加到国家select
            document.getElementById("province").options.add(option);
        }

        //填充地区
        for (var i = 0; i < arr[arr[arr[0]][0]].length; i++) {
            //创建option对象
            //第一种
            var option = new Option();
            option.text = arr[arr[arr[0]][0]][i];
            option.value = arr[arr[arr[0]][0]][i];
            //将option添加到国家select
            document.getElementById("area").options.add(option);
        }

    }

    function init() {
        //填充国家
        fillData(arr, "country");
        //填充省市
        fillData(arr[arr[0]], "province");
        //填充地区
        fillData(arr[arr[arr[0]][0]], "area");
    }

    function fillData(arr, id) {
        //清空省市
        document.getElementById(id).options.length = 0;
        //添加选项
        for (var i = 0; i < arr.length; i++) {
            //创建option对象
            /*
            //第一种
            var option = new Option();
            option.text = arr[i];
            option.value = arr[i];
            */
            //第二种
            var option = new Option(arr[i], arr[i]);

            //将option添加到select
            document.getElementById(id).options.add(option);
        }
    }

    function changePro(coun) {

        //添加省市
        fillData(arr[coun], "province");

        //添加地区
        fillData(arr[arr[coun][0]], "area");
    }

    function changeArea(pro) {

        //添加地区
        fillData(arr[pro], "area");
    }

    //-->
	</script>
	<body onload="init()">
	国家：<select id="country" onchange="changePro(this.value)"></select>
	省市：<select id="province" onchange="changeArea(this.value)"></select>
	地区：<select id="area"></select>
	</body>
	</html>   
  
<hr>

## document对象的集合属性  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>document对象的集合属性</title>
	</head>
	<script type="text/javascript">
    <!--

    function fun() {
        document.all[6].innerHTML = "你好";//从<head>开始 计数1

        document.forms[1].username.value = "张无忌";

        document.images[2].src = "images/1.jpg";
    }

    //-->
	</script>
	<body onload="fun()">
	<p></p>
	<form method="post" action="">
    姓名1：<input type="text" name="">
	</form>
	<form method="post" action="">
    姓名2：<input type="text" name="username">
	</form>
	<form method="post" action="">
    姓名3：<input type="text" name="">
	</form>
	<img src="" alt="aa"><br>
	<img src="" alt="aa"><br>
	<img src="" alt="aa">
	</body>
	</html>  
  
<hr>

## 图片轮播  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>9图片轮播</title>
	</head>
	<style>
    #d {
        position: relative;
        top: -30px;
    }

    label {
        margin-left: 23px;
    }

    .one {
        width: 10px;
        height: 10px;
        border: 1px solid black;
        background-color: white;
    }
	</style>
	<script type="text/javascript">
    <!--

    var n = 0;
    var t = 0;

    function init() {
        var lbs = document.getElementsByTagName("label");
        //注册label事件
        for (var i = 0; i < lbs.length; i++) {
            lbs[i].onmouseover = function () {
                //让事件先停下来
                clearTimeout(t);
                //让图片显示为相应的选项
                var num = this.innerText * 1;
                //拿到img标签
                var img = document.getElementById("img");
                img.src = "images/" + num + ".jpg";
                //清空所以样式
                clearStyle();
                //让label样式变成one
                this.className = "one";

            }

            lbs[i].onmouseout = function () {
                //隔1秒调用fun()
                t = setTimeout("fun()", 1000);
                //改变当前n的值
                n = this.innerText * 1;
            }
        }

        fun();
    }

    function fun() {
        n++;
        if (n == 7)
            n = 1;
        //拿到图标对象
        var img = document.getElementById("img");
        img.src = "images/" + n + ".jpg";
        //清空所以样式
        clearStyle();
        //设定相应的label控件的样式
        document.getElementById("i" + n).className = "one";

        t = setTimeout("fun()", 1000);
    }

    function clearStyle() {
        //先清空所以label的样式
        var lbs = document.getElementsByTagName("label");
        for (var i = 0; i < lbs.length; i++) {
            lbs[i].className = "";
        }
    }

    //-->
	</script>
	<body onload="init()">
	<div align="center">
    <img src="images/1.jpg" width="460" height="520" id="img">
    <div id="d">
        <label id="i1">&nbsp;1&nbsp;</label>
        <label id="i2">&nbsp;2&nbsp;</label>
        <label id="i3">&nbsp;3&nbsp;</label>
        <label id="i4">&nbsp;4&nbsp;</label>
        <label id="i5">&nbsp;5&nbsp;</label>
        <label id="i6">&nbsp;6&nbsp;</label>

    </div>
	</div>
	</body>
	</html>   
  
<hr>

## DOM技术概述  
HTML 文档对象模型（HTML Document Object Model）定义了访问和处理 HTML 文档的标准方法。  
  
* Core DOM：定义了一套标准的针对任何结构化文档的对象 
* XML DOM：定义了一套标准的针对 XML 文档的对象 
* HTML DOM：定义了一套标准的针对 HTML 文档的对象  
  
<hr>

## DOM节点属性  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>DOM技术概述-节点属性</title>
	</head>
	<body>
	<p id="p">你好</p>
	<script type="text/javascript">
    <!--
    var p = document.getElementById("p");
    alert(p.nodeName + " :" + p.nodeValue + " :" + p.nodeType);

    //-->
	</script>
	</body>
	</html>  
  
<hr>

## DOM节点的导航  
IE11 chrome新版 无法执行  
  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>DOM节点的导航</title>
	</head>
	<body>
	<table>
    <tr>
        <td>成龙</td>
        <td>男</td>
        <td>60</td>
    </tr>
    <tr>
        <td>小龙女</td>
        <td>女</td>
        <td>18</td>
    </tr>
    <tr>
        <td>张春华</td>
        <td>女</td>
        <td>28</td>
    </tr>
	</table>
	<script type="text/javascript">
    <!--
        //拿到成龙的年龄
        //拿到根节点
        var root = document.documentElement;
        //alert(root.nodeName);
        //拿到body节点
        var body = root.lastChild;
        //alert(body.nodeName);
        var table = body.firstChild.nextSibling;
        //alert(body.firstChild.nextSibling.nodeName);
        //拿到tbody节点
        var tbody = table.lastChild;
        //拿到成龙年龄//nextSibling下一个兄弟//lastChild小儿子
        //alert(tbody.nodeName);
        var age = tbody.firstChild.firstChild.nextSibling;
        alert(age.nodeName);
    //-->
	</script>
	</body>
	</html>  
  
<hr>

## 获取标签节点对象的方法  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>获取标签节点对象的方法</title>
	</head>
	<body>
	<h1 id="h1">明天休息</h1>
	<script type="text/javascript">
    <!--
    //示例： 拿到明天休息的文本
    //第一种方式
    var h1 = document.getElementById("h1");
    //第二种方法
    var h2 = document.getElementsByTagName("h1");
    alert(h2[0].innerHTML);
    //alert(h1.innerHTML);
    //alert(h1.firstChild.nodeValue);
    //alert(h1.lastChild.nodeValue);
    alert(h1.innerText);

    //-->
	</script>
	</body>
	</html>  
  
<hr>

## 列表的文本  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>列表的文本值</title>
	</head>
	<body>
	<ul>
    <li id="bj" value="beijing">
        北京
        <h1>海淀</h1>
        上海
    </li>
    <li id="nj" value="nanjing">
        南京
    </li>
    <br>
    <input type="button" value="li取值" onclick="getLi()">
	</ul>
	<script type="text/javascript">
    <!--
    function getLi() {
        //拿到北京节点
        var li = document.getElementById("bj");
        //拿到北京节点的所有子节点
        var childs = li.childNodes;
        for (var i = 0; i < childs.length; i++) {
            //alert(childs[i].nodeName + ":" + childs[i].nodeValue + ":" + childs[i].nodeType);
            if (childs[i].nodeType == 1) {
                //nodeType 值为1 说明其 为标签节点，其就有子节点
                alert(childs[i].firstChild.nodeValue);
            } else {
                alert(childs[i].nodeValue);
            }
        }
    }

    //-->
	</script>
	</body>
	</html>  
  
<hr>

## 获取下拉列表框的option文本  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>获取下拉列表框的option文本</title>
	</head>
	<body>
	<select name="edu" id="edu">
    <option value="本科">本科</option>
    <option value="专科">专科</option>
    <option value="高中">高中</option>
    <option value="小学">小学</option>
    <option value="幼儿园">幼儿园</option>
	</select><br>
	<script type="text/javascript">
    <!--
    var ops = document.getElementsByTagName("option");
    for (var i = 0; i < ops.length; i++) {
        //alert(ops[i].text);
        alert(ops[i].innerHTML);
    }

    //-->
	</script>
	</body>
	</html>  
  
<hr>

## 复制、克隆节点  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>获取下拉列表框的option文本</title>
	</head>
	<body>
	<ul>
    <li id="bj" onclick="changeNode()">北京</li>
    <li>湖南</li>
    <li>山东</li>
	</ul>
	<ul>
    <li id="game">打<p>灰机</p></li>
    <li>抓泥鳅</li>
    <li>斗地主</li>
	</ul>
	<script type="text/javascript">
    <!--

    function changeNode() {
        //拿到北京节点
        var bjNode = document.getElementById("bj");
        //拿到打灰机对象
        var gameNode = document.getElementById("game");
        //替换
        //bjNode.parentNode.replaceChild(gameNode, bjNode);
        //克隆一份打灰机
        var node = gameNode.cloneNode(true);
        bjNode.parentNode.replaceChild(node, bjNode);
    }

    //-->
	</script>
	</body>
	</html>  
  
<hr>

## 添加下拉框的选项  
	<!DOCTYPE html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>添加下拉框选项</title>
	</head>
	<script type="text/javascript">
    <!--

    function addOptions() {
        //创建一个新的节点
        var option = document.createElement("option");
        option.value = "小学";
        option.text = "小学";
        //拿到下拉框。加入小学
        document.getElementsByTagName("select")[0].options.add(option);

        //第二种方式
        //获得select对象
        var select = document.getElementsByTagName("select")[0];
        select.innerHTML = select.innerHTML + "<option value='幼儿园'>幼儿园</option>"

        //第二种方式//appendChild//IE不能用
    }

    function fun() {

        //拿到div对象
        var d = document.getElementById("d");
        //创建一个img标签对象
        var img = document.createElement("img");
        //指定属性
        img.src = "images/1.jpg";
        img.style.width = "200px";
        img.height = "300";//不写单位
        //将图片添加到div中
        d.appendChild(img);
    }

    //-->
	</script>
	<body>
	<input type="button" value="添加选项" onclick="addOptions()">
	<input type="button" value="添加图片" onclick="fun()">
	<select>
    <option>本科</option>
    <option>专科</option>
    <option>高中</option>
    <option>初中</option>
	</select><br>
	<div id="d"></div>
	</body>
	</html>   
  
<hr>

## 全选全不选  
	<!doctype html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>全选全不选</title>
	</head>
	<script type="text/javascript">
    <!--
    function checkAll(flag) {
        //拿到所有的多选框
        var hobbys = document.getElementsByName("hobby");
        //循环赋值
        for (var i = 0; i < hobbys.length; i++) {
            hobbys[i].checked = flag;
        }
    }

    function reverseCheck() {
        //拿到所有的多选框
        var hobbys = document.getElementsByName("hobby");
        //循环赋值
        for (var i = 0; i < hobbys.length; i++) {
            hobbys[i].checked = !hobbys[i].checked;
        }
    }

    //-->
	</script>
	<body>
	<h1>请选择你的爱好：</h1>
	全选/全不选<input type="checkbox" name="hobbys" onclick="checkAll(this.checked)"/><br/>
	<input type="checkbox" name="hobby" value="football"/>足球
	<input type="checkbox" name="hobby" value="basketball"/>篮球
	<input type="checkbox" name="hobby" value="swim"/>游泳
	<input type="checkbox" name="hobby" value="singing"/>唱歌<br/>
	
	<input type="button" value="全选" onclick="checkAll(true)"/> <input type="button" value="全不选" onclick="checkAll(false)"/>
	<input type="button" value="反选" onclick="reverseCheck()"/></body>

	</body>
	</html>

<hr>

## 移动下拉框选项（单项）  
	<!doctype html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>移动下拉框选项(单项)</title>
	</head>
	<script type="text/javascript">
    <!--
    function removeLeft() {
        //拿到左边下拉框的对象
        var leftSel = document.getElementById("left");
        //拿到右边的下拉框对象
        var rightSel = document.getElementById("right");

        //拿到左边下拉框选中的option
        var op = leftSel.options[leftSel.selectedIndex];

        //将选中选项添加到右边下拉框中
        rightSel.appendChild(op);
    }

    function removeLeftAll() {
        //拿到左边下拉框的对象
        var leftSel = document.getElementById("left");
        //拿到右边的下拉框对象
        var rightSel = document.getElementById("right");

        //循环添加
        var length = leftSel.options.length;
        for (var i = 0; i < length; i++) {
            rightSel.appendChild(leftSel.options[0]);
        }

    }

    //-->
	</script>
	<body>
	<table align="center">
    <tr>
        <td>
            <select size="10" id="left">
                <option>选项1</option>
                <option>选项2</option>
                <option>选项3</option>
                <option>选项4</option>
                <option>选项5</option>
                <option>选项6</option>
                <option>选项7</option>
                <option>选项8</option>

            </select>
        </td>
        <td>
            <input type="button" value="--->" onclick="removeLeft()"/><br/>
            <input type="button" value="===>" onclick="removeLeftAll()"/><br/>
            <input type="button" value="<---" onclick=""/><br/>
            <input type="button" value="<===" onclick=""/><br/>
        </td>
        <td>
            <select size="10" id="right">

                <option>选项9</option>
            </select>
        </td>
    </tr>
	</table>
	</body>
	</html>  
  
<hr>

## 移动下拉框选项（多项）  
	<!doctype html>
	<html lang="en">
	<head>
    <meta charset="UTF-8">
    <title>下拉框选项的移动(多项)</title>
	</head>
	<script type="text/javascript">
    <!--
    function removeLeft() {
        //拿到左边下拉框的对象的option数组
        var leftOps = document.getElementById("left").options;
        //拿到右边的下拉框对象
        var rightSel = document.getElementById("right");

        for (var i = 0; i < leftOps.length; i++) {
            if (leftOps[i].selected) {
                //说明选中了
                rightSel.appendChild(leftOps[i]);
                i--;
            }
        }
    }

    function removeLeftAll() {
        //拿到左边下拉框的对象
        var leftSel = document.getElementById("left");
        //拿到右边的下拉框对象
        var rightSel = document.getElementById("right");

        //循环添加
        var length = leftSel.options.length;
        for (var i = 0; i < length; i++) {
            rightSel.appendChild(leftSel.options[0]);
        }

    }

    //-->
	</script>
	<body>
	<table align="center">
    <tr>
        <td>
            <select size="10" id="left" multiple>
                <option>选项1</option>
                <option>选项2</option>
                <option>选项3</option>
                <option>选项4</option>
                <option>选项5</option>
                <option>选项6</option>
                <option>选项7</option>
                <option>选项8</option>

            </select>
        </td>
        <td>
            <input type="button" value="--->" onclick="removeLeft()"/><br/>
            <input type="button" value="===>" onclick="removeLeftAll()"/><br/>
            <input type="button" value="<---" onclick=""/><br/>
            <input type="button" value="<===" onclick=""/><br/>
        </td>
        <td>
            <select size="10" id="right">

                <option>选项9</option>
            </select>
        </td>
    </tr>
	</table>
	</body>
	</html>
