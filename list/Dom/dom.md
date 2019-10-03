### 1 JavaScript组成部分

![](assets/img/01.jpg)

+ ECMAScript 核心语法
+ BOM   浏览器对象模型
+ DOM  文档对象模型

**注意：** 

> ① ECMAScript是独立于浏览器平台的。还可以运行在NodeJS平台
>
> ② DOM其实是属于BOM的一部分。DOM在BOM占的比重大，而且是重点。
>
> ③ DOM和BOM是浏览器提供的，只有在浏览器上才可以操作DOM和BOM。



### 2 webAPI介绍

![](media/box.jpg)

- API：（Application Programming Interface,应用程序编程接口）， **工具**。
- web API：操作浏览器 和 网页的一套**==工具库== ** （ **BOM 和 DOM** ）。



### 3 文档树

DOM，文档对象模型，又称为**文档树模型**。 

浏览器在加载页面时， **会把html文档解析成一系列的对象**。再由这些对象组成 **树状结构**。存入内存。

这些对象对外都提供了 **属性和方法**。我们可以 **通过调用对象的属性和方法来操作网页**。

![](assets/img/02.jpg)



**注意**： 树状结构上的每一个都是对象，也可叫做==节点对象==。 

**节点对象的分类：** ==文档对象==、==元素对象==、属性对象、文本对象 

**小结：**

> 文档树：本质就是浏览器把**文档**、**文档中标签**、标签属性以及标签文本转换成对象，按照嵌套关系以**树状结构** 存放这一组对象，并放入内存中。




### 3 获取元素的方式

- 获取方式

  - 1 document.getElementById('标签的id值');   

    ```javascript
    // 根据标签的id值，获取【单个节点对象】。 返回单个节点对象
    var mainNode = document.getElementById('main');
    console.dir(mainNode);  // 找到返回一个节点对象，找不到返回null

    // 注意：标签的id值，一般都是唯一的。若有重复的id值，则仅仅获取第一个。
    // id值的命名规范：由数字、字母、_、$组合，不可以数字开头。
    ```

    ​

  - 2 document.getElementsByTagName('标签名');  【推荐使用】**

    ```javascript
    // 根据标签名获取【一组节点对象】。返回一个伪数组
    var liNodes = document.getElementsByTagName('li');
    console.dir(liNodes);  // 找到返回一个伪数组，伪数组中存放了多个节点对象。找不到返回空的伪数组
    ```
     ​

  - 3 document.querySelector('选择器'); 【不考虑IE低版本，移动端，推荐使用】**

  ```javascript
  // 根据选择器获取【单个节点对象】。返回一个节点对象
  var zzNodes = document.querySelector('ul li.active');
  console.dir(zzNodes);  //找到返回一个节点对象，找不到返回null

  // 注意：该方式有兼容性问题。在IE低版本（IE8以下有兼容性问题）
  ```

  - 4 document.querySelectorAll('选择器'); 【不考虑IE低版本，移动端，推荐使用】**

  ```javascript
  // 根据标签的name值获取【一组节点对象】。返回一个伪数组
  var zzNodes = document.querySelectorAll('ul li.active');
  console.log(zzNodes);  //找到返回一个伪数组，伪数组中存放了多个节点对象。找不到返回空伪数组

  // 注意：该方式有兼容性问题。在IE低版本（IE8以下有兼容性问题）
  ```

  - 5 document.getElementsByClassName('标签的类名');【了解】

  ```javascript
  // 根据标签的类名获取一组节点对象。返回一个伪数组
  var boxNodes = document.getElementsByTagName('box');
  console.dir(liNodes);  // 找到返回一个伪数组，伪数组中存放了多个节点对象。找不到返回空伪数组

  // 注意：该方式有兼容性问题。在IE低版本（IE8及以下有兼容性问题）会报错
  ```

  - 6 document.getElementsByName('标签的name值');【了解】

  ```javascript
  // 根据标签的name值获取一组节点对象。返回一个伪数组
  var zzNodes = document.getElementsByName('zz');
  console.dir(zzNodes);  // 找到返回一个伪数组，伪数组中存放了多个节点对象。找不到返回空伪数组

  // 注意：该方式有兼容性问题。在IE低版本（IE10以下有兼容性问题）
  ```


### 4 什么是事件

​		我们和网页之间的交互，可以理解为何网页之间的一些行为。常见行为有鼠标点击、鼠标的移动、鼠标的移入和移出、键盘控制等等。这些行为，在我们DOM中被称之为事件。

​	总而言之， **事件就是被JavaScipt侦测到的行为。**
​	事件的目的：就是 **实现网页交互**。



#### 4.1 事件三要素

- 事件源（事件目标）：触发事件的元素
- 事件类型：哪种交互方式（鼠标点击、鼠标移入、鼠标离开等）
- 事件处理程序：事件触发后的结果，也就是事件发生后要执行的程序， 用**函数**表示



#### 4.2 给元素注册事件

- 语法

  **事件源.事件类型 = 事件处理程序;**

- 代码

  ```html
  <input type="button" vlaue="按钮" id="btn">
  <script>
  	// 需求：点击按钮，弹出'hello'
  	// ① 获取事件目标
  	var btn = document.getElementById('btn');
  	// ② 给事件目标绑定点击事件
  	btn.onclick = function(){
        alert('hello');
  	};
  </script>
  ```

  ![](assets/img/03.jpg) 

  ​

- 事件处理程序的本质：就是元素对象的一个方法。当事件触发时，方法会被调用。



#### 4.3 事件类型 

==onclick==  点击事件

其他事件可以参考手册
![](assets/img/event.png)



### 5 操作元素对象的基本属性

#### 5.1 元素对象属性分类

- 非表单属性
  - id
  - title
  - href
  - src
  - ==className== 
  - ==innerHTML== 
  - ==innerText== 
- 表单属性（明天讲）



#### 5.2 操作元素对象属性的语法

- 获取： **==元素.属性名==** ;

  ```javascript
  var div = document.getElementById('box');
  console.log(div.title);  // 获取属性对应的值 
  ```

- 设置：**==元素.属性名 = 值==;** 

  ```javascript
  var div = document.getElementById('box'); // 获取元素
  console.log(div.title);  // 设置之前，获取属性对应的值 
  div.title = 'hello';     // 设置（更改）这个div的title属性的值
  console.log(div.title);  // 设置之后，获取属性对应的值 
  ```



#### 5.3 操作非表单元素对象属性

