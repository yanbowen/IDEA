<center>  

# HTML  

<hr width = "50%">

## HTML语言：超文本标记语言 --- Hypertext Markup Language  

</center>    

* IE浏览器是微软开发的  
* 2013-5-6 发布HTML5草案  
* XHTML 符合xml语法的HTML  

---

### 排版标签  
    <p align = "center">代表段落，单独占据一行</p>  
    <br>换号标记
	<hr width = "50%" color = "red" size = "10">线,单位：像素
	<pre>预先格式化，可显示空格</pre>
	<div id = "d" align = "center">块级标签，将对象作为块来对待，单独占据一行</div>
	<span>也是块级标签，不同点是不换行</span>

---

### 字体标签  
<font face = "楷体" size = "7" color = "0000FF">闫博文</font>  


    <h1 align = "center">字体标签，h后数字可修改</h1>
	<font face = "宋体" size = "1-7" color = "blue">红FF0000绿00FF00</font>  
  
* 将标签作为文本书写时，如下 ： &lt;p&gt;  
  
---

### 图片标签  
* 相对路径：相对当前页面的路径 `..相对于当前路径的上一级路径 .当前路径`
* 绝对路径： a.以逻辑盘符开始的路径 `----` b.网络路径 http://www.baidu.com/images/2.jpg
* border可做相框
* title公共属性：提示性文本
* align:是指图片和周围文字的相对位置  
* 如下：  

    <img src = "images/1.jpg" width = "100" height = "100" alt = "美女" border = "10" title = "提示性文本"> 

	`<img src = "images/1.jpg" width = "100" height = "100" alt = "美女" border = "10" title = "提示性文本">` 
 
---

### 超链接  
<a href = "out.html" name = "out">超链接</a>  
<a href = "#a">回到顶部</a>

	 <a href = "out.html" name = "out">超链接</a>
	 <a href = "#a">回到顶部</a>  

* 外部链接：链接到一个外部文件  
* 锚链接： 链接到本页面或者其他页面的特定位置（如：网页下拉后 置顶） 

---

### 热点问题  

* 热点问题：指对图片的局部区域加超链  


---

### 清单标签  
* 无序清单：type:取值：disc,square,circle  
	<ul type = "disc">
		<li>中国</li>
		<li type = "square">美国</li>
		<li>日本</li>
	</ul>  
	`<ul type = "disc">
		<li>中国</li>
		<li type = square>美国</li>
		<li>日本</li>
	 </ul> `  

* 有序清单：type：取值：1,a,A,i,I  
	<ol type = "I" start = "10">
		<li>中国</li>
		<li>美国</li>
		<li>日本</li>
	</ol>  
	`<ul type = "I" start = "10">
		<li>中国</li>
		<li>美国</li>
		<li>日本</li>
	 </ul> ` 

* 定义清单 ： dt:清单标题  
	<dl>
		<dt>第一条</dt>
		<dd>做一个勇敢的人</dd>
		<dd>做一个快乐的人</dd>
		<dt>第二条</dt>
		<dd>做一个勇敢的人</dd>
		<dd>做一个快乐的人</dd>
	</dl>

	`<dl>
		<dt>第一条</dt>
		<dd>做一个勇敢的人</dd>
		<dd>做一个快乐的人</dd>
		<dt>第二条</dt>
		<dd>做一个勇敢的人</dd>
		<dd>做一个快乐的人</dd>
	`</dl>  

---

### 表格标签  

<table border = "1" width = "500" height = "300" align = "center" cellpadding = "20" cellspacing = "10" bordercolordark = "red" bordercolorlight = "blue" bgcolor = "#ffcccc" background = "images/1.jpg" dir = "rtl">
	<tr bgcolor = "#00cc00">
		<td valign = "bottom">刘德华</td>
		<td>51</td>
		<td>香港</td>
		<td>男</td>
	</tr>
	<tr>
		<td rowspan = "2">郭靖 貂蝉</td>
		<td>27</td>
		<td align = "center">汴梁</td>
		<td>男</td>
	</tr>
	<tr>
		
		<td>22</td>
		<td>洛阳</td>
		<td>女</td>
	</tr>
</table>  

`<table border = "1" width = "500" height = "300" align = "center" cellpadding = "20" cellspacing = "10" bordercolordark = "red" bordercolorlight = "blue" bgcolor = "#ffcccc" background = "images/1.jpg" dir = "rtl">
	<tr bgcolor = "#00cc00">
		<td valign = "bottom">刘德华</td>
		<td>51</td>
		<td>香港</td>
		<td>男</td>
	</tr>
	<tr>
		<td>郭靖</td>
		<td>27</td>
		<td align = "center">汴梁</td>
		<td>男</td>
	</tr>
	<tr>
		<td>貂蝉</td>
		<td>22</td>
		<td>洛阳</td>
		<td>女</td>
	</tr>
</table>`  

---

### 框架集   

	<frameset rows = "200,*" bordercolor = "red">
		<frame src = "out.html" noresize scrolling = "no"></frame>
		<frameset cols = "100,*">
			<frame src = "left.html"></frame>
			<frame src = "in.html"></frame>
		</frameset>
	</frameset>  
  
