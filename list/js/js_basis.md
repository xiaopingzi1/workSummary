## js简单介绍
```javascript
1.  1994年，网景公司(Netscape)发布了Navigator浏览器0.9版，这是世界上第一款比较成熟的网络浏览器，
	轰动一时。但是这是一款名副其实的浏览器--只能浏览页面，浏览器无法与用户互动,当时解决这个问题有两个办		法，一个是采用现有的语言,许它们直接嵌入网页。另一个是发明一种全新的语言。
2. 1995年Sun公司将Oak语言改名为Java，正式向市场推出。Sun公司大肆宣传，许诺这种语言可以"一次编写，到处运	 行"(Write Once, Run Anywhere)，它看上去很可能成为未来的主宰。
3. 网景公司动了心，决定与Sun公司结成联盟
4. 34岁的系统程序员Brendan Eich登场了。1995年4月，网景公司录用了他,他只用10天时间就把Javascript设计出来了。  （多肽语言）
5.  (1)借鉴C语言的基本语法; (2)借鉴Java语言的数据类型和内存管理; (3)借鉴Scheme语言，将函数提升到"第一等公民"(first class)的地位; (4)借鉴Self语言，使用基于原型(prototype)的继承机制。
```
> #### JavaScript是什么？

```javascript
 JavaScript： 基于对象和事件驱动，运行在浏览器客户端的脚本语言。[js]
	
     ✔ js的运行环境： 运行在浏览器端的一种语言
     ✔ 最后将所有的js代码都要以对象的形式去执行，都要通过事件的方式去触发执行【DOM】 
 对象： 
	 现实世界中的对象：  将任何一个具体的事物都是一个对象【万事万物皆对象】
   编程中的对象： 对现实中对象的抽象描述。
     
 ✔面向对象：【推荐】
 	   代码执行都要以一个具体的对象为整体去执行
 
 ✔面向过程：
 	   代码执行的时候，一行一行执行的。
```


> #### JavaScript组成

```javascript
  ☞ ECMASCRIPT    定义了javascript的语法规范,描述了语言的基本语法和数据类型
  
  ☞ BOM （Browser Object Model） 即浏览器对象模型。
	浏览器对象模型,一套操作浏览器功能的API,通过BOM可以操作浏览器窗口，比如：弹出框、控制浏览器跳转、获取分辨率等
    
  ☞ DOM (Document Object Model) 文档对象模型,一套操作页面元素的API,DOM可以把HTML看做是文档树，通过	     
  DOM提供的API可以对树上的节点进行操作 【js+HTMl+css】
```

## JavaScript书写位置

> #### 内嵌式写法

```javascript
 ☞  在html页面内部设置
     <script type="text/javascript">
		 js
	</script>

  注意：
  	  该标签可以放到head标签中或者body标签中
```

> #### 外联式写法[推荐写法]

```javascript
 ☞ 
 	1. 新建js文件
    1. 通过script标签引用到当前页面中
    <script type="text/javascript" src="test.js"></script>


 注意：
	  1. 不能将代码写到外联式标签中。
      2. 一个网页中可以同时调用多个外部js文件
    <script type="text/javascript" src="test.js"></script>
	<script type="text/javascript" src="test.js"></script>
	<script type="text/javascript" src="test.js"></script>
	<script type="text/javascript" src="test.js"></script>
```

> #### 行内式写法（不推荐）

```javascript
☞  将js代码写到标签内部
<div onclick="js代码"></div>

注意：
	 onclick 是一个点击事件： 当点击div的时候，会触发该事件，执行该事件中的代码
```

## JavaScript中输入消息方式

```javascript

alert();

document.write('<h1>我是一段文字</h1>');   在网页中输出信息

prompt("请输入姓名","测试");

confirm("确定不听课么");

console.log("adsadsfafds");

总结：
	1. 在js中如果希望输出一个具体的文本信息，必须带引号
  2. 在使用document.write();的时候，可以在方法内输出html标签，加引号。
```

## 变量（重点）

> #### 变量概念

```javascript
 ☞ 变量：  在程序中用来保存数据的一个容器
```

> #### 定义变量及赋值

```javascript
 ☞ 定义变量
	var 自定义变量名；
    
☞ 变量赋值	

	 变量名 = 值；

☞ 总结：
	  1. 变量一次只能保存一个值
    2. 变量只能保存最后一次赋值结果
    3. js中区分字母大小写
```

> #### 变量命名规范

```javascript
☞ 规则    必须遵守的，不遵守的话 JS引擎 发现并报错 
    1. 由字母(A-Za-z)、数字(0-9)、下划线(_)、美元符号( $ )组成，如：var usrAge, num01, _name
    2. 区分大小写 强调：JS 严格区分大小写 ，var app; 和 var App; 是两个变量
    3. 不能 以数字开头，或者汉字定义变量名
    4. 不能 是关键字、保留字 和 代码符号，例如：var、for、while、&, class
    5. 不能出现空格
        
☞ 规范  建议遵守的，不遵守的话 JS引擎 也不会报错
	1. 变量名必须有意义
  2. 遵守驼峰命名法。首字母小写，后面单词的首字母需要大写。
```