- **元素对象.calssName**

  - 作用：操作元素的类名。可以通过类名管理或切换元素的样式。

  - 代码：

    ```javascript
    // 获取元素
    var div = document.getElementById('box'); 
    // 获取元素的类名
    console.log(div.className);  
    // 设置元素的类名
    div.className = 'dv1 dv2';   // 注意：类名可以有多个，多个类名之间用空格分隔
    // 获取元素的类名
    console.log(div.className);  
    ```

- **元素对象.innerHTML**

  - 作用：操作元素的内容

  - 代码：

    ```javascript
    // 获取元素
    var div = document.getElementById('box'); 
    // 获取元素内部的内容，若元素内部有其他标签，获取则包含内部的标签和文本
    console.log(div.innerHTML); 
    // 设置元素内部的内容，若设置的元素内部有其他标签，则元素内部标签会被浏览器解析
    div.innerHTML = '<h1>标题</h1>';
    // 获取元素内部的内容
    console.log(div.innerHTML); 
    ```

- **元素对象.innerText**

  - 作用：操作元素的内容

  - 代码：

    ```javascript
    // 获取元素
    var div = document.getElementById('box'); 
    // 获取元素内部的内容，若元素内部有其他标签，获取的仅仅是文本，不包含内部标签
    console.log(div.innerText); 
    // 设置元素内部的内容，若设置的元素内部有其他标签，则元素内部标签不会被解析，标签会被转义
    div.innerText = '<h1>标题</h1>';
    // 获取元素内部的内容
    console.log(div.innerText);  // 获取元素的类名
    ```



### 6：innerText 和 textContent的区别

innerText 是非标准的属性，textContent是标准的属性

+ 相同点：都是操作元素的文本
+ 不同点：
  + innerText 对IE的兼容性较好 
  + textContent虽然作为标准方法但是只支持IE8+以上的浏览器 
  + 最新的浏览器，两个都可以使用



### 7 事件处理程序中的this

+ 事件处理程序中的this代表的是事件源（将来触发哪个元素，就代表那个元素）


### 8 操作表单元素对象的属性【重点】

- **元素对象.value**

  - 作用：操作表单元素的值【所有表单元素都可以用】

  - 代码：

    ```html
    <input type="text" id="userName">
    <script>
    	// 获取文本框元素
    	var userName = document.getElementById('userName');
    	// 获取文本框的内容
    	console.log(userName.value);  // ''
    	// 【设置文本框的内容】
    	userName.value = 'admin';
    	// 【获取文本框的内容】
    	console.log(userName.value);  // 'admin'
    </script> 
    ```

- **元素对象.checked**

  - 作用：操作表单元素 **是否**选中【针对 单选框 和 多选框 】

  - 代码：

    ```html
    喜欢足球：<input type="checkbox" id="ck">
    <script>
    	// 获取多选框元素
    	var ck = document.getElementById('ck');
    	// 获取多选框选中状态
    	console.log(ck.checked);   // false 未选中
    	// 【设置多选框选中状态为 选中】
    	ck.checked = true;
    	// 【获取多选框的选中状态】
    	console.log(ck.checked);   // true  选中
    </script>    	
    ```

- **元素对象.disabled**

  - 作用：操作表单元素 **是否**禁用【针对按钮】

  - 代码：

    ```html
    <input type="button" id="btn"value='按钮'>
    <script>
    	// 获取按钮元素
    	var btn = document.getElementById('btn');
    	// 获取按钮是否可禁用状态
    	console.log(btn.disabled);   // false 没有禁用
    	// 【设置按钮是否可禁用状态 禁用】
    	btn.disabled = true;
    	// 【获取按钮是否可禁用状态】
    	console.log(ck.checked);   // true  禁用了
    </script> 
    ```

- **元素对象.selected**

  - 作用：操作下拉框选项**是否**选中【针对下拉框】

  - 代码：

    ```html
    <select id='userName'>
    	<!-- 默认选中张三 -->
    	<option value="张三">张三</option>
    	<option value="李四">李四</option>
    	<option value="王五">王五</option>
    	<option value="赵六">赵六</option>
    </select>
    <script>
    	// 获取下拉框 和 一组option项
    	var userName = document.getElementById('userName');
    	var options = document.getElementsByTagName('option');
    	// 获取下拉框选中的内容
    	console.log(userName.value);
    	// 获取李四是否被选中 【李四对应的索引时候1】
    	console.log(options[1].selected);  // false 李四没有被选中
    	// 设置李四被选中
    	options[1].selected = true;  
    	// 获取下拉框选中的内容
    	console.log(userName.value);
    	// 获取李四是否被选中 【李四对应的索引时候1】
    	console.log(options[1].selected);  // true 李四被选中
    </script>
    ```


### 9 操作元素的样式【重点】

- 通过元素的style属性操作

  ```javascript
  var box = document.getElementById('box');
  box.style.width = '100px';
  box.style.height = '100px';
  box.style.backgroundColor = 'red';   // css→ background-color     js→ backgroundColor
  ```

  **注意：通过样式属性设置宽高、位置的属性类型是字符串，需要加上px。**

  ​

- 通过设置元素的className属性操作

  ```javascript
  var box = document.getElementById('box');
  box.className = 'aa bb';//设置
  box.className.replace('aa','AA');//替换
  ```

**小结：元素的style属性适合操作单个样式，而元素className适合操作一组样式**


### 10 操作标签的自定义属性【了解】 

- 什么是自定义属性

  > 针对html标签的属性可以分为两类：
  >
  > - **标签自带属性（语言设计者提供的属性）**
  >   id、title、src、href、name、type等
  >
  > - **自定义标签属性**
  >   用户根据需求，自己给标签添加的自己定义的标签属性
  >
  >   ```html
  >   <img src='wc.jpg' bigImg='bigWc.jpg' />
  >   <!--bigImg='bigWc.jpg' 就是用户自定义的标签属性-->
  >   ```

- 操作方式

  > - 获取
  >
  >   ```javascript
  >   节点对象.getAttribute('属性名');   // 会返回标签的属性的值
  >   ```
  >
  > - 设置
  >
  >   ```javascript
  >   节点对象.setAttribute('属性名','值');   // 会修改或添加标签属性
  >   ```
  >
  > - 删除
  >
  >   ```javascript
  >   节点对象.removeAttribute('属性名');   // 会删除标签的属性
  >   ```

**注意：自定义标签属性的操作只能够通过元素的getAtrribute、setAttribute、removeAttribute提供的方法操作。 不能直接通过元素点的方式直接获取或设置**

### 11 根据元素的关系获取元素

#### 1 元素之间的关系

+ 嵌套关系
  + 父子关系
  + 祖孙关系
+ 并列关系
  + 兄弟关系


#### 2 获取父元素【重点】