![](http://i.imgur.com/0tHGyIP.png)  

* 分块后属性 noresize控制是否可以拖动  
* scrolling 是否可以滑动
* bordercolor 分框颜色

---

### 表单标签   

	<form>
		姓名：<input type = "text" value = "请输入姓名" size = "50" readonly><br>
		密码：<input type = "password" value = "请输入姓名" size = "50" ><br>
		隐藏框：<input type = "hidden" value = "请输入姓名" size = "50" ><br>
		性别：<input type = "radio" name = "gender" value = "male" checked>男<input type = "radio" name = "gender" value = "female">女<br>
		国籍：<input type = "radio" name = "country" value = "china" checked>中国<input type = "radio" name = "country" value = "american">美国<br>
		爱好：<input type = "checkbox" name = "love" value = "eat" checked>吃饭<input type = "checkbox" name = "love" value = "sleep" checked>睡觉<input type = "checkbox" name = "love" value = "study" checked>学Java<br>
		学历：<select name = "xueli">
					<option value = "大学">大学</option>
					<option value = "高中">高中</option>
					<option value = "小学">小学</option>
			 </select><br>
		备注：<textarea rows = "5" cols = "20">留言留言留言</textarea><br>
		<input type = "button" value = "普通按钮" onclick = "alert(this.value)"><br>
		<input type = "submit" value = "提交按钮"><br>
		<input type = "reset" value = "重置按钮"><br>
		<input type = "image" src = "images/1.jpg" width = "80" height = "30"><br>
	</form>  

* readonly :只读 无法输入
* disabled :点击都不行
* value ：文本框内容，传递给服务器的值
* multiple:多选  

	<form>
		姓名：<input type = "text" value = "请输入姓名" size = "50" readonly><br>
		密码：<input type = "password" value = "请输入姓名" size = "50" ><br>
		隐藏框：<input type = "hidden" value = "请输入姓名" size = "50" ><br>
		性别：<input type = "radio" name = "gender" value = "male" checked>男<input type = "radio" name = "gender" value = "female">女<br>
		国籍：<input type = "radio" name = "country" value = "china" checked>中国<input type = "radio" name = "country" value = "american">美国<br>
		爱好：<input type = "checkbox" name = "love" value = "eat" checked>吃饭<input type = "checkbox" name = "love" value = "sleep" checked>睡觉<input type = "checkbox" name = "love" value = "study" checked>学Java<br>
		学历：<select name = "xueli">
					<option value = "大学">大学</option>
					<option value = "高中">高中</option>
					<option value = "小学">小学</option>
			 </select><br>
		备注：<textarea rows = "5" cols = "20">留言留言留言</textarea><br>
		<input type = "button" value = "普通按钮" onclick = "alert(this.value)"><br>
		<input type = "submit" value = "提交按钮"><br>
		<input type = "reset" value = "重置按钮"><br>
		<input type = "image" src = "images/1.jpg" width = "80" height = "30"><br>
	</form>  

---

### 表单语义化   
	<fieldset>
		<legend>选填信息</legend>
		姓名：<input type = "text" value = "请输入姓名" size = "50" readonly><br>
	</fieldset>
	<fieldset>
		<legend>选填信息</legend>
		姓名：<input type = "text" value = "请输入姓名" size = "50" readonly><br>
	</fieldset>  
  
* `<fieldset>`标签是添加边框；`<legend>`标签是添加文字；
	<fieldset>
		<legend>选填信息</legend>
		姓名：<input type = "text" value = "请输入姓名" size = "50" ><br>
	</fieldset>
	<fieldset>
		<legend>选填信息</legend>
		姓名：<input type = "text" value = "请输入姓名" size = "50" ><br>
	</fieldset>  

---

### 多媒体标签   
	<bgsound src = "http://cdn.y.baidu.com/2353657f691b51f88ccc5a301ac88b88.mp3"></bgsound>
	<video src = "http://cdn.y.baidu.com/2353657f691b51f88ccc5a301ac88b88.mp3" autostart = "true"></video>
* loop播放次数  
* embed播放视频  
* video是HTML5最新播放视频  
* autostart是否自动开始


<bgsound src = "http://cdn.y.baidu.com/2353657f691b51f88ccc5a301ac88b88.mp3"></bgsound>
<video src = "http://cdn.y.baidu.com/2353657f691b51f88ccc5a301ac88b88.mp3" autostart = "true"></video>
<marquee direction = "" behavior = "slide">我来了</marquee>
<marquee direction = "" behavior = "alternate">我来了</marquee>
<marquee direction = "" behavior = "scroll" loop = "3">我来了</marquee>  

---

### 头标签   
`<html lang = "en"></html>` <br>
`<head>` <br>
`<meta http-equiv = "refresh" content = "3;url=http://www.baidu.com">` 刷新 3秒刷新到百度页面 <br>
`</head>`  

* `<label>`标签
* `<label onclick = "alert(this.innerHTML)"></label>`