## 数据类型（重点）

> #### 数据类型
>
> ```javascript
>   ☞ 数据类型---- 指的是变量的数据类型
> ```

> #### 简单数据类型
>
> - 数值类型(number)
>
> ```javascript
>  ☞ 凡是数字都属于该类型【整数，小数，负数】
>  
>  ☞ 只要变量的值是一个具体的数字，那么当前变量的数据类型就是数值类型
>  
>  ☞ number类型表示的数字大小：
>  	  最大值是±1.7976931348623157乘以10的308次方    Number.MAX_VALUE
>       最小值是±5 乘以10的-324次方				  Number.MIN_VALUE
>   
>  ☞ 数值类型表示方式：
> 	 ✔ 十进制表示
>      	var  n1=10,n2=9, n3=100;
> 
> 	 ✔ 十六进制表示
>      	以 0x开头 0到9之间的数字，a(A)-f(F)之间字母构成。 a-f对应的数字是10-15
> 		var num = 0xA;
> 
> 	 ✔ 八进制表示
>      	八进制直接以数字0开始，有0-7之间的数字组成。
>         var num1 = 07;   // 对应十进制的7
>         var num2 = 019;  // 对应十进制的19
>         var num3 = 08;   // 对应十进制的8
> 
> ☞ 备注：
> 	 进行算数计算时，八进制和十六进制表示的数值最终都将被转换成十进制数值。
> ```
>
> - 字符串类型(string)
>
> ```javascript
>  ☞ 字符串可以是引号中的任意文本。可以使用单引号或双引号
>  
>  ☞  在js中一般写字符串类型的变量时候，推荐使用单引号。
>  
>  ☞ 注意：
> 	 1. 单引号和双引号之间的嵌套
>       	例如： 输出    我是"高帅富"程序猿;  
>         
>      2. 转义字符
>      	 \n        换行
>          \\		   斜杠
>          \'		   单引号
> 		\"		  双引号
> 		\r 		  回车符
>         
>         例如：
>         var strMsg = 'I'm the GOD of my world ~!';   //输出：I'm the GOD of my world ~!
>         var strMsg2 = "I"m the GOD of my world ~!";  //输出：I"m the GOD of my world ~!
>         var strMsg3 = '反斜杠是这个 \\，神奇！';  //输出：反斜杠是这个 \，神奇！
> ```
>
> - 布尔类型(boolean)
>
> ```javascript
>  ☞ true  和 false 
> ```
>
> - undefined类型（了解）
>
> ```javascript
> ☞ 如果一个变量，没有赋值，那么该变量的默认是是 undefined
> 
> ☞ 如果一个变量的值是undefined，那么该变量对应的数据类型就是undefined类型
> ```
>
> - null 空对象类型（了解）
>
> ```javascript
>   ◆ null类型被看做空对象指针.只有一个值，即 null 值
>   ◆ null 空比如一个变量原先有值 可以将变量的值设置为null 代表清空变量容器中的数据 
>   ◆ 作用为了清空对象。
> ```

> #### 复杂数据类型
>
> - object类型
>

#### 数据类型判断

```javascript
 ☞ 使用  typeof 变量  可以得到对应变量的数据类型
 
 例如：
	    var n1 = '123';
		var n2;
		console.log(typeof  n2);
```

#### 判断一个变量是不是数字

```javascript
isNaN(x) 方法

例如：
	var usrAge = 21;
    var isOk = isNaN(usrAge);
    console.log(isNum); // false ，21 不是一个 非数值

    var usrName = "James";
    console.log(isNaN(usrName));//true ，"James"是一个 非数值
```

#### 数据类型转换

- 转数值类型

```javascript
 ☞Number(变量)：
  	 总结：
     	1. 可以通过该方法将数据类型转换为数值类型
        var n1 = '123';
			n1 = Number(n1);
      2. 在转换的过程中，遇到小数直接保留下来，不会舍去
      3. 如果变量无法转换为数值类型，那么返回的结果是NaN； 对应的数据类型依然是数值类型
      4. 如果将布尔类型转换为数值类型，true 转化后的结果是 1  false 转化后的结果是0
          
  ☞parseInt(变量)
  	var num1 = parseInt("12.3abc");   // 返回12，如果第一个字符是数字会解析知道遇到非数字结束
    var num2 = parseInt("abc123");   // 返回NaN，如果第一个字符不是数字或者符号就返回NaN
    备注：
        1 只会保留整数部分，通过该方式进行数据类型转换后得到就是一个整数
        2. 如果一个变量中的值无法转换为具体数字，那么返回的结果是一个 NaN 的值
        3. NaN (not  a  number)   ----NaN对应的数据类型是数值类型
        4. 通过该方法可以将其他数据类型转为数值类型
        
        
  ☞parseFloat(变量)
	总结：
    	1. 通过该方法可以将其他数据类型转换为数值类型
      2. 在转换过程中，如果遇到小数，那么会直接将小数部分保留
      3. 如果转化不成功过，返回的结果NaN
         
	parseFloat()把字符串转换成浮点数
    
```