- 语法：

  > **元素节点.parentNode**
  >
  > 作用：获取一个节点的父节点

- 代码：

  ```html
  <div id="grandFather">
  	<p id="father">
  		<a href="#" id="son">超链接</a>
  	</p>
  </div>
  <script>
  	// 获取a元素节点
  	var a = document.getElementById('son');
  	// 获取a元素的父节点
  	console.dir(a.parentNode);     // 获取p元素
  	// 获取a元素的父节点的父节点
  	console.dir(a.parentNode.parentNode);  // 获取div元素
  </script> 
  ```

  ​

#### 3 获取子元素【重点】

+ 语法：

  > **元素节点.children** 
  >
  > 作用：获取一组子元素

+ 代码：

  ```html
  <ul id="list">
  	<li>我是li1</li>
  	<li>我是li2</li>
  	<li>我是li3</li>
  	<li>我是li4</li>
  	<li>我是li5</li>
  </ul>
  <script>	
  	// 获取ul元素
  	var ul = document.getElementById('list'); 
  	// 获取ul下的所有元素节点（仅仅元素节点）
  	var items = ul.children;  
  	console.log(items.length);  // 结果是5
  	console.log(items); // HTMLCollection(5) [li, li, li, li, li]
  </script>
  ```


#### 4 获取兄弟元素【了解】

- 获取上一个兄弟元素

  ```javascript
  // 获取上一个同级的元素节点，有兼容问题IE9以下不支持
  元素节点.previousElementSibling;
  ```

- 获取下一个

  ```javascript
  // 获取下一个同级的元素节点，有兼容问题IE9以下不支持
  元素节点.nextElementSibling;
  ```


### 12 动态操作元素

#### 1 创建元素

##### 1.1 创建方式1

- 语法：
  **元素.innerHTML = '内容';**

- 代码：

  ```html
  <ul id="list">
  	<li>我是li1</li>
  	<li>我是li2</li>
  </ul>
  <button id="btn">创建元素</button>
  <script>
  	// 获取按钮元素
  	var btn = document.getElementById('btn');
  	// 获取ul元素
  	var ul = document.getElementById('list');
  	// 获取所有li元素，并给每一个li元素添加点击事件
  	var lis = ul.children;
  	for (var i = 0; i < lis.length; i++) {
  		lis[i].onclick = function () {
  			alert(this.innerText); 
  		};
  	}
  	// 给按钮注册点击事件
  	btn.onclick = function () {
  		// 给ul中添加也新的li元素
  		ul.innerHTML = ul.innerHTML  + '<li><a href="#">我是新的li</a></li>';
  	};
  </script>
  ```

- 缺点：会覆盖部分网页元素以及事件。

- 优点：对于创建嵌套多的元素方便。





##### 2.2 创建方式2

- 语法：
  **document.createElement('标签名');**

- 代码：

  ```html
  <ul id="list">
  	<li>我是li1</li>
  	<li>我是li2</li>
  </ul>
  <button id="btn">创建元素</button>
  <script>
  	// 获取按钮元素
  	var btn = document.getElementById('btn');
  	// 获取ul元素
  	var ul = document.getElementById('list');
  	// 获取所有li元素，并给每一个li元素添加点击事件
  	var lis = ul.children;
  	for (var i = 0; i < lis.length; i++) {
  		lis[i].onclick = function () {
  			alert(this.innerText); 
  		};
  	}
  	// 给按钮注册点击事件
  	btn.onclick = function () {
  		// 创建一个新的li元素节点
  		var li = document.createElement('li');
  		// 把新的li追加到ul最后面
  		ul.appendChild(li)
  		// 创建一个a元素
  		var a = document.createElement('a');
  		// 给a设置属性 和 内容
  		a.href = '#';
  		a.innerText = '我是新来的';
  		// 把a存入到li中
  		li.appendChild(a);
  	};
  </script>
  ```

- 优点：不会覆盖原有的元素的事件。

- 缺点：对于添加嵌套多的内容操作麻烦。




##### 2.3 创建元素性能问题 【了解】

- innerHTML 会产生字符串解析，由于字符串的不可变性，尽量避免大量的拼接，否则消耗内存，影响性能。
- document.createElement('标签')创建的性能要比innerHTML要高，但是若涉及到多层嵌套内容时，代码操作麻烦。
- 所以，一般情况下,两者配合使用较多
  + document.createElement用来创建元素
  + innerHTML可以设置元素中的内容（元素内部的标签或文本）

 **备注：性能测试**

**小结：在开发的中，innerHTML 和 document.createElement配合使用较多** 




#### 2 追加元素

- 语法：
  ​	**父节点.appendChild(新的子节点);**

- 作用：向父节点最后追加新的节点

- 代码：

  ```html
  <ul id="list">
  	<li>我第1个li</li>
  	<li>我第2个li</li>
  	<li>我第3个li</li>
  </ul>
  <button id="btn">按钮</button>
  <script>
  	// 获取ul元素
  	var ul = document.getElementById('list');
  	// 获取按钮元素
  	var btn = document.getElementById('btn');
  	// 给按钮元素注册事件
  	btn.onclick = function () {
  		// 创建一个新的li元素
  		var li = document.createElement('li');
  		// 设定新的li的元素的内容
  		li.innerHTML = '我是新来的';
  		// 把新创建的li元素追加到ul中
  		ul.appendChild(li);
  	}
  </script>
  ```

  ​



#### 3 删除元素

- 语法：
  ​	**父节点.removeChild(子节点)** 

- 作用：删除父元素中的指定的子节点

- 代码：

  ```html
  <ul id="list">
  	<li>我第1个li</li>
  	<li>我第2个li</li>
  	<li>我第3个li</li>
  </ul>
  <button id="btn">删除第二个li</button>
  <script>
  	// 获取ul元素
  	var ul = document.getElementById('list');
  	// 获取按钮元素
  	var btn = document.getElementById('btn');
  	// 给按钮元素注册事件
  	btn.onclick = function () {
  		var li2 = ul.children[1];
  		// 删除第二li
  		ul.removeChild(li2);
  	}
  </script>
  ```

### 12.1：动态操作元素 

#### 2.1 插入元素 【了解】

- 语法：
  ​	**父节点.insertBefore(新的节点,旧的子节点)** 

- 作用：将一个新的节点插入到父节点中的某个子节点的前面

