### 一、起源

​	JavaScript诞生与1995年，主要用于处理网页中的前端验证

​	JavaScript由网景公司发明，起初命名为LiveScript，后来由于SUN公司的介入更名为JavaScript

​	为了确保不同浏览器上运行的JavaScript标准一致，所以几个公司共同定制了JS的标准，命名为ECMAScript

​	ECMAScript是一个标准，而这个标准需要各个厂商去实现，不同的浏览器厂商对于该标准会有不同的实现（Chrome的V8引擎最快）

​	一个完整JavaScript实现包含：ECMAScript，DOM，BOM

### 二、特点

 -	解释型语言（不需要编译，可直接运行）
	-	动态语言
			基于原型的面向对象

### 三、基础

```javascript
<!-- 外部js资源文件 
		<script>默认type="text/javascript"-->
	<script src="myjs.js"></script>

<!-- js代码可编写位置 -->
	<button onclick="alert('onclick--');">onClick</button>
	<a href="javascript:alert('Href--')">href</a>
	<a href="javascript:;">href</a>
```



#### 1.字面量：不可改变的值

#### 2.变量：var声明变量

#### 3.标识符：

- js中的所有可以自主命名的
- js底层保存标识符时实际采用Unicode编码

- 数据类型：字面量的类型

  - 6种：String、Number、Boolean、Null、Undefined、Object
  - 前5种为基本数据类型，Object为引用数据类型
  - typeof检查变量类型
  - NaN:not a number
  - "属性名" in 对象 ：检查该对象是否包含该属性
  - 类型转换：
     - String: toString()(Null与Undefined没有)；String()
        Number: Number()( 对于String中有数字与字符一起时，转换为NaN)
        	parseInt(),parseFloat()将String中数字进行转换，对于非String类型，都先转换String型，再转换为Number
        	Boolean:Boolean(）
        	进制
        - 1进制：0x开头
           8进制：0开头
           	2进制：0b开头

#### 4.函数

##### 	函数声明

```javascript
var fun_1 = new Function("console.log('fun_1');");
		var fun_2 = function(){
			console.log("fun_2");
		}
		function fun_3(){
			console.log("fun_3");
		}
```
##### 	立即执行函数

```javascript
(function(){
			console.log("fun_4");
		})();
```
##### 	作用范围

- 在全局中不以var声明时，都属于window属性或方法
- 变量的声明提前：使用var关键字生命的变量，会在所有的代码执行前被声明（但不会被赋值）；如果声明变量时不使用var关键字，则变量不会被提前声明
- 函数的声明提前：使用函数声明形式创建的函数function 函数(){}，会在所有代码执行前就被创建，所以可以在函数声明前来调用函数；使用函数表达式创建的函数，不会被声明提前，所以不能在声明前调用
- 在方法中的声明提前与全局类似，对于在方法中没有用var声明的变量，会以变成上一级的变量
- this：解析器在调用函数每次都会向函数内部传递一个隐含的参数，为函数执行的上下文对象，以函数的调用方式不同，this指向不同的对象：
  		 	以函数形式，指向window
  		 	以方法形式，指向调用方法的对象
- 对于函数，使用new，相当于构造函数；通过instanceof判断is-a关系;而this指向的是新创建的对象

```javascript
function Person(name,age){
			this.name = name;
			this.age = age;
			this.sayName = function(){
				console.log(this.name);
			}
		}
		var per = new Person("lov",22);
		per.sayName();
		console.log(per instanceof Person);

```
##### 	原型对象prototype

```javascript
// hasOwnProperty();判断是否有该属性
		Person.prototype.a = 10;
		//per.prototype.a = 11;实例不能操控原型
		console.log(per.__proto__);
		console.log(Person.__proto__);
		console.log(Person.prototype.a);
		console.log(per.hasOwnProperty("name"));
		console.log(per);
		var result = per.toString();
		console.log(result);
```
##### 	函数方法：call(),apply()

- 当对函数调用时都会调用函数执行
- 调用时可以将一个对象指定为第一个参数，这个对象将成为函数执行时的this
- call()方法可以将实参在对象之后依次传递
- apply()方法需要将实参封装到一个数组中统一传递

```javascript
function fun(a , b){
		 	console.log(a);
		 	console.log(b);
		 	console.log(this);
		 }
		 var obj = {name: "lov"};
		 fun.call(obj,2,3);
		 fun.apply(obj,[2,3])
```
##### 	arguments:调用函数时，浏览器传递的隐含参数

-	callee对象：对应当前正在指向的函数的对象

  ```javascript
    function fun_1(){
    	console.log(arguments.length);
    	console.log(arguments.callee);
    }
    fun_1(1,2);
  ```

	####     	JS中拥有自动的垃圾回收机制，会自动将这些垃圾对象从内存中销毁，不能手动进行垃圾回收操作

#### 5.数组：可以放任何类型的值

- forEach()：只支持IE8以上浏览器；需要一个函数作为参数，浏览器会给该回调函数传递三个参数：1、当前正在遍历的元素-2、当前正在遍历的元素的索引-3、正在遍历的数组
- sort()：默认按照Unicode编码排序；通过回调函数，返回值大于0，则元素交换位置，小于0或等于0不交换位置

```javascript
 //数组，可以放任何类型的值
var arr = new Array();
//var arr = [0,1,2];
//var arr = new Array(1,2,3);
//var arr = new Array(3);
arr[0] = 0;
arr[1] = 1;
console.log(arr);
console.log(arr.length);
//push()
var result = arr.push("values");//arr.unshift("values");
console.log(result);
console.log(arr);
//pop()
var result_1 = arr.pop();//arr.shift();
console.log(result_1);
console.log(arr);

		 /*
		 forEach():只支持IE8以上浏览器；需要一个函数作为参数，浏览器会给该回调函数传递三个参数：1、当前正在遍历的元素-2、当前正在遍历的元素的索引-3、正在遍历的数组
		  */
arr.forEach(function(value,index,obj){
	console.log(value);
	console.log(index);
	console.log(obj == arr);
});
//slice()
var result_2 = arr.slice(0, 1);
console.log(result_2);
//splice()
arr.splice(0,1, "a","b");
console.log(arr);

//concat()
var arr_1 = [3,4,5];
var result_3 = arr.concat(arr_1,arr_1,"h");
console.log(result_3);
		 //join()
console.log(arr.join("---"));
		 //reverse()
console.log(arr.reverse());
		 //sort():默认按照Unicode编码排序；通过回调函数，返回值大于0，则元素交换位置，小于0或等于0不交换位置
console.log(arr.sort());
console.log(arr.sort(function(a,b){
		 	/*if (a > b) {return 1;}
		 	else if (a < b) {return -1;}
		 	if (a == b) {return 0;}*/
		 	return a-b;
		 }));
```
#### 6.Date对象

```javascript
var d = new Date();//当前代码执行时间
console.log(d);
var d2 = new Date("12/02/2013 11:11:11");
console.log(d2);
console.log(d.getDate());//日
console.log(d.getDay());//周几（0为周日）
console.log(d.getMonth());//月（0开始）
console.log(d.getFullYear());//年
console.log(d.getTime());//时间戳，从1970.1.1 0:0:0到现在的毫秒数
console.log(Date.now());//当前时间戳

```
#### 7.Math对象

```javascript
console.log(Math.PI);
		 console.log(Math.ceil(1.1)+","+Math.floor(1.1)+","+Math.round(1.5));//向上取整，向下取整，四舍五入
console.log(Math.round(Math.random()*10+1));//生成x-y之间的随机数：Math.round(Math.random()*(y-x)+x);
console.log(Math.max(1,2,5));
console.log(Math.min(3,4,5));
console.log(Math.pow(2,3));//2的3次方
console.log(Math.sqrt(9));//开方
```
#### 8.包装类(一般不使用)

当对一些基本数据类型的值调用属性和方法时，浏览器会临时使用包装类将期转换为对象，然后在调用对象额属性与方法，调用完后，再将期转换为基本数据类型

  ```javascript
   var number = new Number(1);
  var boolea = new Boolean(true);
  var string = new String("string");
  console.log(number+","+boolea+","+string);
  var n = 1;
  n.test = 2;
  console.log(n.test);
  ```

#### 9.字符串

```javascript
var s = "hello world";
console.log(s.length); 
console.log(s[4]);
console.log(s.charAt(4));
console.log(s.charCodeAt(4));//获取字符的Unicode编码
console.log(String.fromCharCode(72));//根据字符编码获取字符
console.log(s.concat("aa"));
console.log(s.indexOf("o",2));//从指定位置查找该字符并返回索引
console.log(s.lastIndexOf("o", 5));//从后往前查找
console.log(s.slice(2, 3));
console.log(s.substring(2, 3));
console.log(s.substr( 2, 3));
s = "a,b,c,d";
console.log(s.split(",").length);
console.log(s[0].toUpperCase());
console.log(s[0].toUpperCase().toLowerCase());
s = "1b2b3b4b5b6b7h8";
console.log(s.split(/[A-z]/).length);
console.log(s.search(/b[0-9]/));
console.log(s.match(/[a-z]/gi).length);
console.log(s.replace(/[a-z]/gi,"-"));
```
#### 10.正则表达式

​    var 变量 =  new RegExp("正则表达式","匹配模式");
	 var 变量 = /正则表达式/匹配模式;
	 匹配模式：i：忽略大小写，g：全局匹配模式
	 正则表达式：
	|：表示或关系
	[]:表示或关系
	[^]：除了

    ```java
      //var reg = /a|b/i;
      var reg = /[A-z]/ ;//任意字母
      console.log(reg.test("abc"));	
    ```
    
    - 量词	
        	{n} 正好出现n次
        	{m，n} 出现m-n次
        	{m，} m次以上
        	+ 至上一个
        	* 任意个数
        	? 0或1个
        	^ 表示开头
        	$ 表示结尾
    
        ```javascript
        var reg = /a{3}/;//匹配上即可
        		reg = /a{1,3}/;//匹配上即可
        		reg = /a{3,}/;
        		reg = /a+b/;
        		reg = /^a+a$/
        		console.log(reg.test("aaa"));
        		reg = /^1[3-9][0-9]{9}$/	;//手机号匹配
        		console.log(reg.test(18628255319));
        ```
    
    - . 表示任意字符
        在正则表达式中使用\作为转义字符
        \\. 表示
    
        \w 字母、数字、_  [A-z0-9_]
        \W 除了字母、数字、_  [^A-z0-9_\]
        \d 任意数字  [0-9]
        \D 除了数字  [^0-9\]
        \s 空格
        \S 除了空格
        \b 单词边界
        \B 除了单词边界
    
        ```javascript
          		reg = /\./;
        		console.log(reg.test("b."));
        		reg = /\w/;
        		console.log(reg.test("123bc"));
        		reg = /\W/;
        		console.log(reg.test("&^*"));
        		reg = /\d/;
        		console.log(reg.test(786785));
        		reg =  /\D/;
        		console.log(reg.test("ajsbd"));
        		reg = /\s/;
        		console.log(reg.test("sbah v"));
        		reg = /\S/;
        		console.log(reg.test("  "));
        		reg = /\bhello\b/;
        		console.log(reg.test("hello li"));
        		reg = /\Bhello\B/;
        		console.log(reg.test("jsihelloli"));
        ```
    
        - 去除空格/邮箱验证
    
          ```javascript
          //var str =  prompt("print message:");//接受用户输入
          var str = '    he  llo    ';
          //console.log(str.replace(/\s/g,""));//去除所有空格
          		console.log(str.replace(/^\s+|\s+$/g,""));//去除开头与结尾
          
          var emailReg = /^\w{3,}(\.\w+)*@[A-z0-9]+(\.[A-z]{2,5}){1,2}/;//邮箱
          		console.log(emailReg.test('sb_lov@sina.com'));
          ```

#### 11.DOM

​	(Documennt Object Model)

​	Document：整个Html网页文档

​	Object：将页面中的每一个部分转换为一个对象

​	Model：用模型小时对象之间的关系

​	Node：网页中最基本的组成部分，网页中每一部分都是一个节点

​	常用节点

- 文档节点：整个html
- 元素节点：html标签
- 属性节点：元素的属性
- 文本节点：html标签中的文本内容

![节点属性](C:\Users\Administrator\Desktop\Web\JS\js\节点属性.png)

##### 	1.事件（用户与浏览器之间的交互行为）

```javascript
<button id="btn" onclick="alert('onclick');">Click</button>
```



​	文档加载顺序：自上向下顺序加载，如将script标签卸载页面的上面，在代码执行时，页面还没加载，页面没有加载DOM对象，导致script中无法获取

​	onload事件：在整个页面加载完成后才触发

```javascript
window.onload = function(){

			var btn =  document.getElementById("btn");
			console.log(btn);
			btn.onclick = function(){
				alert("message");
			};
```



##### 2.DOM查询

- document:
    		getElementById()：一个元素节点对象
    		getElementsByTagName()：一组元素节点对象
    		getElementsByName()：一组元素节点对象
- 元素节点：
    		getElementsByTagName()
    		childNodes：获取包括文本节点在内的所有节点（DOM标签间的空白也是文本节点）
    		children
    		firstChild：获取当前元素的第一个子节点（包括空白文本节点）
    		firstElementChild
    		lastChild
- 具体节点：
    		parentNode
    		previousSibling（也会获取空白的文本）
    		previousElementSibling
    		nextSibling （也会获取空白文本）
- 读取元素节点的属性：元素.属性名（读取class：元素.className）
- 获取body：
  		document.getElementsByTagName('body')[0]
  		document.body
  		documentElement
- 获取所有元素
  		document.all
  		document.getElementsByTagName('*')
- 根据元素class属性查询一组元素节点对象
  		getElementsByClassName()
- 根据css选择器查询元素
  		document.querySelector()//只返回满足条件的第一个元素
  		document.querySelectorAll()//无论满足的条件多少，都以数组形式返回

##### 3.图片切换

```css
*{
			margin: 0;
			padding: 0;
		}
		#outer{
			width: 300px;
			margin: 50px auto;
			padding: 10px;
			background-color: yellow;
		}
		img{
			width: 300px;
		}
```

```html
<div id="outer">
		
		<p id="info"></p>
		<img src="img/1.png" alt="image">

		<button id="prev">prev</button>
		<button id="next">next</button>

	</div>
```

```javascript
window.onload = function(){
    //图片切换
	var prev = document.getElementById("prev");
	var next = document.getElementById("next");
	var img = document.getElementsByTagName("img")[0];//返回的数组取第一个值
	var info = document.getElementById("info");
	var imgArr =["img/1.png","img/2.png","img/3.png","img/4.png"];
	
	//当期图片索引
	var index = 0;
	info.innerHTML = index+1+ "/"+imgArr.length;
	prev.onclick = function(){
		index--;
		if (index < 0) {index = imgArr.length-1};
		img.src = imgArr[index];
		info.innerHTML = index+1+ "/"+imgArr.length;
	};

	next.onclick = function(){
		index++;
		if (index > imgArr.length-1) {
			index = 0;
		};
		img.src = imgArr[index];
		info.innerHTML = index+1+ "/"+imgArr.length;
	};
    
}
```
##### 4.全选

```html
<form action="" method="post">
		<input type="checkbox" id="checkedAllBox">全选/全不选
		<br>
		<input type="checkbox" name="item" value="a">a
		<input type="checkbox" name="item" value="b">a
		<input type="checkbox" name="item" value="c">a
		<input type="checkbox" name="item" value="d">a
		<br>
		<input type="button" id="checkedAllBtn" value="全选">
		<input type="button" id="checkedNoBtn" value="全不选">
		<input type="button" id="checkedRevBtn" value="反选">
		<input type="button" id="sendBtn" value="提交">

	</form>
```

```javascript
var items = document.getElementsByName("item");
		
		//全选
		var checkedAllBtn = document.getElementById("checkedAllBtn");
		checkedAllBtn.onclick = function(){

			for(var i=0;i<items.length;i++){
				items[i].checked = true;
			}
			checkedAllBox.checked = true;
		};

		//全不选
		var checkedNoBtn = document.getElementById("checkedNoBtn");
		checkedNoBtn.onclick = function(){
			
			for(var i=0;i<items.length;i++){
				items[i].checked = false;
			}
			checkedAllBox.checked = false;
		};

		//反选
		var checkedRevBtn = document.getElementById("checkedRevBtn");
		checkedRevBtn.onclick = function(){
			checkedAllBox.checked = true;
			for(var i=0;i<items.length;i++){
				items[i].checked = !items[i].checked;

				if (!items[i].checked) {
					checkedAllBox.checked = false;
				};
			}
		};

		//发送
		var sendBtn = document.getElementById("sendBtn");
		sendBtn.onclick = function(){

			for(var i=0;i<items.length;i++){
				if (items[i].checked) {
					console.log(items[i].value);
				};
			};
		};

		//全选/全不选
		var checkedAllBox = document.getElementById("checkedAllBox");
		checkedAllBox.onclick = function(){
			console.log(this +"this === checkedAllBox");

			for(var i=0;i<items.length;i++){
				items[i].checked = this.checked;
			};
		};

		//item事件
		for(var i=0;i<items.length ;i++){
			items[i].onclick = function(){
				checkedAllBox.checked = true;
				for(var j=0;j<items.length;j++){
					if (!items[j].checked) {
						checkedAllBox.checked = false;
						break;
					}
				}
			};
		}
```
##### 5.DOM增删改

- document.createElement():用于创建元素节点对象，标签名作为参数

- document.createTextNode():创建文本节点对象，文本内容为参数

- appendChild():向父节点添加一个新的子节点（父节点.appendChild(子节点)）

- insertBefore():(父节点.insertBefore(新节点,旧节点))

- replaceChild():(父节点.replaceChild(新节点,旧节点))

- removeChild():(父节点.removeChild(子节点))---子节点.parentNode.removeChild(子节点)

    ```css
    *{
    			margin: 0;
    		}
    		#outer{
    			width: 500px;
    			margin: 50px auto;
    			padding: 10px;
    			background-color: #D3D3D3;
    			text-align: center;
    		}
    		
    		form{
    			margin-top: 200px;
    			
    			text-align: center;
    		}
    		label{
    			display: inline-block;
    			width: 60px;
    		}
    		 table{
                    border:0;
                    cellspacing:0;
                    cellpadding:0;
                    display: inline-block;
                    margin: 0 auto;
                }
                 
                table tr{
                    border:none;
                    padding:0;
                    margin:0;
                }
     
                table td,th{
                    border-bottom:2px solid #778899;
                    margin:0;
                    padding:7px;
                }
     
                table td:hover{
                    background:#eee;
                    cursor:pointer;
                }
    		a{
    			text-decoration: none;
    		}
    		a:link{
    			color: #778899;
    		}
    		a:active{	
    			color: #838B83	;
    		}a:hover{
    			color: #2F4F4F;
    		}
    ```

    ```html
    <div id="outer">
    	<table id="employeeTable" cellspacing="0" cellpadding="0">
    		<tr>
    			<th>Name</th>
    			<th>Email</th>
    			<th>Salary</th>
    			<th>&nbsp</th>
    		</tr>
    		<tr>
    			<td>Lov-1</td>
    			<td>lov1@sina.com</td>
    			<td>10000</td>
    			<td><a href="javascript: ;">Delete</a></td>
    		</tr>
    		<tr>
    			<td>Lov-2</td>
    			<td>lov2@sina.com</td>
    			<td>10000</td>
    			<td><a href="deleteEmp?id=002">Delete</a></td>
    		</tr>
    		<tr>
    			<td>Lov-3</td>
    			<td>lov3@sina.com</td>
    			<td>10000</td>
    			<td><a href="deleteEmp?id=003">Delete</a></td>
    		</tr>
    
    	</table>
    
    	<form action="">
    		<label for="name">Name:</label><input id="name" type="text"><br>
    		<label for="email">Email:</label><input id="email" type="text"><br>
    		<label for="salary">Salary:</label><input id="salary" type="text">
    		<br>
    		<button id="submit">submit</button>
    	</form>
    
    </div>
    ```

    ```javascript
    /*
    	document.createElement():用于创建元素节点对象，标签名作为参数
    	document.createTextNode():创建文本节点对象，文本内容为参数
    	appendChild():向父节点添加一个新的子节点（父节点.appendChild(子节点)）
    	insertBefore():(父节点.insertBefore(新节点,旧节点))
    	replaceChild():(父节点.replaceChild(新节点,旧节点))
    	removeChild():(父节点.removeChild(子节点))---子节点.parentNode.removeChild(子节点)
    
     */
     	var del = function(){
     				var tr = this.parentNode.parentNode;
    
    
     				//弹出带有确认取消的提示框
     				var flag = confirm("delete--"+tr.getElementsByTagName("td")[0].innerText);
     				if (flag) {
     					//this是点击的超链接
     					tr.remove();
     				}
    
     				//超链接默认行为跳转页面，通过返回false取消默认行为
     				return false;
     			};
    
     	window.onload = function(){
    
     		var allA = document.getElementsByTagName("a");
    
     		for(var i = 0; i<allA.length; i++){
     			/*
     			for循环会在页面加载完成后立即执行，而响应函数在超链接点击时才执行
     			 */
     			allA[i].onclick = del;
     		}
    
     		var submit = document.getElementById("submit");
     		submit.onclick = function(){
     			var name = document.getElementById("name").value;
     			var email = document.getElementById("email").value;
     			var salary = document.getElementById("salary").value;
    
     			var table = document.getElementById("employeeTable");
     			var tr = document.createElement("tr");
     			
    
     			tr.innerHTML="<td>"+name+"</td>"+
     						"<td>"+email+"</td>"+
     						"<td>"+salary+"</td>"+
     						"<td>"+'<a href="javascript: ;">Delete</a>'+"</td>";
     			
    
     			
     			table.appendChild(tr);
    
     			tr.lastChild.firstChild.onclick = del;
    
     				
     				return false;
     			};
    
     		
    
     		
     	}
    ```

##### 6.CSS操作

- 修改元素的样式：元素.style.样式名 = 样式值（对于含有-的样式名，以驼峰方式）：通过该方式修改的css为内联样式

- 获取元素当前显示的样式

     1. 元素.currentStyle.样式名（当前没有设置样式，读取默认值；该方式只有ie支持）

     2. getComputedStyle()(window的方法)：需要两个参数，‘获取样式的元素’，‘可以传一个伪元素，一般传null’；返回一个对象，该对象封装了当前元素对应的样式；对应没有设置的，会读取真实值;不支持ie8

        ```javascript
        兼容问题的解决思路
        
        	if(window.getComputedStyle){
        
        				getComputedStyle
        
        			}else{	currentStyle	}
        ```

- clientWidth,clientHeight：获取元素的可见宽度与高度（包括内边距）；返回数字，不带px；该属性为只读

- offsetParent：获取离当前元素最近的开启了定位的元素；如果没有，返回body

- offsetLeft：当前元素相对其定位元素的水平偏移量

- offsetTop：当前元素相对其定位元素的垂直偏移量

- scrollWidth，scrollHeight：可以获取元素整个滚动区域的宽度和高度

- scrollLeft，scrollTop：可以获取水平/垂直滚动条滚动的距离

- scrollHeight-scrollTop == clientHeight：垂直滚动条到底

- scrollWidth-scrollLeft == clientWidth：水平滚动条到底

    ```css
    #box{
    			/* width: 200px; */
    			height: 200px;
    			background: red;
    		}
    
    		#box1{
    			width: 100px;
    			height: 400px;
    			background-color: red;
    		}
    
    		#a{
    			width: 200px;
    			height: 300px;
    			/* overflow: hidden; */
    			overflow: auto;
    		}
    		#info{
    			width: 300px;
    			height: 500px;
    			background-color: yellow;
    			overflow: auto;
    		}
    ```

    ```html
    <button id="btn1">btn1</button>
    	<button id="btn2">btn2</button>
    	<div id="box"></div>
    
    	<button id="btn01">click</button>
    	<br>
    	<div id="i" style="position:relative;">
    		<div id="a">
    			<div id="box1"></div>		
    		</div>
    	
    	</div>
    	
    	<div>
    		<h3>welcome</h3>
    		<p id="info">……</p>
    		<input type="checkbox"	disabled="true">
    		<input type="submit" value="submit" disabled="true" >
    	</div>
    ```

    ```javascript
    window.onload = function(){
    		var btn1 = document.getElementById("btn1");
    		var btn2 = document.getElementById("btn2");
    		var box = document.getElementById("box");
    
    		/*
    			JS修改元素的样式：元素.style.样式名 = 样式值
    			（对于含有-的样式名，以驼峰方式）
    			通过该方式修改的css为内联样式
    		 */
    		btn1.onclick = function(){
    			box.style.width = "300px";
    			box.style.height = "300px";
    			box.style.backgroundColor = "yellow";
    		}
    		/*
    			JS读取元素的样式：元素.style.样式名
    			通过该方式读取的css为内联样式
    
    			获取元素当前显示的样式
    				元素.currentStyle.样式名（当前没有设置样式，读取默认值；该方式只有ie支持）
    				getComputedStyle()(window的方法)：需要两个参数，‘获取样式的元素’，‘可以传一个伪元素，一般传null’；返回一个对象，该对象封装了当前元素对应的样式；对应没有设置的，会读取真实值;不支持ie8
    	
    			兼容问题的解决思路
    			if(window.getComputedStyle){
    				getComputedStyle
    			}else{	currentStyle	}
    		 */
    		btn2.onclick = function(){
    			//alert(box.style.width+"--"+box.style.height)
    			alert(getComputedStyle(box,null).width);
    		}
    
    		var box01 = document.getElementById("box1");
    		var btn01 = document.getElementById("btn01");
    
    		btn01.onclick = function(){
    			/*
    				clientWidth,clientHeight
    					获取元素的可见宽度与高度（包括内边距）
    					返回数字，不带px；该属性为只读
    
    			 */
    			//alert(box01.clientWidth);
    			/*
    				offsetParent
    					获取离当前元素最近的开启了定位的元素；如果没有，返回body
    			 */
    			//var op = box01.offsetParent;
    			//alert(op.id);
    			/*
    				offsetLeft
    					当前元素相对其定位元素的水平偏移量
    				offsetTop
    					当前元素相对其定位元素的垂直偏移量
    			 */
    			//alert(box01.offsetLeft);
    			/*
    				scrollWidth
    				scrollHeight
    					可以获取元素整个滚动区域的宽度和高度
    				scrollLeft
    				scrollTop
    					可以获取水平/垂直滚动条滚动的距离
    			 */
    			var a = document.getElementById("a");
    			//alert(a.scrollHeight);
    			//alert(a.scrollTop);
    			/*
    				scrollHeight-scrollTop == clientHeight
    				垂直滚动条到底
    			 */
    			/*
    				scrollWidth-scrollLeft == clientWidth
    				水平滚动条到底
    			 */
    			alert(a.scrollHeight-a.scrollTop == a.clientHeight);
    
    		}
    
    		var info = document.getElementById("info");
    		var inputs = document.getElementsByTagName("input");
    
    		info.onscroll = function(){
    			if(info.scrollHeight - info.scrollTop == info.clientHeight){
    				inputs[0].disabled = false;
    			}
    		}
    
    		inputs[0].onclick = function(){
    			if (this.checked) {inputs[1].disabled = false;}
    			else
    			{inputs[1].disabled = true;}
    			
    		}
    
    	}
    ```

##### 7.事件对象

​	当事件的响应函数被触发时，浏览器每次都会将一个事件对象作为实参传递给响应函数

##### 8.事件的冒泡（Bubble）

​	指事件的向上传导，当后代元素上的事件触发，其祖先的相同事件也会触发；可以取消冒泡

##### 9.事件的委托

  	 指将事件统一绑定给元素的共同的祖先元素，当后代元素事件触发时，会冒泡传到祖先元素，再通过祖先元素的响应函数处理事件

```css
  #box1{
  			width: 300px;
  			height: 200px;
  			background-color: yellow;
  		}
  		#box2{
  
  			width: 300px;
  			height: 80px;
  			background-color: yellow;
  			margin-top: 50px;
  		}
  		#box3{
  			width: 50px;
  			height: 50px;
  			background-color: red;
  			position: absolute;
  		}
  		#box4{
  			width: 400px;
  			height: 200px;
  			background-color: blue;
  			
  		}
  		#box5{
  			margin-top: 60px;
  		}
```

```html
  <div id="box1">
  	</div>
  	<div id="box2"></div>
  	
  	<div id="box4"></div>
  	<div id="box3">
  		
  	</div>	
  
  	<div id="box5">
  		
  		<button id="new">NEW</button>
  		<ol id="ol">
  			
  			<li><a href="javascript:;" class="link">click</a></li>
  			<li><a href="javascript:;" class="link">click</a></li>
  			<li><a href="javascript:;" class="link">click</a></li>
  		</ol>
  	</div>
```

```javascript
  var box1 = document.getElementById("box1");
  	var box2 = document.getElementById("box2");
  
  	/*
  		当事件的响应函数被触发时，浏览器每次都会将一个事件对象作为实参传递给响应函数
  	 */
  	box1.onmousemove = function(event){
  
  		/*
  			ie8及以下，将事件对象作为window对象的属性保存
  		 */
  		event = event || window.event;
  
  		/*
  			clientX：获取鼠标指针的水平坐标
  			clientY：获取鼠标指针的垂直坐标
  			鼠标在当前可见窗口的坐标
  		 */
  		var x = event.clientX;
  		var y = event.clientY;
  
  		box2.innerHTML = x + '+'+y;
  	}
  
  	var box3 = document.getElementById("box3");
  
  	//
  	document.onmousemove = function(event){
  
  		event = event || window.event;
  
  		/*
  		获取页面滚动条距离
  			解决兼容：
  
  		var st = document.body.scrollTop || document.documentElement.scrollTop;
  		var sl = document.body.scrollLeft || document.documentElement.scrollLeft;
  
  		var left = event.clientX;
  		var top = event.clientY;
  
  		box3.style.top = top +st +"px";
  		box3.style.left = left  +sl+"px";
  */
  		//pageX/pageY : 获取鼠标相对当前页面的坐标 ，ie8不支持
  		var left = event.pageX;
  		var top = event.pageY;
  
  		//box3.style.top = top  +"px";
  		//box3.style.left = left  +"px";
  
  
  	}
  
  	/*
  			事件的冒泡（Bubble）
  				指事件的向上传导，当后代元素上的事件触发，其祖先的相同事件也会触发；可以取消冒泡
  		 */
  		
  	 var box4 = document.getElementById("box4");
  	 box4.onmousemove = function(event){
  
  		 	event = event || window.event;
  
  		 	//取消冒泡
  		 	event.cancelBubble = true;
  	 }
  
  
  	 var newl = document.getElementById("new");
  	 var ol = document.getElementById("ol");
  
  	 /*
  	 	事件的委托
  	 		指将事件统一绑定给元素的共同的祖先元素，当后代元素事件触发时，会冒泡传到祖先元素，再通过祖先元素的响应函数处理事件
  	  */
  	 newl.onclick = function(){
  
  	 	
  	 	var li = document.createElement("li");
  	 	li.innerHTML = '<a href="javascript:;" class="link">click</a>';
  
  	 	ol.appendChild(li);
  	 }
  
  	 ol.onclick = function(event){
  	 	event = event || window.event;
  	 	//target：event中的target表示触发事件的对象
  	 	if (event.target.className == 'link') {
  	 		alert("message");
  	 	};
  	 }
```
##### 10.事件的传播

三个阶段

​	1.捕获阶段
		由最外层的祖先元素，向目标元素进行事件的捕获，但是默认不触发事件
	2.目标阶段
		事件捕获到目标元素，捕获结束开始在目标元素上触发事件
	3.冒泡阶段
		由目标向祖先元素传递，依次触发事件

##### 11.元素绑定多个响应事件

```html
<button id="bt">click</button>
```

```javascript
window.onload = function(){

		var bt= document.getElementById("bt");

		/*
			addEventListener()
				为元素绑定响应事件
				参数
					事件的字符串，不要on
					回调函数
					是否在捕获阶段触发事件，需要一个boolean值，一般为false
				可以为同一个元素的相同事件绑定多个响应函数，函数按绑定顺序执行
				其中的this是绑定事件的对象
				不兼容ie8
		 */
	/*	bt.addEventListener("click", function(){
			alert(1);
		}, false);
		bt.addEventListener("click", function(){
			alert(2);
		}, false);*/
		bind(bt, "click", function(event) {
			alert(this);
		});

		/*
			attachEvent()
				ie8中使用
				参数：
					事件的字符串，要on
					回调函数
				执行顺序与绑定顺序相反
				其中this是window
		 */
		/*bt.attachEvent("onclick", function(){
			alert(1);
		})
		bt.attachEvent("onclick", function(){
			alert(2);
		})
*/
	//兼容：
	//	obj 绑定事件的对象
	//	eventStr 事件的字符串
	//	callback 回调函数
	function bind(obj , eventStr ,callback){
		if(obj.addEventListener){
			obj.addEventListener(eventStr,callback,false);
		}else{
			/*
			 	this是谁由调用方式决定
				callback.call(obj)

			 */
			obj.attachEvent("on"+eventStr , function(){
				//在匿名函数中调用回调函数
				callback.call(obj);
			})
		}
	}

	
	}
```

##### 12.鼠标事件

```html	
<div id="box1"></div>
	<div id="box2"></div>
	<div id="box3"></div>
```

```css
#box1{
			width: 100px;
			height: 100px;
			background-color: red;
			position: absolute;
		}
		
		#box3{
			
			margin-left: 300px;
			width: 100px;
			height: 100px;
			background-color: yellow;
			
		}
```

```javascript
var box1 = document.getElementById("box1");
		//按下
		box1.onmousedown = function(event){
			event = event || window.event;
			//鼠标偏移量
			var l = event.clientX - box1.offsetLeft;
			var t = event.clientY - box1.offsetTop;

			//拖拽
			document.onmousemove = function(event){
				event = event || window.event;

				var left = event.clientX;
				var top = event.clientY;

				box1.style.left = left-l+"px";
				box1.style.top = top -t+"px";
			}

			//松手
			document.onmouseup = function(){
				document.onmousemove = null;

				document.onmouseup = null;
			}

			//取消全选时，没有绑定事件的元素的拖拽行为
			return false;
		}


		var box3 = document.getElementById("box3");

		//鼠标滚动事件
		box3.onmousewheel = function(event){
			event = event || window.event;
			//正值向上滚，负值向下
			// alert(event.wheelDelta);
			if (event.wheelDelta >0 ) {
				box3.style.height = box3.clientHeight - 10+'px';
			}else{
				box3.style.height = box3.clientHeight + 10+'px';
			}


			//取消浏览器默认行为
			//通过addEventListener()绑定的响应函数，取消默认行为需要
			//event.preventDefault();
			return false;
		}
```

##### 13.键盘事件

```html
<input id="inp" type="text">
	<div id="box4"></div>
```

```css
#box4{
			
			
			width: 100px;
			height: 100px;
			background-color: green;
			position: absolute;
		}
```

```javascript

		/*
			键盘事件
				onkeydown
					如果一直按着某个键，则一直触发
					连续触发时，第一次与第二次间隔稍微长，这种设计为了防止误操作
				onkeyup

		 */
		inp.onkeydown = function(event){
			/*
				通过keyCode获取按键编码
				其他属性
					altKey
					ctrlKey
					shiftKey
			 */
			if (event.keyCode === 89 && event.ctrlKey) {
				console.log("onkeydown");
			}
			if (event.keyCode >= 48 && event.keyCode <= 57) {
				//输入数字时，取消默认的输出行为
				return false;
			};
		}

		var box4 = document.getElementById("box4");
		document.onkeydown = function(event){
			switch(event.keyCode){
				case 37:
					// alert("message");
					box4.style.left = box4.offsetLeft-10+'px';
					break;
				case 39:
					box4.style.left = box4.offsetLeft+10+'px';
					break;
				case 38:
					box4.style.left = box4.offsetTop-10+'px';
					break;
				case 40:
					box4.style.left = box4.offsetTop+10+'px';
					break;

			}

		}
```

#### 12.BOM

​	**Window**
		代表整个浏览器窗口，同时window也是网页中的全局对象
	**Navigator**
		代表当前浏览器的信息，通过该对象可以识别不同的浏览器
	**Location**
		代表当前浏览器的地址栏信息，通过Location可以地址栏信息，操作浏览器跳转页面
	**History**
		代表浏览器的历史记录，可以通过该对象操作浏览器的历史记录（由于隐私问题，该对象不能获取具体历史记录，只能操作浏览器想前或向后翻页，而且操作只在当次访问有效）
	**Screen**
		代表用户的屏幕信息，通过该对象获取用户的显示器的相关信息

​	*这些BOM对象在浏览器中都是作为window的属性保存，可以通过**window**对象调用或直接使用*

##### 	1.Navigator

​		由于历史原因，navigator对象中的大部分属性都不能用来识别浏览器了，一般只使用userAgent来判断浏览器信息
		userAgent是一个字符串，包含描述浏览器信息的内容，不同浏览器有不同的userAgent

```javascript
	console.log(navigator);
	console.log(navigator.appName);
	console.log(navigator.userAgent);

	if ((/chrome/i).test(navigator.userAgent)) {
		console.log('YES');
	};

```

##### 	2.History

​		length：获取当前访问的链接数量
		console.log(history.length);
		back()：退后上一个页面，与浏览器返回一样
		forward()：跳转下一个页面，与浏览器前进一样
		go()：跳转到指定页面
			整数作为参数：
				1：向前跳转一个页面
				2：向前跳转两个页面
				-1：向后跳转一个页面
				-2：向后跳转两个页面
			history.go(1);

##### 	3.Location

```javascript
	console.log(location);
	 // 直接修改会直接跳转到相应页面
	  //location = "http://www.baidu.com";
	  /*
	  	assign()
	  		跳转到其他页面
	   */
	  //location.assign('http://baidu.com')
	  /*
	  	reload()
	  		用于重新加载当前页面，刷新
	  		在方法中传递true为参数，则强制清空缓存刷新
	   */
	  //location.reload(true);
	  /*
	  	replace()
	  		使用新页面替换当前页面
	   */
	  //location.replace("http://www.baidu.com")
	  
	  /*
```

#### 13.定时/延时调用

```javascript
/*
	  	setInterval()
	  		定时调用，将一个函数每隔一段时间执行一次
	  		参数：
	  			回调函数
	  			间隔时间，毫秒
	  		返回值：
	  			number数据
	  	clearInterval()
	  		关闭指定定时器
	   */
	var h = document.getElementById("h");
	var num = 1;
	var timer = setInterval(function(){
		h.innerHTML = num++;
		if (num == 11) {
			clearInterval(timer);
		};
	},1000);  	

	/*
		延时调用
	 */
	var dtimer =setTimeout(function(){
		console.log(num++);
	}, 3000);

	// clearTimeout(timer);
```

#### 14.类操作

```css
.b1{
		width: 100px;
		height: 100px;
		background-color: red;
	}
	.b2{
		/* width: 200px; */
		height: 200px;
		background-color: green;
	}
```

```html
<button id="btn1">btn1</button>
	<button id="btn2">btn2</button>
	<br>
	<br>
	<div id="box1" class="b1"></div>
```

```javascript
/*
		class操作
	 */
	window.onload = function(){
		var btn1 = document.getElementById("btn1");
		var btn2 = document.getElementById("btn2");

		var box1 = document.getElementById("box1");

		btn1.onclick = function(){
			/*
				通过style属性修改的样式，没修改一次，浏览器就会重新渲染一次页面

			 */
			// box1.style.width = "200px";
			/*
				修改class属性，页面只重新渲染一次
			 */
			// box1.className += " b2";
			
			
			addClass(box1,"b2");
		}

		btn2.onclick = function(){
			//removeClass(box1,"b2");
			toggleClass(box1,"b2");
		}

		//添加class
		function addClass(obj, cn){
			if(!hasClass(obj,cn)){

				obj.className += " "+cn;
			}
		}
		// 判断是否有该class
		function hasClass(obj , cn ){

			var reg = new RegExp("\\b"+cn+"\\b");
			return reg.test(obj.className);

		}
		//移除class
		function removeClass(obj , cn){
			var reg = new RegExp("\\b"+cn+"\\b");
			obj.className = obj.className.replace(reg, "");

		}
		//切换
		function toggleClass(obj , cn){
			if (hasClass(obj,cn)) {

			removeClass(obj,cn);
				
			}else{
				
			addClass(obj,cn);
			}
		}
    }
```

#### 15.JSON

```javascript
/*
			JSON
				JavaScript Object Notaion Js对象表达法
				JSON字符串中的属性名必须加双引号
				JSON分类：
					对象{}
					数组[]
				JSON中的值：
					字符串
					数值
					布尔值
					nul
					对象
					数组
		 */
		var obj = '{"name":"lov","age":20,"gender":"man"}';
		var obj2 = {"name":"lov","age":20,"gender":"man"};
		/*
			json :js对象
				JSON.parse()
					将JSON字符串转换为js对象
				JSON.stringify()
					将js对象转换为JSON字符串
		 */
		console.log(JSON.parse(obj).name);
		console.log(JSON.stringify(obj2));
		/*
			eval()
				执行一段字符串形式的js代码，并将执行结果返回
				使用eval()执行的字符串中如有{}，会将{}当成代码块
				如果不希望以代码块解析，在字符串加()
				该函数功能很强大，但执行性能差，并有安全隐患	
		 */
		eval("console.log('eval')");

		console.log(eval("("+obj+")"));
```

### DEMO:

​	定时器：javascript_11.html

​	轮播：javascript_12.html