- 转字符串类型

```javascript
 ☞  toString()
 		var num = 5;
		console.log(num.toString());

 ☞  String()
    	
	备注：
	String()函数存在的意义：有些值没有toString()，这个时候可以使用String()。比如：undefined和null
```

- 转布尔类型

```javascript
 ☞ Boolean() 
 备注：
	 0  |''(空字符串) | null | undefined | NaN  会转换成false  其它都会转换成 true
```
##运算符

#### 算数运算符

```javascript
 +运算
	总结：
    	1. 如果是数值类型的变量相加，得到的结果是数值类型
      2. 如果有一个数据类型是字符串类型，相加得到的结果是字符串结果 【加号起到就是一个连接的作用】
 -运算
	总结：
	  	1. 如果是数值类型的变量相减，得到的结果是数值类型
      2. 如果一个非数字类型的字符串相减，得到的结果是 NaN
 	    3. 如果是一个数字的字符串相减，得到的结果是数值类型（代码在执行过程中发生了隐式类型转换）
        
 *运算
	总结：
	  	1. 如果是数值类型的变量相乘，得到的结果是数值类型
      2. 如果是一个数字的字符串相乘，得到的结果是数值类型（代码在执行过程中发生了隐式类型转换）
      3. 如果一个非数字类型的字符串相乘，得到的结果是 NaN
	
 /运算
	 总结：
     	1. 如果是数值类型的变量相除，得到的结果是数值类型 
      2. 如果是一个数字的字符串相乘，得到的结果是数值类型（代码在执行过程中发生了隐式类型转换）
      3. 如果一个非数字类型的字符串相除，得到的结果是 NaN
	    4. 如果除数为0 ，得到的结果是 Infinity（无穷大） 结果也是数值类型
	
 %取余（获取余数）
	   
```

#### 赋值运算符

```javascript
 += |  -=   |  *=  |  /=  |   %= 

var  a += b ;    =====> 等价于        a = a+b;
```

#### 一元运算符

- 前置++  和 后置 ++

```javascript
如果++在变量之后，那么赋值给一个新的变量的时候，先赋值后计算
如果++在变量之前，那么赋值给一个新的变量的时候，先计算后赋值
```

- 前置-- 和 后置--

```javascript
  
```


#### 比较运算符

```javascript
1.   >  
    
2.   <
    
3.   >=     大于 或者 等于，只要有一个满足即可
    
4.   <=     小于 或者 等于，只要满足一个即可

5.  ==      只用来比较变量中的值是否相等，不考虑数据类型
    
6.  ===     用来判断值和数据类型必须同时相等
    
7.  !=	    判断值是否不相等，不考虑数据类型
 
8.  !==      判断值和数据类型
    
    
☞ 总结：
	  ✔ 通过比较运算符得到的结果只有两个结果，一个是正确的，一个是错误的
    ✔ 通过比较运算符得到的结果 只有 true[正确] 和 false[错误]
```

#### 逻辑运算符

```javascript
 1.   ||  或： 条件只要有一个满足即可
      总结：
      	1. 如果条件中有一个结为true(代表有一个条件满足了)，那么通过或运算后最后的结果为true
        2. 如果条件中结果都不满足，那么通过或运算后结果为false
     
 2.   &&  且： 要求所有的条件都必须满足才可以
 	  总结：
	      1. 如果条件都为真（true），那么通过且运算后最后的结果也是真（true）
        2. 如果条件中自少有一个条件不满足（false），那么通过且运算后的结果为false
     
 3.   !	  非（取反） : 
```

#### 运算符优先级（了解）

```javascript
优先级从高到底
	1. ()  优先级最高
	2. 一元运算符  ++   --   !
	3. 算数运算符  先*  /  %   后 +   -
	4. 关系运算符  >   >=   <   <=
	5. 相等运算符   ==   !=    ===    !==
	6. 逻辑运算符 先&&   后||
	7. 赋值运算符
```
## 条件判断

> #### 语法

```javascript
☞   if ( 条件表达式【布尔类型的结果】 ) { 
       
   	    逻辑代码。。。
       
     }else {
       
         逻辑代码。。。
     } 


☞  if ( 条件表达式 ) {
    
	}else if ( 条件表达式 ) {
    
    }else {
        
    }

  执行过程：
  	1. 如果第一个条件满足（true）,程序只会执行第一个if中的代码，后面的代码不会执行
		2. 如果第一个条件不满足，那么看第二个条件是否满足，如果满足，程序只会执行第二if中的代码，后面的代码不执行，如果条件不满足，那么继续往下判断下一个条件是否满足
```