- 代码：

  ```html
  <ul id="list">
  	<li>我第1个li</li>
  	<li>我第2个li</li>
  	<li>我第3个li</li>
  </ul>
  <button id="btn">按钮</button>
  <script>
  	// 获取ul元素
  	var ul = document.getElementById('list');
  	// 获取按钮元素
  	var btn = document.getElementById('btn');
  	// 给按钮元素注册事件
  	btn.onclick = function () {
  		// 创建一个新的li元素
  		var li = document.createElement('li');
  		// 设定新的li的元素的内容
  		li.innerHTML = '我是新来的';
  		// 获取第二li元素
  		var old = ul.children[1];
  		// 把新创建的li元素追加到ul中第二li的前面
  		ul.insertBefore(li,old);
  	}
  </script>
  ```



#### 2.2 替换元素【了解】

- 语法
  ​	**父节点.replaceChild(新的子节点,旧的子节点)** 

- 作用：替换子节点

- 代码

  ```html
  <ul id="list">
  	<li>我第1个li</li>
  	<li>我第2个li</li>
  	<li>我第3个li</li>
  </ul>
  <button id="btn">替换</button>
  <script>
  	// 获取ul元素
  	var ul = document.getElementById('list');
  	// 获取按钮元素
  	var btn = document.getElementById('btn');
  	// 给按钮元素注册事件
  	btn.onclick = function () {
  		// 创建一个新的li元素
  		var li = document.createElement('li');
  		// 设定新的li的元素的内容
  		li.innerHTML = '我是新来的';
  		// 获取第二li元素
  		var old = ul.children[1];
  		// 把新创建的li元素 和 ul中第二li的前面替换
  		ul.replaceChild(li, old);
  	}
  </script>
  ```




### 13 根据节点的关系获取节点

#### 1.1 获取子节点【了解】

- childNodes

  - 语法：

    > **父节点.childNodes**
    >
    > 作用：获取一组子节点（包括文本节点和元素节点）

  - 代码：

    ```html
    <ul id="list">
    	<li>我是li1</li>
    	<li>我是li2</li>
    	<li>我是li3</li>
    	<li>我是li4</li>
    	<li>我是li5</li>
    </ul>
    <script>	
      	// 获取ul元素
    	var ul = document.getElementById('list'); 
        // 获取ul下的所有子节点（包括文本 和 元素节点）
    	var items = ul.childNodes; 
    	console.log(items.length);  // 结果是11
    	console.log(items);  // NodeList(11) [text, li, text, li, text, li, text, li, text, li, text]
    </script>
    ```

    ​

#### 1.2 获取第一个和最后一个子节点【了解】

- 获取第一个

  ```javascript
  // 获取第一个子节点对象，包含空白文本节点对象
  父节点.firstChild;
  // 获取第一个元素子节点对象，有兼容问题IE9以下不支持
  父节点.firstElementChild
  ```

- 获取最后一个

  ```javascript
  // 获取最后一个子节点对象，包含空白文本节点对象
  父节点.lastChild;
  // 获取最后一个元素子节点对象，有兼容问题IE9以下不支持
  父节点.lastElementChild
  ```


### 13 事件监听 
​	   事件监听可以给元素绑定多个事件处理程序。在实际开发中， **便于对事件程序的功能扩展**。

#### 1 什么是事件监听？

​	 **事件注册 或 移除**的第二种方式

#### 2 事件监听给元素注册事件【重要】

- 语法：

  ```javascript
  /*
  	功能：给元素注册事件
  	参数：
  		事件类型  字符串  	注意：事件名不加on 如 'click'
  		事件处理程序	函数
  		是否捕获：可选，默认为false ， true表示启用捕获  false表示启用冒泡
  */
  事件目标.addEventListener(事件类型,事件处理程序,是否捕获);
  ```

- 代码：

  ```html
  <div id="box">我是div</div>
  <button id="btn">点击改变</button>
  <script>
  	// 获取按钮元素节点 和 div元素节点
  	var btn = document.getElementById('btn');
  	var box = document.getElementById('box');
  	// 给按钮注册事件
  	btn.addEventListener('click', function () {
  		box.style.width = '500px';
  	});
  	btn.addEventListener('click',function () {
  		box.style.height = '500px';
  		box.style.backgroundColor = 'blue';
  	});
  </script>
  ```

  ​

#### 3 事件监听移除元素事件程序【重要】

- 语法：

  ```javascript
  /*
  	功能：移除元素的指定事件程序
  	参数：
  		事件类型  字符串  注意：事件名不加on 如：'click'
  		事件处理程序：函数 注意：这里要把函数名传入过来
  */
  事件目标.removeEventListener(事件类型,事件处理程序名称);
  ```

- 代码：

  ```html
  <div id="box">我是div</div>
  <button id="btn">点击改变</button>
  <script>
  	// 获取按钮元素节点 和 div元素节点
  	var btn = document.getElementById('btn');
  	var box = document.getElementById('box');
  	// 定义第一个功能
  	function fn1 () {
  		box.style.width = '500px';
  	}
  	// 给按钮注册事件
  	btn.addEventListener('click',fn1);
  	// 定义第二个功能
  	function fn2 () {
  		box.style.height = '500px';
  		box.style.backgroundColor = 'blue';
  	}
  	// 给按钮注册事件
  	btn.addEventListener('click',fn2);
  	// 移除按钮元素的第二个功能
  	btn.removeEventListener('click', fn2);
  </script>
  ```


### 14 事件流

#### 1 什么是事件流？

​	事件流，指的是 **事件的==传播== 过程。 **传播过程要经历三个阶段（ **事件捕获**、**目标元素** 、 **事件冒泡**）

![](assets/img/01.jpg)

#### 4.2 事件捕获【了解】

- 图解
  **注意：** 虽然没有启用处理捕获阶段，但是捕获阶段依然存在。
  ![](assets/img/03.jpg)


### 15 事件对象【重要】

#### 1 为什么要学习事件对象？

​	在实际应用开发中，我们经常会**通过事件对象 获取当前事件相关的信息**（比如：键盘按下时到底按下了哪个键？鼠标点击或移动时当前鼠标的位置？等等）



#### 2 什么是事件对象？

​	事件对象，是一个小的**工具库**，工具库中存放了和当前事件相关的各种信息和功能。



#### 3 如何获取事件对象？

- 语法：

  ```javascript
  事件目标.事件类型 = function (e) {
    // 事件处理程序（函数），函数的第一个形参就是我们将来要使用的 【事件对象】
  };
  ```

  ![](assets/img/04.jpg)

- 代码：

  ```javascript
  document.onclick = function (e) {
    // 形参e就是当前点击事件的 事件对象
    console.log(e);
  }
  ```

#### 4 事件对象的公共属性和方法

​	公共：不论是什么类型的事件（比如键盘、鼠标、手指触摸等等），他们的事件对象都有的属性 和 方法。

