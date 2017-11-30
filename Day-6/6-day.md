# XML&DOM_SAX&dom4j编程  

<hr>

## Junit测试   
测试方法的写法：  
 
* 方法必须是公有  
* 方法返回值必须是void
* 方法的参数必须无参 
* 前面必须加 @Test注解  
* @before ： 是每个测试方法执行之前都要调用一次此方法
* @beforeclass：是所有测试方法执行之前必须要调用一次方法（只会调用一次）  
  
![](https://i.imgur.com/Cj9Wvwi.jpg)  
  
<hr>
## XML文件概述   
* XML:可扩展标记语言(eXtensible Markup Language)  
	* 传输数据
	* 配置文件（主要用途）  
	
* DTD（Document Type Definition）:文档类型定义  

* XML解析：DOM方式和SAX方式  

* SAX：Simple API for XML  

* 解析开发包
	* JAXP：是SUN公司推出的解析标准
	* Dom4J:是开源组织推出的解析开发包（大家都在用） 
	* JDom
  
### book.xml  
	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<书架>
	<书 ISBN="黑莓">
		<书名>葵花宝典</书名>
		<作者>安倍晋三</作者>
		<售价>
			100
			<内部件>50</内部件>

		</售价>
		<批发价>60</批发价>
	</书>
	<书>
		<书名>金瓶梅</书名>
		<作者>安倍晋四</作者>
		<售价>80</售价>
	</书>
	</书架>
  
### DOM_PARSEXML.java  
	package dom;

	import javax.xml.parsers.DocumentBuilder;
	import javax.xml.parsers.DocumentBuilderFactory;
	import javax.xml.transform.Transformer;
	import javax.xml.transform.TransformerFactory;
	import javax.xml.transform.dom.DOMSource;
	import javax.xml.transform.stream.StreamResult;

	import org.w3c.dom.Document;
	import org.w3c.dom.Element;
	import org.w3c.dom.Node;
	import org.w3c.dom.NodeList;

	//演示dom方式解析XML文件
	public class DOM_PARSEXML {

	public static void main(String[] args) throws Exception {
		// 创建解析器对象
		DocumentBuilder db = DocumentBuilderFactory.newInstance().newDocumentBuilder();
		// 加载XML文档
		Document document = db.parse("src/dom/book.xml");

		// test1(document);
		// test2(document);
		// test3(document);
		// test4(document);
		// test5(document);
		// test6(document);
		test7(document);

	}

	// 1.得到具体某个节点内容：eg:拿到金瓶梅的售价
	public static void test1(Document document) {

		// 拿到所有售价节点
		NodeList list = document.getElementsByTagName("售价");
		// 获得金瓶梅的售价节点
		Node n = list.item(1);
		// 获取售价文本
		System.out.println(n.getTextContent());

	}

	// 2.遍历所有元素节点(递归)
	public static void test2(Node node) {

		// 对node节点进行循环
		NodeList n1 = node.getChildNodes();
		// 循环判断
		for (int i = 0; i < n1.getLength(); i++) {
			Node n = n1.item(i);
			if (n.getNodeType() == Node.ELEMENT_NODE) {
				// 说明此节点是标签节点
				System.out.println(n.getNodeName());
				test2(n);
			}
		}
	}

	// 3.修改某个元素节点的主体内容eg:修改金瓶梅的价格

	public static void test3(Document document) throws Exception {
		// 拿到所有售价节点
		NodeList list = document.getElementsByTagName("售价");
		// 获得金瓶梅的售价节点
		Node n = list.item(1);
		// 修改主体内容
		n.setTextContent("80");
		// 将修改结果保存的硬盘
		Transformer tf = TransformerFactory.newInstance().newTransformer();
		tf.transform(new DOMSource(document), new StreamResult("src/dom/book.xml"));

	}

	// 4. 向指定元素节点中增加子元素节点：eg ：给葵花宝典的售价增加一个内部价节点：50
	public static void test4(Document document) throws Exception {
		// 拿到所有售价节点
		NodeList list = document.getElementsByTagName("售价");
		// 获得葵花宝典的售价节点
		Node n = list.item(0);
		// 创建新的节点
		Element el = document.createElement("内部价");
		// 设置节点的主体内容
		el.setTextContent("50");
		// 将内部件节点挂接到售价节点上
		n.appendChild(el);
		// 保存到硬盘上
		Transformer tf = TransformerFactory.newInstance().newTransformer();
		tf.transform(new DOMSource(document), new StreamResult("src/dom/book.xml"));

	}

	// 5.向指定元素节点上增加同级元素节点： eg: 给葵花宝典的售价增加一个批发价节点：60
	public static void test5(Document document) throws Exception {
		// 拿到所有书节点
		NodeList list = document.getElementsByTagName("书");
		// 获得葵花宝典的书节点
		Node n = list.item(0);
		// 创建新的批发价节点
		Element el = document.createElement("批发价");
		// 设置节点的主体内容
		el.setTextContent("60");
		// 将内部件节点挂接到售价节点上
		n.appendChild(el);
		// 保存到硬盘上
		Transformer tf = TransformerFactory.newInstance().newTransformer();
		tf.transform(new DOMSource(document), new StreamResult("src/dom/book.xml"));

	}

	// 6.删除指定元素节点 eg:删除内部价节点
	public static void test6(Document document) throws Exception {
		// 拿到所有内部价节点
		NodeList list = document.getElementsByTagName("内部价");
		// 获得葵花宝典的内部价节点
		Node n = list.item(0);
		// 父亲干掉儿子
		n.getParentNode().removeChild(n);
		// 保存到硬盘上
		Transformer tf = TransformerFactory.newInstance().newTransformer();
		tf.transform(new DOMSource(document), new StreamResult("src/dom/book.xml"));

	}

	// 7.操作XML 文件属性： eg:给葵花宝典的书节点增加一个属性：ISBN: “黑莓”
	public static void test7(Document document) throws Exception {
		// 拿到所有书节点
		NodeList list = document.getElementsByTagName("书");
		// 获得葵花宝典的书节点
		Node n = list.item(0);

		// 增加一个属性
		((Element) n).setAttribute("ISBN", "黑莓");

		// 保存到硬盘上
		Transformer tf = TransformerFactory.newInstance().newTransformer();
		tf.transform(new DOMSource(document), new StreamResult("src/dom/book.xml"));

	}
	}

  

<hr>

## SAX解析示例   
* 在使用DOM解析XML文档时，需要读取整个XML文档，在内存中构架代表整个DOM树的Doucment对象，再对XML文档进行操作。
	* 此种情况下，如果XML文档特别大，就会消耗计算机的大量内存，并且容易导致内存溢出
* SAX解析允许在读取文档的时候，即对文档进行操作处理，而不必等到整个文装载完  
  
### SAX_parseXML3.java  
	package sax;

	import java.util.ArrayList;
	import java.util.List;

	import javax.xml.parsers.SAXParser;
	import javax.xml.parsers.SAXParserFactory;

	import org.xml.sax.Attributes;
	import org.xml.sax.SAXException;
	import org.xml.sax.XMLReader;
	import org.xml.sax.helpers.DefaultHandler;

	import bean.Book;

	//演示封装数据到JavaBean中
	public class SAX_parseXML3 {

	public static void main(String[] args) throws Exception {
		// 创建sax解析器对象
		SAXParser sax = SAXParserFactory.newInstance().newSAXParser();
		// 获取内容读取器
		XMLReader xml = sax.getXMLReader();
		// 创建集合放置所有的书
		List<Book> list = new ArrayList<Book>();
		// 注册内容处理器
		xml.setContentHandler(new DefaultHandler() {

			String curName = "";// 记录当前是那个标签
			int index = 0;// 记录读取到那个作者
			Book book = null;

			@Override
			public void startElement(String uri, String localName, String qName, Attributes attributes)
					throws SAXException {
				if (qName.equals("书")) {
					book = new Book();
				}
				curName = qName;
			}

			@Override
			public void endElement(String uri, String localName, String qName) throws SAXException {
				if (qName.equals("书")) {
					list.add(book);
				}
				curName = null;
			}

			@Override
			public void characters(char[] ch, int start, int length) throws SAXException {
				if ("书名".equals(curName))
					book.setBookName(new String(ch, start, length));
				if ("作者".equals(curName))
					book.setBookName(new String(ch, start, length));
				if ("售价".equals(curName))
					book.setBookName(new String(ch, start, length));

			}

		});
		// 加载XML文档
		xml.parse("src/sax/book.xml");

		// 打印集合数据
		for (Book book : list) {
			System.out.println(book);
		}

	}

	}  
  
### Book.java  
	package bean;

	public class Book {

	private String bookName;

	private String author;

	private String price;

	public String getBookName() {
		return bookName;
	}

	public void setBookName(String bookName) {
		this.bookName = bookName;
	}

	public String getAuthor() {
		return author;
	}

	public void setAuthor(String author) {
		this.author = author;
	}

	public String getPrice() {
		return price;
	}

	public void setPrice(String price) {
		this.price = price;
	}

	@Override
	public String toString() {
		return "Book [bookName=" + bookName + ", author=" + author + ", price=" + price + "]";
	}

	}  
  


### Book.xml  
	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<书架>
	<书>
		<书名>葵花宝典</书名>
		<作者>安倍晋三</作者>
		<售价>100</售价>
	</书>
	<书>
		<书名>金瓶梅</书名>
		<作者>安倍晋四</作者>
		<售价>80</售价>
	</书>
	</书架>  
  
<hr>

## SAX解析   