> #### 执行过程

```javascript
1.  先判断if中的条件是否满足（true | false）,如果结果是true,那么程序只会执行if后面的功能代码，不会执行else中的代码

2.  如果条件表达式得到的结果是 false(条件不满足)，那么程序会进入else中执行对应的代码，不会执行if语句中的代码
```

### 三元运算

> #### 语法

```
   表达式 ?  结果1 ：  结果2 
```

> #### 执行过程

```
   1. 先判断表达式结果是否为true
   2. 如果结果为true 那么执行 问号后面第一个代码块
   3. 如果结果为false,那么执行冒号后面的代码
   
   注意：
   	   ？   相当于   if
   	   :    相当于   else
   	   1. 如果在程序中想要实现一个简单的条件判断，那么可以考虑使用三元表达式替代if条件判断
```

### switch语句

> #### 语法

```javascript
switch ( 变量 ) {
    case  值1:
        代码语句..
     break;
        
    case  值2:
        代码语句...
    break;

    default:    
    break;
}
```

> #### 执行过程

```javascript
 总结：
	1. 如果在程序中要表示一个范围，那么推荐使用条件判断
  2. 如果程序中表示的是一个具体的值， 可以用switch语句
```

## 循环

```javascript
  ☞ 反复的再做一件事情。
```

- ### while循环

> #### 语法

```javascript
while (条件表达式) {
    循环体（各种功能代码）
}
```

> #### 执行过程

```javascript
1.先判断条件表达式的结果是否为true
1. 如果条件表达式的结果为true,那么执行循环体中的代码
2. 如果条件表达式的结果为false,程序就不会执行循环体中的代码
```

- ### do .. while 循环

> #### 语法

```javascript
do {
    循环体代码
}while（条件表达式）;
```

> #### 执行过程

```javascript
1.  先执行一次循环体代码
2.  执行第一次循环体代码后，要进行条件判断，如果为true，继续执行循环体中代码，如果条件为false，循环体中的代码不再执行
 区别：	
 	1. 如果条件不满足，do while循环会比while循环多一次
  2. 如果条件满足，那么do while循环和while循环执行次数是一样的
```

### for循环

#### 语法

```javascript
 ☞  如果能够确定循环次数，推荐使用for循环。
 
 for ( 变量初始化; 条件判断（范围判断）;  变量自增（自减） ) {
      循环体代码
 }
 
```

### 执行过程

```javascript
  1. 先执行变量初始化
  2. 条件判断，是否为true
  3. 如果条件为true,那么执行循环体中的代码
  4. 变量自增或自减
  5. 继续判断条件是否成立，如果成立执行代码
```

### continue语句

#### 特点

```javascript
1. 当代码执行continue的时候，本次循环后面的代码不再执行，会进入到下一次循环中
```

### break语句

#### 特点

```javascript
 1. 当代码执行到break的时候，会跳转整个循环，后面的代码不再执行。
```

## 数组

> ### 创建数组
>
> - #### 字面量创建数组 
>
>   ```javascript
>     var  自定义数组名称 = [] ;
>   ```
>
> - #### 构造函数创建数组 
>
>   ```javascript
>      var  自定义数组名称  = new Array();
>   ```
>
> ### 数组赋值
>
> - #### 创建数组并赋值
>
>   ```javascript
>     ☞ 构造函数方式
>     	  var  ary = new  Array (1,2,3,5,6);
>   
>     ☞ 字面量方式赋值
>     	 var  ary = [1,2,3,4,6];
>   ```
>
> - #### 通过索引方式赋值
>
>   ```javascript
>       var  ary = [];
>   	ary[0]=1;
>   	ary[1]=2;
>   
>   总结：
>   	 1. 数组中索引值是从 0 开始的
>      2. 通过索引的方式给数组赋值，要按照顺序个数设置
>      3. 通过  数组名.length 可以获取到当前数组的长度
>   ```
>
> #### 获取数组中的值
>
> ```javascript
>    ☞  通过索引的方式获取数组中的值，数组的索引从0开始
>    
>    ☞  语法：
> 	    数组名[索引号]
>    
>    例如：
> 	   var  ary = [1,2,3,4,5];
> 	   ary[0];
> 	   ary[1];
> ```
>
> ### 数组遍历
> ### 冒泡排序

> ```javascript
> 冒泡排序，从小到大  
> 冒泡排序：  
> 将两个相邻的数字进行比较，如果第一个数比第二个数大，就交换，一直比较到最后，将把最大值移动到数组
```

## 函数

> #### 函数的概念

```javascript
  函数： 可以封装一段特定功能代码，然后通过函数名调用，实现对该段代码重复使用
  
  	✔ 封装（把散开的代码写到一个集体中）
    ✔ 重复使用
    
```

> #### 函数的作用

```javascript
   实现代码的重复使用。
```

#### 创建函数