- 公共属性

  - **事件对象.type** 

    - 作用：获取当前的事件名。

    - 代码：

      ```javascript
      document.onclick = function (e) {
          // 查看当前的事件类型
          console.log(_e.type);  // click
      }
      ```

  - **事件对象.target** 

    - 作用：获取事件目标里最先触发事件的元素

    - 备注：在实际处理程序中事件对象的target和this的区别

      + this指的是事件源
      + target指的是最先触发的元素，不一定是事件源

    - 代码：

      ```html
      <!DOCTYPE html>
      <html lang="en">
          <head>
              <meta charset="utf-8">
              <style>
      			div {
      				width: 300px;
      				height: 300px;
      				background-color: green;
      			}
              </style>
          </head>
          <body>
          	<div></div>
          	<script>
          		document.onclick = function (e) {
          			console.log(e.target);
          		};
          	</script>
          </body>
      </html>
      ```

    ​

- 公共方法

  - **事件对象.preventDefault();**

    - 作用：阻止事件默认行为的执行。

    - 代码：

      ```html
      <a id="link" href="//www.baidu.com">点击</a>
      <script>
      	var link = document.getElementById('link');
      	link.onclick = function (e) {
      		alert('执行了');
      		// 阻止默认行为
      		e.preventDefault(); // 可以用return false 代替
      	};
      </script>
      ```

  - **事件对象.stopPropagation();**

    - 作用：停止冒泡

      ​

#### 5 鼠标事件对象的属性

- **事件对象.clientX  /  事件对象.clientY**

  > - 作用：鼠标在**浏览器可视区域**中的坐标
  >
  > - 代码：
  >
  >   ```html
  >   <!DOCTYPE html>
  >   <html>
  >   <head lang="en">
  >     <meta charset="UTF-8">
  >     <title></title>
  >     <style>
  >       body {
  >         height: 2000px;
  >       }
  >     </style>
  >   </head>
  >   <body>
  >     <script>
  >       document.onclick = function (e) {
  >         // 获取鼠标在浏览器可视区域中的坐标
  >         alert('x:' + e.clientX + ',y:' + e.clientY);
  >       }
  >     </script>
  >   </body>
  >   </html>
  >   ```

- **事件对象.offsetX  /  事件对象.offsetY**

  > - 作用：获取鼠标在**指定的元素的区域**中的坐标
  >
  > - 代码：
  >
  >   ```html
  >   <!DOCTYPE html>
  >   <html>
  >   <head lang="en">
  >     <meta charset="UTF-8">
  >     <title></title>
  >     <style>
  >       div {
  >         width: 300px;
  >         height: 300px;
  >         background-color: red;
  >         margin:100px auto;
  >         cursor: default;
  >       }
  >     </style>
  >   </head>
  >   <body>
  >     <div>我第div</div>
  >     <script>
  >       var divNode = document.querySelector('div');
  >       divNode.onclick = function(e){
  >         // 获取鼠标在div中的坐标
  >         alert('X:' + e.offsetX + ',Y:' + e.offsetY);
  >       }
  >     </script>
  >   </body>
  >   </html>
  >   ```

- **事件对象.pageX  /  事件对象.pageY**

  > - 作用：获取鼠标**在整个文档区域**中的坐标
  >
  > - 代码：
  >
  >   ```html
  >   <!DOCTYPE html>
  >   <html>
  >   <head lang="en">
  >     <meta charset="UTF-8">
  >     <title></title>
  >     <style>
  >       body {
  >         height: 2000px;
  >       }
  >     </style>
  >   </head>
  >   <body>
  >     <script>
  >       document.onclick = function(e){
  >         // 获取鼠标在整个文档区域中的坐标
  >         alert('x:' + e.pageX + ',y:' + e.pageY);
  >       }
  >     </script>
  >   </body>
  >   </html>
  >   ```

**图解：client/offset/page的x/y的区别**

![](assets/img/05.jpg)



#### 6 键盘事件对象的属性

- **事件对象.altKey**

  > - 作用：检测是否按下键盘上的  **Alt键**。 按下返回 true  
  >
  > - 代码：
  >
  >   ```javascript
  >     document.onkeydown = function (e) {
  >       alert(e.altKey);  // 按下alt键，返回true
  >     }
  >   ```

- **事件对象.ctrlKey**

  > - 作用：检测是否按下键盘上的   **Ctrl键**。 按下返回 true
  >
  > - 代码：
  >
  >   ```javascript
  >    document.onkeydown = function (e) {
  >       alert(e.ctrlKey);  // 按下Ctrl键，返回true
  >     }
  >   ```

- **事件对象.shiftKey**

  > - 作用：检测是否按下键盘上的   **Shift键**。 按下返回 true
  >
  > - 代码：
  >
  >   ```javascript
  >     document.onkeydown = function (e) {
  >       alert(e.shiftKey);  // 按下shift键，返回true
  >     }
  >   ```

- **事件对象.keyCode**

  > - 作用：返回被敲击的键生成的 **Unicode 字符码**(ascii码)
  >
  > - 代码：
  >
  >   ```javascript
  >     document.onkeydown = function (e) {
  >       alert(e.keyCode); // 返回ascii码表对应的十进制的数字
  >     }
  >   ```



### 扩展：兼容问题

#### 兼容问题1：获取事件对象

- 标准方式： 事件处理程序函数的第一个参数 e

- IE低版本方式：window.event

- 兼容处理：

  ```javascript
  document.onclick = function (e) {
  	// 事件对象的兼容处理
  	var _event = e || window.event;     
  };
  ```



#### 兼容问题2：事件监听的注册和移除

- 注册事件：

  - 标准：

    ```javascript
    /*
    事件目标.addEventListener(事件类型,事件处理程序,是否捕获);

    	事件目标：要绑定的那个节点对象。
    	事件类型：交互行为，在这里不加on
    	事件处理程序：函数
    	是否捕获:可选，布尔值，true是捕获，false是冒泡，默认为false;
    */
    ```

  - IE低版本：

    ```javascript
    /*
    	事件目标.attachEvent(事件类型,事件处理程序);
    	
    	事件目标：要绑定的那个节点对象。
    	事件类型：交互行为，在这里要加on
    	事件处理程序：函数
    */
    ```

  - 兼容处理：

    ```javascript
      /*
        功能：绑定事件
        参数：
          node 事件目标 节点对象
          type 事件类型 string 不加on
          handler 事件处理程序 函数
        返回值：无
      */
      function addEvent(node, type, handler){
        if (node.addEventListener) { // 检测浏览器是否支持标准方式
          // 支持
          node.addEventListener(type, handler);
        } else {
          // 不支持
          node.attachEvent('on' + type, handler);
        }
      }
    ```

    ​
    ​

