### 1 BOM介绍【了解】

​	BOM：（**B**rowser **O**bject **M**odel） **浏览器对象模型**。提供了操作浏览器的工具库（浏览器中的文档，地址栏，刷新，历史记录，浏览器的信息等等）。
![](media/01.png)



### 2 BOM中的顶级对象window

#### 2.1 window是顶级对象【重要】

- window对象被称为 **顶级对象**（ **全局对象**），在程序中所有的 **全局变量**或者**全局函数**都会被当作window对象中的属性或方法。

- 书写时, **window对象可以省略**

- 代码：

  ```javascript
  // 全局变量
  var userName = '张三';   
  function test(){   // 全局函数
    alert('hello');
  }
    console.log(window.userName); // '张三';
    console.log(userName); // '张三';   window对象可以省略

    window.test();  // 'hello';
    test(); // 'hello';  window对象可以省略
  ```

  **注意：**
  ​	 在定义全局变量名，命名不要是 name 和 top。
  ​	 name变量若存入数组时， 在window中永远都会是字符串。
  	 top 在window中已经被占用，并且top是只读的，无法修改top变量的值。



#### 2.2 window对象中的对话框方法【了解】

- alert();

- prompt();

- confirm(); 

- 代码：

  ```javascript
  alert(1);  // window.alert(1);
  confirm('你确定要删除吗？');  // window.confirm('你确定要删除吗？');
  prompt('请输入你的年龄'); // window.prompt('请输入你的年龄');
  ```



#### 2.3 window对象中的定时器方法【重要】

- **setTimeout(callback, time);**    

  - **作用**：超时调用，**仅执行一次** 。定时炸弹

  - **参数**：

    - callback，函数，表示超时时要执行的程序。
    - time，数字，表示毫秒数

  - **返回值**：返回一个数字，标识这一个定时器。

  - **代码**：

    ```javascript
    // 三秒后爆炸
    setTimeout(function () {
    	alert('爆炸了！');
    }, 3000);
    // 问题：定时器后面的代码，是在爆炸后执行？还是爆炸前执行？为什么？
    console.log('执行了');
    ```

    ![](media/02.png)

    ​

  - **清除setTimeout定时器**

    - 语法：**clearTimeout(定时器数字标识);** 

    - 代码：

      ```html
      <button id="stop">清除定时器（拆弹）</button>
      <script>
      	// 创建一个定时器，并用变量接收定时器返回的标识。
      	var flag = setTimeout(function () {
      		alert('爆炸');
      	}, 3000);
      	// 获取按钮元素
      	var stop = document.getElementById('stop');
      	// 给按钮元素注册点击事件
      	stop.onclick = function () {
      		// 清除定时器
      		clearInterval(flag);
      	};
      </script>
      ```

    ​

- **setInterval(callback, time);**  

  - **作用**：超时调用，重复执行（每间隔一段时间执行一次）。 定时闹钟

  - **参数**：

    - callback，函数，表示超时时要执行的程序。
    - time，数字，表示毫秒数

  - **返回值**：返回一个数字，标识这一个定时器。

  - **代码**：

    ```javascript
    setInterval(function () {
    	console.log('懒虫起床');
    }, 3000);
    ```

    ![](media/03.png)

  - **清除setInterval定时器**

    - 语法：**clearInterval(定时器数字标识);**

    - 代码：

      ```html
      <button id="stop">清除定时器（摔闹钟）</button>
      <script>
      	// 创建一个定时器，并用变量接收定时器返回的标识。
      	var flag = setInterval(function () {
      		console.log('懒虫起床');
      	}, 1000);
      	// 获取按钮元素
      	var stop = document.getElementById('stop');
      	// 给按钮元素注册点击事件
      	stop.onclick = function () {
      		// 清除定时器
      		clearInterval(flag);
      	};
      </script>
      ```

    ​



### 3 BOM中的location对象【了解】

#### 3.1 location对象介绍

​	location对象可以用来**操作地址栏中的地址 **



#### 3.2 URL介绍

- URL统一资源定位符 (Uniform Resource Locator, URL)，指的就是**网址** 

- URL的组成： **scheme://host:port/path?query#fragment**

  ```
  scheme:通信协议
  	常用的http,https,ftp,maito等
  	
  host:主机
  	服务器(计算机)域名系统 (DNS) 主机名或 IP 地址。
  	
  port:端口号
  	整数，可选，省略时使用方案的默认端口，如http的默认端口为80。
  	
  path:路径
  	由零或多个'/'符号隔开的字符串，一般用来表示主机上的一个目录或文件地址。
  	
  query:查询
  	可选，用于给动态网页传递参数，可有多个参数，用'&'符号隔开，每个参数的名和值用'='符号隔开。例如：name=zs
  	
  fragment:信息片断
  	字符串，锚点.
  ```

  ![](media/04.png)

#### 3.3 location对象中的属性

![](media/05.png)

> ```javascript
> // 地址：https://www.jd.com/index.html?userName=admin&pwd=123456#beijing
> console.log(location.hash);  // #beijing
> console.log(location.host);  // www.jd.com
> console.log(location.hostname);  // www.jd.com
> console.log(location.href);  // https://www.jd.com/index.html?userName=admin&pwd=123456#beijing
> console.log(location.hostname);  // /index.html
> console.log(location.port);  // '' 默认是80
> console.log(location.protocol);  // https
> console.log(location.search); // ?userName=admin&pwd=123456
> ```



#### 3.4 location对象中的方法

- location.reload();

  ```html
  <!--刷新当前页面-->
  <button onclick="location.reload()">刷新</button>
  ```



### 3.4 BOM中的history对象【了解】

- history对象介绍

  > 用来**操作历史记录**

- history对象中常用的方法

  > - history.back();
  >
  >   ```html
  >   <!--加载上一个历史记录-->
  >   <button onclick="history.back()">上一个页面</button>
  >   ```
  >
  > - history.forward();
  >
  >   ```html
  >   <!--加载下一个历史记录-->
  >   <button onclick="history.forward()">下一个页面</button>
  >   ```
  >
  > - history.go(num);
  >
  >   ```html
  >   <!--加载上一个历史记录-->
  >   <button onclick="history.go(-1)">上一个页面</button>
  >   <!--加载下一个历史记录-->
  >   <button onclick="history.go(1)">下一个页面</button>
  >   ```



### 3.5 BOM中的Navigator对象【了解】

- navigator对象介绍

  > 用来获取当前浏览器的信息（所在的系统、浏览器的版本）

- navigator对象中常见的属性

  > - navigator.userAgent
  >
  >   ```javascript
  >   通过userAgent可以判断用户浏览器的类型
  >   ```
  >
  > - navigator.platform
  >
  >   ```javascript
  >   通过platform可以判断浏览器所在的系统平台类型.
  >   ```


> 1. 理解window对象是顶级对象
> 2. 掌握两种定时器的创建 和 清理
> 3. 掌握location对象中href属性