> #### 方式一： 函数声明及执行方式（推荐）
>
> ```javascript
> ☞ 函数的声明：
>
> function  自定义函数名() {
>     
>     具体的功能代码
>   
> }
> 注意：
> 	 1. 由于函数是用来实现某种特定功能代码，所以一般我们设置函数名的时候，以动词开始。
>    2. 函数不能自己执行代码，需要通过函数名调用实现代码的执行
>      
>  
>  ☞ 调用函数（执行函数）
>  
>      函数名();  //函数的调用
> ```
>
> #### 方式二：函数表达式（字面量）及执行方式（了解）
>
> ```javascript
> var  fn = function () {
>     
> }   
>
> fn();
> ```

#### 函数的参数

> #### 形参
>
> ```javascript
> 在 函数创建时，在小扩号中定义的变量
>
> 语法：
> function 函数名(形参,形参,形参...) {//形参，就是一个占位符，命名规则和规范和变量一样
> 	//函数体
> }
>
>
> 注意：
> 	  1 函数也可以做为参数进行传递
> ```
>
> #### 实参
>
> ```javascript
> 实参，在函数调用时，在小扩号中所传入的实际的数据。
>
> 语法：
>   函数名(数据,数据,数据...);   //实参，就是实际的数据
> ```

#### 函数的返回值

> #### 返回值：函数执行完后，可以把执行的结果 通过 **return 语法** 返回给 调用者
>
> ```javascript
> function add(num1，num2){
>     //函数体
>     return num1 + num2; // 注意：return 后的代码不执行
> }
> var resNum = add(21,6); // 调用函数，传入 两个实参，并通过 resNum 接收函数返回值
> alert(resNum);// 27
>
> 注意：
>     1. 如果函数没有显示的使用 return语句 ，那么函数有默认的返回值：undefined
>     2. 如果函数中写了return语句，后面没有写任何其他内容，那么函数的返回值依然是 undefined
>     3. 一个函数只能有一个返回值
>     4. return 代码执行完成后，后面的代码不再执行
>     5. 函数也可以作为返回值（理解）
> ```

## 函数其他部分

#### arguments的使用
     
☞ 通过 arguments获取到函数参数的个数 【不确定函数到底有多少个参数】

☞ 总结：
	1. 如果函数参数不确定，可以定义函数的时候不写参数，通过arguments获取
  2. 如果函数的参数确定，那么推荐定义函数的时候写参数


#### 匿名函数和自调用函数

```javascript
☞ 匿名函数： 没有函数名的函数
例如：
var  fn = function () {
    
}

☞总结：
	1. 匿名函数不能单独使用
  2. 可以将匿名函数赋值给一个变量
  3. 可以让匿名函数自己调用自己（自调用函数【匿名函数】）


☞ 自调用函数： 函数封装好，立即执行。
	总结：
    	1. 自调用函数必须是匿名函数
      2. ( function () {} )(); 
☞ 函数属于一种数据类型
☞ 函数作为参数
☞ 函数可以为返回值
```

## 函数作用域及局部变量

> #### 作用域
>
> ```javascript
>
>  作用域： 变量或者函数可以起作用的区域
>  
>  ◆ 全局作用域（全局变量）
>  	  1， 在script标签中或者js文件中定义的变量，在任何地方都可以访问
>     2,  在函数内部声明变量不使用var关键字 （不建议使用）
>       
>  ◆ 局部作用域（局部变量）
>  	  1， 在函数内部定义的变量
> 	  2， 局部变量只能在定义变量的函数中使用
>       
>  ◆ 块级作用域 （目前所学版本没有，新版本语义中有块级作用域）
>        {
>           块级作用域
>        }  
>  	   1. 本质上块级作用域中的变量在外部不能访问
>      2. 但是在js中可以访问块级作用域的变量（证明js没有块级作用域）
> ```
>
> #### 全局作用域（全局变量）
>
> ```javascript
> 声明在所有函数外部的变量，可以所有地方使用
>
> 案例：
> 	说出下列代码的运行结果？
> 	
> ```
>
> #### 局部作用域（局部变量）
>
> ```javascript
> 声明在某个函数内部的变量或函数的形参，只能在函数内部使用
>
> ```

#### 作用域链

```javascript
作用域链：
	当访问一个变量时，会先从本作用域中去找这个变量，若找不到则向上一级作用域中去找，依次类推，就形成了一个作用域链。

    
案例代码分析：
    var a = 1;
    function fn1(){
      var a = 2;
      function fn2(){
          console.log(a);   //a的值 
      }
      fn2()
    }
    fn1();

```

#### 作用域案例分析

```javascript

1. 分析代码执行结果
function  f1 () {
    var num = 123;
    function f2 () {
        console.log( num );//123
    }
    
    f2 ();
} 
var  num = 456;
f1();
```

#### 预解析