- 移除事件：

  - 标准：

    ```javascript
    /*
    事件目标.removeEventListener(事件类型,事件处理程序的名称);

    	事件目标: 要解绑事件的那个节点对象
    	事件类型：解绑什么类型的实际，不加on
    	事件处理程序的名称：函数的名称；
    */
    ```

  - IE低版本：

    ```javascript
    /*
    事件目标.detachEvent(事件类型,事件处理程序的名称);

    	事件目标：要绑定的那个节点对象。
    	事件类型：交互行为，在这里要加on
    	事件处理程序的名称：函数名称
    */
    ```

  - 兼容处理：

    ```javascript
      /*
        功能：解绑事件
        参数：
          node 事件目标  节点对象
          type 事件类型  string
          handlerName 事件处理程序名称 函数
        返回值：无
      */
      function removeEvent(node, type, handlerName){
        if (node.removeEventListener) {// 检测浏览器是否支持标准方式
          //支持
          node.removeEventListener(type, handlerName);
        } else {
          // 不支持
          node.detachEvent('on' + type, handlerName);
        }
      }
    ```



###  16 鼠标相关的事件

+ 事件名称：onmousemove
  + 作用：鼠标在元素上移动时，会不断的检测
+ 事件名称：onmosuedown
  + 作用：鼠标按键按下时
+ 事件名称：onmosueup
  + 作用：鼠标按键松开时


  ​# webAPI-第五天

## 一.核心知识点

+ 事件委托（原理、实现方式、作用）
+ 定时器（setInterval）
+ DOM元素的offset系列属性


## 二. 事件委托

### 2.1 什么是事件委托

​	事件委托，也叫==事件代理== 。指的是子孙元素的事件绑定，完全交给其上级父元素或祖先元素绑定。

### 2.2 为什么学习事件委托

​	在web前端开发中，并不是程序注册事件越多越好， **事件注册越多，就越消耗程序的性能**。所以，在事件注册较多的情况下， **为了提高程序的性能，应当适当减少事件的绑定**。

​	传统的事件处理中，需要为每个元素注册事件。事件委托则是一种简单有效的技巧，通过它可以把**事件注册到一个父级或父级以上的元素上**，从而**避免把事件注册到多个子级元素上**。

### 2.3 事件委托的原理 【重点】

​	事件委托的原理用到的就是  **目标元素** 和  **事件冒泡**，**把事件注册到父元素或父级以上的元素上**，等待 **子元素事件冒泡**，并且在父元素或父级以上的元素注册的事件中能够 **通过事件对象.target判断是哪个子元素**，从而做相应处理。
​	==① 给目标元素的父元素或父级以上的元素注册事件== 

​	==② 在父元素或父级以上元素注册的事件中通过 **事件对象.target**判断是哪个子元素== 

​	==③ 根据判断做出处理。== 



### 2.4 事件委托的作用【重点】

- 提高程序性能
- 可以代理新动态添加的元素的事件。



### 2.5 代码实现

```html
<!DOCTYPE html>
<html>
<head lang="en">
  <meta charset="UTF-8">
  <title></title>
  <style>
    p {
      background-color: blue;;
    }
  </style>
</head>
<body>
  <div id="box">
    <h2>标题</h2>
    <p>段落1</p>
    <p>段落2</p>
    <h2>标题</h2>
    <p>段落3</p>
    <h2>标题</h2>
    <p>段落4</p>
    <p>段落5</p>
    <h2>标题</h2>
    <p>段落6</p>
    <p>段落7</p>
    <h2>标题</h2>
  </div>
  <script>
  	// 获取div元素
    var divNode = document.getElementById('box');
    divNode.onclick = function(e){
      // 获取最先触发的元素节点
      var node = e.target;
      // 节点对象.tagName  获取节点对象对应的标签名 返回的是大写
      if(node.tagName.toLowerCase()=='p'){
        alert(node.innerHTML);
      }
    }
  </script>
</body>
</html>
```



### 课堂一练

+ 案例1:    事件委托的方式事件对ul中的li（原有的和新添加的）的点击事件
+ 案例2： 事件委托的方式实现表格管理中的删除功能





## 四. DOM中的元素的offset系列属性

### 4.1 获取元素的大小 【重要】

- 语法：

  > **元素.offsetWidth**  和  **元素.offsetHeight**
  >
  > 获取元素的宽度 和 高度，返回数字，不含单位。
  >
  > 元素的宽度：width + padding(左右) + border（左右）;
  >
  > 元素的高度： height + padding(上下) + border(上下);

- 代码：

  ```html
  <!DOCTYPE html>
  <html>
  <head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
      div {
        width: 100px;
        height: 100px;
        padding: 10px;
        border: 5px solid red;
        background-color: blue;
      }
    </style>
  </head>
  <body>
    <div></div>
    <script>
      var divNode = document.querySelector('div');
      // width(100) + padding(左10 右10) + border(左5 右5)
      console.log(divNode.offsetWidth);// 130
      // height(100) + padding(上10 下10) + border(上5 下5)
      console.log(divNode.offsetHeight);// 130
    </script>
  </body>
  </html>
  ```

  ​

### 4.2 获取元素的位置【重要】

- 语法：

  > **元素.offsetLeft**   和   **元素.offsetTop**
  > 作用：获取元素的坐标，相对于其最近的定位的上级元素的坐标。否则，相对于body。

- 代码：父元素定位了

  ```html
  <!DOCTYPE html>
  <html>
  <head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
      * {
        margin:0;
        padding:0;
      }
      .father {
        width: 300px;
        height: 300px;
        background-color:blue;
        margin:50px auto;
        border:1px solid blue;
        position: relative;
      }
      .son {
        width:200px;
        height: 200px;
        margin:50px auto;
        background-color: #000;
      }
    </style>
  </head>
  <body>
    	<!--父元素是定位的-->
      <div class="father">
        <div class="son"></div>
      </div>
      <script>
        var sonNode = document.querySelector('.son');
        console.log(sonNode.offsetLeft);// 50  参照定位的父元素
        console.log(sonNode.offsetTop); // 50  参照定位的父元素
      </script>
  </body>
  </html>
  ```

- 代码：父元素没有定位

  ```html
  <!DOCTYPE html>
  <html>
  <head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
      * {
        margin:0;
        padding:0;
      }
      .father {
        width: 300px;
        height: 300px;
        background-color:blue;
        margin:50px auto;
        border:1px solid blue;
      }
      .son {
        width:200px;
        height: 200px;
        margin:50px auto;
        background-color: #000;
      }
    </style>
  </head>
  <body>
      <!-- 父元素的没有定位-->
      <div class="father">
        <div class="son"></div>
      </div>
      <script>
        var sonNode = document.querySelector('.son');
        console.log(sonNode.offsetLeft);// 406  参照body
        console.log(sonNode.offsetTop);// 101   参照body
      </script>
  </body>
  ```

  ​

### 4.3 获取元素的父元素【重要】

- 语法：

  > **元素.offsetParent**
  > 作用：获取元素的最近的定位的上级元素

- 代码1：父元素定位了

  ```html
  <!DOCTYPE html>
  <html>
  <head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
      * {
        margin:0;
        padding:0;
      }
      .father {
        width: 300px;
        height: 300px;
        background-color:blue;
        margin:50px auto;
        border:1px solid blue;
        position: relative;
      }
      .son {
        width:200px;
        height: 200px;
        margin:50px auto;
        background-color: #000;
      }
    </style>
  </head>
  <body>
      <!-- 父元素有定位-->
      <div class="father">
        <div class="son"></div>
      </div>
      <script>
        var sonNode = document.querySelector('.son');
        var parent = sonNode.offsetParent;
        console.log(parent); // 获取定位的上级元素，div.father
      </script>
  </body>
  </html>
  ```

- 代码2：父元素没有定位

  ```html
  <!DOCTYPE html>
  <html>
  <head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
      * {
        margin:0;
        padding:0;
      }
      .father {
        width: 300px;
        height: 300px;
        background-color:blue;
        margin:50px auto;
        border:1px solid blue;
      }
      .son {
        width:200px;
        height: 200px;
        margin:50px auto;
        background-color: #000;
      }
    </style>
  </head>
  <body>
      <!-- 父元素没有定位-->
      <div class="father">
        <div class="son"></div>
      </div>
      <script>
        var sonNode = document.querySelector('.son');
        var parent = sonNode.offsetParent;
        console.log(parent); // 因为没有最近的定位的上级元素，所以获取body
      </script>
  </body>
  </html>
  ```

### 1.4 图解offset系列属性

![](media/06.png)



### 本节小结

> 获取元素的大小
>
> 获取元素的位置
>
> 获取元素的父元素



## 课堂一练

+ 案例1：放大镜



## 扩展：

### 扩展1：BOM中window对象中onload事件和onunload事件

- onload

  - 作用：页面加载（页面元素，图片，媒体资源，外联等）完后要执行的代码。

  - 代码：

    ```javascript
    onload = function() {
    	console.log('页面加载完了');
    }
    ```

- onunload

  - 作用：页面卸载完后（刷新），要执行的代码。

  - 代码：

    ```javascript
    onunload = function() {
    	console.log('页面卸载了');
    }
    ```



### 扩展2：onmouseenter和onmouseover的区别 以及onmouseleave和onmouseout的区别

+ 相同点：
  + 都是鼠标进入或离开事件，功能一致。
+ 不同点：
  + onmouseenter和onmouseleave不冒泡
  + onmouseover和onmouseout会冒泡

  ​
## 一. offset系列【回顾】

### 1.1 获取元素的大小 【重要】

- 语法：

  > **元素.offsetWidth**  和  **元素.offsetHeight**
  >
  > 获取元素的宽度 和 高度，返回数字，不含单位。
  >
  > 元素的宽度：width + padding(左右) + border（左右）;
  >
  > 元素的高度： height + padding(上下) + border(上下);

- 代码：

  ```html
  <!DOCTYPE html>
  <html>
  <head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
      div {
        width: 100px;
        height: 100px;
        padding: 10px;
        border: 5px solid red;
        background-color: blue;
      }
    </style>
  </head>
  <body>
    <div></div>
    <script>
      var divNode = document.querySelector('div');
      // width(100) + padding(左10 右10) + border(左5 右5)
      console.log(divNode.offsetWidth);// 130
      // height(100) + padding(上10 下10) + border(上5 下5)
      console.log(divNode.offsetHeight);// 130
    </script>
  </body>
  </html>
  ```

  ​

### 1.2 获取元素的位置【重要】

- 语法：

  > **元素.offsetLeft**   和   **元素.offsetTop**
  > 作用：获取元素的坐标，相对于其最近的定位的上级元素的坐标。否则，相对于body。

- 代码：父元素定位了

  ```html
  <!DOCTYPE html>
  <html>
  <head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
      * {
        margin:0;
        padding:0;
      }
      .father {
        width: 300px;
        height: 300px;
        background-color:blue;
        margin:50px auto;
        border:1px solid blue;
        position: relative;
      }
      .son {
        width:200px;
        height: 200px;
        margin:50px auto;
        background-color: #000;
      }
    </style>
  </head>
  <body>
    	<!--父元素是定位的-->
      <div class="father">
        <div class="son"></div>
      </div>
      <script>
        var sonNode = document.querySelector('.son');
        console.log(sonNode.offsetLeft);// 50  参照定位的父元素
        console.log(sonNode.offsetTop); // 50  参照定位的父元素
      </script>
  </body>
  </html>
  ```

- 代码：父元素没有定位

  ```html
  <!DOCTYPE html>
  <html>
  <head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
      * {
        margin:0;
        padding:0;
      }
      .father {
        width: 300px;
        height: 300px;
        background-color:blue;
        margin:50px auto;
        border:1px solid blue;
      }
      .son {
        width:200px;
        height: 200px;
        margin:50px auto;
        background-color: #000;
      }
    </style>
  </head>
  <body>
      <!-- 父元素的没有定位-->
      <div class="father">
        <div class="son"></div>
      </div>
      <script>
        var sonNode = document.querySelector('.son');
        console.log(sonNode.offsetLeft);// 406  参照body
        console.log(sonNode.offsetTop);// 101   参照body
      </script>
  </body>
  ```

  ​

### 1.3 获取元素的父元素【重要】

- 语法：

  > **元素.offsetParent**
  > 作用：获取元素的最近的定位的上级元素

- 代码1：父元素定位了

  ```html
  <!DOCTYPE html>
  <html>
  <head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
      * {
        margin:0;
        padding:0;
      }
      .father {
        width: 300px;
        height: 300px;
        background-color:blue;
        margin:50px auto;
        border:1px solid blue;
        position: relative;
      }
      .son {
        width:200px;
        height: 200px;
        margin:50px auto;
        background-color: #000;
      }
    </style>
  </head>
  <body>
      <!-- 父元素有定位-->
      <div class="father">
        <div class="son"></div>
      </div>
      <script>
        var sonNode = document.querySelector('.son');
        var parent = sonNode.offsetParent;
        console.log(parent); // 获取定位的上级元素，div.father
      </script>
  </body>
  </html>
  ```