```javascript
☞  思考1
	var num = 5; 
	console.log( num );

☞  思考2
	console.log( num );
    var  num = 5;

预解析：
	1. js 代码执行先执行预解析
  2. 先进行变量提升： 把变量声明提升到当前作用域的最上面，不包括变量的赋值
  3. 函数提升： 把函数声明提升到当前作用域的最上面，不包括函数的调用
    
预解析案例分析：
1. 
var  a  = 25;
function abc () {
    alert(a);
    var a = 10;
}

abc();
自己写
var a;
function abc () {
  var a;
  alert(a);弹出a的值为undefined;
  a = 10;
}
abc()
a = 25;

2. 
console.log(a)
function a () {
    console.log("aa");
}

var a = 1;
console.log(a);



自己写
function a () {
  console.log('aa');
}
var a;
console.log(a);
a = 1;
console.log(a);



注意：
	 1. 如果函数名和变量名一样，函数优先

3 var  a  = 18;
f1();
function f1 () {
    var b = 9;
    console.log(a);
    console.log(b);
    var a = 123;
}

自己写
var a;
function f1() {
  var b;
  var a;
   b=9;
  console.log(a);未定义
  conslol.log(b);9
  a=123
}
a = 18;
f1();

4.
f1();
console.log(c);
console.log(b);
console.log(a);
function f1 () {
    var a = b = c = 9;
    console.log(a);
    console.log(b);
    console.log(c);
}

自己写
function f1 () {
      var a ；
      a = 9
      b= 9 两个是全局变量没有加var
      c= 9
    console.log(a);
    console.log(b);
    console.log(c);
   a = 9
 
}
f1();
console.log(c);
console.log(b);
console.log(a);

```

## 对象
> ### 什么是对象？
>
> ```javascript
>  ☞ 总结：
> 	  1. 程序中的对象：
>       	✔ 对象必须有对应的属性【描述对象的特点，在程序中一般使用名词描述】
>         ✔ 对象必须有行为动作方法 【方法用来描述具体对象的行为动作，一般方法使用动词】
>       	
> ```
>
> ### 对象字面量创建对象
>
> ```javascript
>  ☞ 通过字面量方式创建对象
>  	
>  	 var  变量名  =  {  key: value, key: value,  key: functon () {}  };
> 
> 
> 备注：
> 	1. 创建对象，必须要确定具体的事物
>   2. 创建对象，必须要确定对象有哪些属性【特征】或者方法【动作，行为】
>   3. 如果一次想要输出多个对象，那么可以将每一个对象放到一个数组中。
>     
>  ☞ 访问对象属性    （对象.属性   |  对象['属性名']）
>  ☞ 访问对象方法    （对象.方法名）
> 
>  注意：
>  	 1、 如果通过  对象['属性名']访问对象的属性时候，必须保证使用字符串格式
> ```
>
> ### 通过构造函数创建对象
>
> ```javascript
>  ☞   var  obj  =  new Object();
>        obj.name = "";
>        obj.eat = function() {
>
>        }
>      obj.eat() //调用方法
>      1. Object 是一个构造函数
>      2. 通过new调用构造函数
>      
>      
> ☞ 添加属性：
> 	 对象变量.属性名 = 值;
> 
> ☞ 添加方法：
>    对象变量.方法名 =  function () {}
> ```
>
> ### 工厂方式创建对象
>
> ```javascript
>  
>  function  create ( name, age, height ) {
>      var  Ob = new Object()
>      	  Ob.name = name;
>      	  Ob.age = age;
>      	  Ob.height = height;
>      	  Ob.eat = function () {}
>      
>       return Ob;
>  }
>  var zs = create('zs',12,12)
> ```
>
> ### 自定义构造函数创建对象
>
> ```javascript
>  ☞ 使用帕斯卡命名法 （每个单词首字母大写）
>  
>  ☞ 例如：
>     function  CreateHero ( name, age, height ) {
>          this.name = name;
>          this.age = age;
>          this.height = height;
>     }
>     var zs = new People('zs',15.111)
> ```
>
> ### new 关键字执行过程
>
> ```
> 1. 执行new开始启动构造函数
> 2. 将实参传递给形参
> 3. 【this指向创建好的对象】
> 4. 【返回对象】
> 
> 注意：
> 	 1. 在构造函数中，默认的返回值就是当前创建的对象
> ```
>
> ### this关键字
>
> ```
> 1. 函数中的this         指向Window
> 2. 在方法中的this	   指向当前方法所属的对象
> 3. 在构造函数的this	  指向创建的对象
> 
> 总结：
> 	 谁调用函数，this就指向谁
> ```
>
> ### 遍历对象删除对象属性
>
> ```javascript
> ☞ 通过   for   in  遍历 对象的成员
> 
> ☞ 遍历对象中的属性
> 
> ☞ 遍历对象中的值
> ```
>
> ### 检测对象的数据类型
>
> ```javascript
> 对象  instanceof  构造函数
> ```

##数据存储
#### 简单数据类型在内存中的存储