- 代码2：父元素没有定位

  ```html
  <!DOCTYPE html>
  <html>
  <head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
      * {
        margin:0;
        padding:0;
      }
      .father {
        width: 300px;
        height: 300px;
        background-color:blue;
        margin:50px auto;
        border:1px solid blue;
      }
      .son {
        width:200px;
        height: 200px;
        margin:50px auto;
        background-color: #000;
      }
    </style>
  </head>
  <body>
      <!-- 父元素没有定位-->
      <div class="father">
        <div class="son"></div>
      </div>
      <script>
        var sonNode = document.querySelector('.son');
        var parent = sonNode.offsetParent;
        console.log(parent); // 因为没有最近的定位的上级元素，所以获取body
      </script>
  </body>
  </html>
  ```

### 1.4 图解offset系列属性

![](media/offset.png)



## 二. client系列

### 2.1 获取元素的大小【了解】

+ 语法

  > **元素.clientWidth**和 **元素.clientHeight** 
  >
  > 获取元素的宽度 和 高度，返回数字，不含单位。
  >
  > 元素的宽度：width + padding(左右) ;
  >
  > 元素的高度： height + padding(上下) 

+ 代码

  ```html
  <!DOCTYPE html>
  <html>
  <head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
      div {
        width: 100px;
        height: 100px;
        padding:10px;
        border:5px solid red;
        background-color: blue;
        margin: 100px auto;
      }
    </style>
  </head>
  <body>
    <div></div>
    <script>
      var divNode = document.querySelector('div');
      // width(100) + padding(左10 右10) 
      // 注意：不包含边框
      console.log(divNode.clientWidth);//120
      // height(100) + padding(上10 下10)
  	// 注意：不包含边框
      console.log(divNode.clientHeight);//120
    </script>
  </body>
  </html>
  ```

  ​

### 2.2 获取元素的位置【了解】

+ 语法：

  > **元素.clientLeft**   和   **元素.clientTop**
  > 作用：获取元素的坐标，获取当前节点对象的padding的外边界，距离border外边界的距离。实际上就是左边框的厚度。

+ 代码：

  ```html
  <!DOCTYPE html>
  <html>
  <head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
      div {
        width: 200px;
        height: 200px;
        padding:10px;
        border:10px solid red;
        border-top:50px solid red;
        background-color: blue;
        margin: 100px auto;
      }
    </style>
  </head>
  <body>
  <div></div>
  <script>
    var divNode = document.querySelector('div');
    console.log(divNode.clientLeft);// 10
    console.log(divNode.clientTop);// 50
  </script>
  </body>
  </html>
  ```



### 2.3 图解client系列属性

![](media/client2.png)



## 三. scroll系列

### 3.1 获取元素的大小【了解】

+ 语法：

  > **元素.scrollWidth**  和  **元素.scrollHieght**
  > 获取当前节点对象的宽度和高度，返回数字，不包含单位。
  >
  > 宽度：width+padding（左右）+ 溢出部分
  >
  > 高度：height+padding（上下）+ 溢出部分

+ 代码1：

  ```html
  <!DOCTYPE html>
  <html>
  <head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
      * {
        margin:0;
        padding:0;
      }
      .father {
        width:300px;
        height: 300px;
        background-color: #000;
        margin:100px auto;
        /*overflow: auto;*/
        padding: 10px;
        border:10px solid red;
      }
      .son {
        width: 400px;
        height: 100px;
        background-color: blue;
      }
    </style>
  </head>
  <body>
    <div class="father">
      <div class="son">

      </div>
    </div>
    <script>
      var fNode = document.querySelector('.father');
      /*
        width + padding(左右)  包含溢出部分
      */
      console.log(fNode.scrollWidth); // 410
    </script>
  </body>
  </html>
  ```

  ![](media/scroll1.png)

+ 代码2：

  ```html
  <!DOCTYPE html>
  <html>
  <head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
      * {
        margin:0;
        padding:0;
      }
      .father {
        width:300px;
        height: 300px;
        background-color: #000;
        margin:100px auto;
        padding: 10px;
        border:10px solid red;
      }
      .son {
        width: 100px;
        height: 400px;
        background-color: blue;
      }
    </style>
  </head>
  <body>
    <div class="father">
      <div class="son">

      </div>
    </div>
    <script>
      var fNode = document.querySelector('.father');
      /*
        height + padding(上下)  包含溢出部分
      */
      console.log(fNode.scrollHeight); //410
    </script>
  </body>
  </html>
  ```

  ![](media/scroll2.png)

  ​

### 3.2 获取元素中被卷去的内容的距离【重要】

+ 语法：

  > **元素.scrollLeft【了解】**  和  **元素.scrollTop【重点】**
  > 作用：获取元素内部总被卷去的内容的横向距离  和  **纵向距离** 

+ 代码：

  + 代码1：

    ```html
    <!DOCTYPE html>
    <html>
    <head lang="en">
      <meta charset="UTF-8">
      <title></title>
      <style>
        * {
          margin:0;
          padding:0;
        }
        .father {
          width:300px;
          height: 300px;
          background-color: #000;
          margin:100px auto;
          padding: 10px;
          overflow: auto;
          border:10px solid red;
        }
        .son {
          width: 400px;
          height: 100px;
          background-color: blue;
        }
      </style>
    </head>
    <body>
      <div class="father">
        <div class="son">

        </div>
      </div>
      <script>
        var fNode = document.querySelector('.father');
        fNode.onscroll = function(){
          console.log(fNode.scrollLeft);
        }
      </script>
    </body>
    </html>
    ```

    ![](media/scroll3.png)

    ​

  + 代码2：

    ```html
    <!DOCTYPE html>
    <html>
    <head lang="en">
      <meta charset="UTF-8">
      <title></title>
      <style>
        * {
          margin:0;
          padding:0;
        }
        .father {
          width:300px;
          height: 300px;
          background-color: #000;
          margin:100px auto;
          padding: 10px;
          overflow: auto;
          border:10px solid red;
        }
        .son {
          width: 100px;
          height: 400px;
          background-color: blue;
        }
      </style>
    </head>
    <body>
      <div class="father">
        <div class="son">

        </div>
      </div>
      <script>
        var fNode = document.querySelector('.father');
        fNode.onscroll = function(){
          console.log(fNode.scrollTop);
        }
      </script>
    </body>
    </html>
    ```

    ![](media/scroll4.png)



## 本章小结

> 能够区分offset、client、scroll三个系列属性的区别
>
> 掌握onscroll事件以及scrollLeft和**scrollTop** 的使用

## 课堂一练

1. 固定导航栏和回到顶部案例