```javascript
  ☞ 简单数据类型（值类型） 存储在内存的 栈 上
  
  ☞ Number  String   Boolean  Null Undefined
  ☞ 分析简单数据类型在内存中的存储方式
  	var  n1 = 10;
	  var  n2 = n1;

```

#### 复杂数据类型在内存中的存储

```javascript
  ☞ 复杂数据类型（引用类型） 存储在内存的 堆 上
  
  ☞  Object | Array | 函数
```

### 简单数据类型作为函数的参数在内存存储

```javascript
 ☞  分析案例代码
 
 function  fn ( a, b ) {
      a = a+1;
      b = b+1;
      console.log( a );
      console.log( b );
 }

 var  x = 10；
 var  y = 5;

 fn(x, y);

 console.log( x, y );   思考：x ， y 的值是多少？
```

### 复杂数据类型作为函数的参数在内存存储

```javascript
  ☞ 
  
  function Person ( name, age ) {
       this.name =  name; 
       this.age = age;
       this.sayHi = function () {
          console.log( "你好" );
       }
  }

   var p1 = new Peron( "张三", 18 );

    function getperson ( person ) {
		
          person.name = "李四";
        
    }

	getperson( p1 );

    console.log( p1.name );   思考： p1 的name值是什么？

```

## 课堂案例

```javascript 
☞ 
function Person ( name, age ) {
    this.name = name;
    this.age = age;
    this.sayHi = function () {
        console.log( "你好" );
    }
}


var p1 = new Person(" 张三 ", 18);
function getperson ( person ) {
    person.name = "李四";
    person = new Person("王五",20);
    console.log(person.name);  
}

getperson(p1);
console.log(p1.name);    思考： p1.name 输出的结果是什么？


☞  数组作为参数

function getary ( ary ) {
    ary[0] = -1;
}

var newary = [1,2,3];

getary( newary );

console.log( newary[0] );
```

## 内置对象介绍

```javascript
☞  JavaScript组成：   ECMAScript  |   DOM   |  BOM

☞  ECMAScript：  变量 ， 函数， 数据类型 ，流程控制，内置对象。。。

☞  js中的对象： 自定义对象 ， 内置对象 ， 浏览器对象（不属于ECMAScript）

☞  Math对象，Array对象，Date对象。。。。

### Math对象

```javascript
  ☞ 提供了一系列与数学相关的方法或属性  ( 静态  |  实例)
  
  ☞ Math.PI          获取圆周率【属性】 
  ☞ Math.random()    返回大于等于0小于1之间的随机数
  
  
  ☞ Math.floor() 	 向下取整，返回一个小于当前数字的整数
  ☞ Math.ceil()	     向上取整，返回一个大于当前数字的整数
  
  
  ☞ Math.round()     四舍五入（小数如果小于0.5,返回小于当前数字的整数，如果小数部分大于0.5返回大于当前数字的一个整数）
  ☞ Math.abs()		取绝对值（返回当前数字的绝对值，正整数）
  
  ☞ Math.max()       返回一组数中的最大值 （可以设置多个参数，返回其中最大值，参数不可以是数组）
  ☞ Math.min()       返回一组数中的最小值 （可以同时设置多个参数，与最大值效果一样）
  
  ☞ Math.sin(x)	     返回一个正弦的三角函数 ( 注意： x 是一个以弧度为单位的角度)
  ☞ Math.cos(x)	     返回一个余弦的三角函数 （注意： x 参数是一个以弧度为单位的角度）
  
  
  	记住角度和弧度之间的关系
   		   //已知角度求对应的弧度
			function aTor(angle) {
				return angle*Math.PI/180
			}

			//已知弧度求对应的角度
			function rToa (rotate) {
				return rotate*180/Math.PI
			}
  
  ☞ Math.pow(x,y)	 返回x的y次幂
```

### 静态成员和实例成员

```javascript
 ☞静态成员：  
 	    1. 不需要通过构造函数创建对象且能访问对象中的属性或方法
        
 ☞实例成员： 
    	1.  首先必须通过构造函数创建对象
      2.  通过构造函数创建对象并访问的属性或方法[实例成员]
```

### Date对象

```javascript
☞ Date是一个构造函数，必须通过 new Date() 创建一个实例成员才能使用

☞ 用法一：空构造函数
   var d = new Date();
   ☞GMT 格林威治时间（0时区）

☞ 用法二：在构造函数中传入毫秒值
   var d = new Date(d.valueOf());

☞ 用法三： 传入日期格式的字符串
  var  d = new Date("1988-8-8")

☞ 用法四： 传入数字
  var  d = new Date(year, month[,day,time,second]);  //必须设置年和月
  备注： 月份从0 开始， 0 代表1月


☞ 获取当前时间的毫秒值：
	d.valueOf()  
  d.getTime()  // 推荐使用
  Date.now()   //H5 新方法 有兼容信息
```

### Date中的方法

```javascript
☞ 日期格式化方法
var d = new Date();
    d.toString();  //转化成字符串
    d.toDateString();  //转换成日期字符串
    d.toTimeString();  //转换成时间字符串
    d.toLocaleDateString();   //返回本地的日期格式  （不同浏览器不同效果）
    d.toLocaleTimeString();   //返回本地的时间格式  （不同浏览器不同效果）


☞ 获取日期其他部分
	d.getSeconds()  //获取秒
    d.getMinutes()  //获取分钟
    d.getHours()    //获取小时
    d.getDay()      //返回周几   （0表示周日）
    d.getDate()     //返回当前月的第几天
    d.getMonth()    //返回月份   （从0开始）
    d.getFullYear()  //返回年份
```

#### Data对象案例

```javascript
 ☞ 写一个函数，格式化日期对象，返回 yyyy-mm-dd HH:mm：ss 形式
 
 ☞ 写一个函数计算时间差，返回相差的天/时/分/秒  【求 2008年8月8日到今天】
```

### 数组对象

#### Array基本使用

```javascript
 ☞  创建数组的方式
 		✔ 通过字母量方式创建
    ✔ 通过构造函数
        
 ☞  数组中常用的属性
 	  数组.length  获取数组长度
 
 ☞  清空数组的方式
 		✔ 给数组赋值为null
    ✔ 给数组赋值为空
    ✔ 可以将数组的长度设置为0
```

### Array中的方法

```javascript
  ☞  toString()   // 把数组转换为字符串，使用逗号分隔
  ☞  valueOf()   //  返回数组对象本身

  ☞ 栈方法(先进后出)
   ary.push()   // 该方法有一个返回值，表示数组最新的长度，该方法中可以设置多个参数
	 ary.pop()    //返回数组中最后一个字，且会修改数组的长度

  ☞ 队列方法(先进先出)
	 ary.shift() 		//取出数组中的第一个元素，修改数组的长度
	 ary.unshift(number)  //在数组中最开始位置添加一个值

   ☞ 排序方法
   	ary.reverse()  // 翻转数组
	  ary.sort()	//数组排序  默认是从字符编码排序的

	  备注:
			自定义排序规则:
            function compare (a, b) {
                	//升序排列
                    return  a-b;
            }
			
 		    function compare1 (a, b) {
                	//降序排列
                    return  b-a;
            }
		
   ☞ 其他方法汇总
◆ concat()  //把两个数组拼接到一块,返回一个新数组
◆ slice(startindex, endindex)   //从当前数组中截取一个新的数组 
	✔ 第一个参数表示开始索引位置,第二个参数代表结束索引位置
◆ splice(startindex, deletCont, options)  //删除或者替换数组中的某些值
	✔ 第一个参数代表从哪开始删除
  ✔ 第二个参数代表一共删除几个
  ✔ 第三个参数代表要替换的值
◆ indexOf(content[,index])   //没找到返回-1
	✔ 找数组中的某个值,如果找到返回索引位置,如果没有找到返回-1
◆lastIndexof()  从数组的末尾开始找,如果找到,返回索引位置,如果没有找到返回-1
◆ Join()   //将数组中的每一个元素通过一个字符链接到一块
◆ 数组遍历
  filter(function(item,index, ary) {})   //返回一个新数组,可以获取赛选结果
	map(function(item,index,ary) {})  //遍历数组,返回一个新数组
	forEach(function(item,index, ary) {}) //遍历数组,没有返回值
```

### 基本包装类型(了解)

```javascript
☞  对象具有属性和方法（复杂类型），简单类型不具有属性和方法

☞  基本包装类型：
	   1. String | Number  | Boolean   ----构造函数
    例如：
      var s1 = 'adsfafd';		   ---简单类型的字符串
			var  s2 = new String('asdaf'); ----复杂类型的对象（字符串）
	   1. 推荐使用基本包装类型中的String，不推荐使用 Number | Boolean
```

### 字符串

#### 特性

```javascript
 ☞ 不可变性
 ☞ 注意: 尽量不要大量的拼接字符串
```

#### 字符串中的方法

```javascript
 ☞ 字符方法
1. charAt(index)  	//获取指定位置处的字符
2. str[index]		   //获取指定位置的字符 （H5中的方法）

 ☞ 字符串方法
1. concat()   //拼接字符串  等效于 +
2. slice(strat,end)       //从指定位置开始，截取字符串到结束位置，end值取不到
3. substring(start,end)   //从指定位置开始，截取字符串到结束位置， end值取不到
4. substr(start,length)   //从指定位置开始，截取length长度个字符


  ☞ 位置方法
1. indexOf(字符)   //返回字符在字符串中的位置
2. lastIndexOf(字符)  //从后往前找，只找第一个匹配的字符

  ☞ 去除空白
trim()      //只能去除字符串前后空白

  ☞ 大小写转换法
toLocaleUpperCase()  //转化为大写
toLocaleLowerCase()  //转化为小写

  ☞其他
replace(a,b)  // 用b替换a
split()   //	以一个分割符,将一个字符串串分割成一个数组
```

