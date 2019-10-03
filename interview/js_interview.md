### 1 split 和 join 的区别
   * Split()方法用于把一个字符串分割成字符串数组.   
     stringObject.split(a,b)这是它的语法  
     a是必须的决定个从a这分割  
     b不是必须的，可选。该参数可指定返回的数组的最大长度 。  
     如果设置了该参数，返回的子串不会多于这个参数指定的数组。如果没有设置该参数，整个字符串都会被分割，不考虑它的长度。
     注意返回的数组中不包括a本身。
--------------------- 
   * Join()方法是将数组转换成字符串。  
      1.join() 方法用于把数组中的所有元素放入一个字符串。  
      元素是通过指定的分隔符进行分隔的。  
      指定分隔符方法join("#");其中#可以是任意.  

### 2 详细介绍了解的for循环 
  ##### 一 for 
* 1 for循环中的i在循环结束之后任然存在于作用域中，因为ECMAScript中不存在块级作用域，即使i是在循环内部定义的一个变量，但在循环外部仍然可以访问到它，所以为了避免影响作用域中的其他变量，使用函数自执行的方式将其隔离起来()();
* 2 避免使用for(var i=0; i<demo1Arr.length; i++){} 的方式，这样的数组长度每次都被计算，效率低于上面的方式。也可以将变量声明放在for的前面来执行，提高阅读性；  
    1 var i = 0, len = demo1Arr.length;
    2 for(; i<len; i++) {};
* 3 跳出循环的方式有如下几种
    return 函数执行被终止
    break 循环被终止，退出当前循环
    continue 循环被跳过，即退出当次循环，继续下一次循环
    
  ##### 二 for in
*    for(var item in arr|obj){} 可以用于遍历数组和对象
    遍历数组时，item表示索引值， arr表示当前索引值对应的元素 arr[item]
    遍历对象时，item表示key值，obj表示key值对应的value值 obj[item]

  ##### 三 foreach 
* demoArr.forEach(function(arg) {}) arg表示数组中的每一项元素
* 注意事项：
* 回调函数中有2个参数，分别表示值和索引，这一点与jQuery中的$.each相反
* forEach无法遍历对象
* forEach无法在IE中使用，firefox和chrome实现了该方法
* forEach无法使用break，continue跳出循环，使用return时，效果和在for循环中使用continue一致
* 最重要的一点，可以添加第二参数，为一个数组，而且回调函数中的this会指向这个数组。而如果没有第二参数，则this会指向window。
  
```js
var newArr = [];
demoArr.forEach(function(val, index) {
     this.push(val); // 这里的this指向newArr
 }, newArr) 
```

  ##### 四 do/while

  ##### 五 $.each
 * $.each(demoArr|demoObj, function(e, ele))
 * 注意事项：
* 使用return 或者return true为跳过一次循环，继续执行后面的循环
* 使用return false为终止循环的执行，但是并不终止函数执行
* 无法使用break与continue来跳过循环

  ##### 六 $(selecter).each 专门用来遍历DOMList


### 3 js如何检测变量是字符串类型，写出函数实现

```js
function a(obj){
   return typeof(obj)=="string";
}
alert(a(123));
alert(a("abc"));

function b(obj){
   return obj.constructor === String
}
alert(b(123));
alert(b("abc"));

function type(data){
   return Object.prototype.toString.call(data).slice(8,-1).toLowerCase();
}
alert(type(123));
alert(type("abc"));
--------------------- 
```

### 4 如何让判断Js数据类型
typeof、instanceof、 constructor、 prototype方法比较
  > 1.使用typeof操作符

    (1) undefined：如果这个值未定义
    (2) boolean：如果这个值是布尔值
    (3) string：如果这个值是字符串
    (4) number：如果这个值是数值
    (5) object：如果这个值是对象或null
    (6) function：如果这个值是函数

    需要注意：typeof不适合用于判断是否为数组。当使用typeof判断数组和对象的时候，都会返回object
          可以使用isArray()来判断是否为数组。

  > 2.instanceof

    instanceof 运算符用来判断一个构造函数的prototype属性所指向的对象是否存在另外一个要检测对象的原型链上。需要区分大小写。
    简单的来说，instanceof 用于判断一个变量是否某个对象的实例。

```js
　　    var arr = new Array( );
　　　　alert(arr instanceof Array);   // 返回true
 ```
　　注意：instanceof只能用来判断对象和函数，不能用来判断字符串和数字等。判断它是否为字符串和数字     时，只会返回false。

   > 3.constructor

     constructor 属性返回对创建此对象的数组函数的引用。  
     在JavaScript中，每个具有原型的对象都会自动获得constructor属性。

```js
// String
var str = "字符串";
alert(str.constructor); // function String() { [native code] 这是JavaScript的底层内部代码实现，无法显示代码细节。　　}
alert(str.constructor === String); // true

// Array
var arr = [1, 2, 3];
alert(arr.constructor); // function Array() { [native code] }
alert(arr.constructor === Array); // true

// Number
var num = 5;
alert(num.constructor); // function Number() { [native code] }
alert(num.constructor === Number); // true
```

  > 4.prototype

    以上三种方法多少都会有一些不能判断的情况。为了保证兼容性，可以通过Object.prototype.toString方法，判断某个对象值属于哪种内置类型。

```js
// 注意区分大小写
alert(Object.prototype.toString.call(“字符串”) === ‘[object String]’) -------> true;
alert(Object.prototype.toString.call(123) === ‘[object Number]’) -------> true;
alert(Object.prototype.toString.call([1,2,3]) === ‘[object Array]’) -------> true;
alert(Object.prototype.toString.call(new Date()) === ‘[object Date]’) -------> true;
alert(Object.prototype.toString.call(function a(){}) === ‘[object Function]’) -------> true;
alert(Object.prototype.toString.call({}) === ‘[object Object]’) -------> true;

```

### 5 原型
 * 构造函数有一个属性是原型，该原型是一个对象，里面有constructor和-Proto-两个属性
 * 使用构造函数创建的所有对象，都可以访问该构造函数原型对象上的成员，所以可以把所有对象共享的成员，放到构造函数的原型对象上
 * 对象的原型 
     student {name:"zs",age:18}
       age:18
       name:zs
       _proto_:object
 * 构造函数的原型
 * 对象可以访问到原型上的constructor，可以获取到创建该对象的类型（构造函数）


### 6 js操作数组的函数有哪些？
##### 一、concat()

concat() 方法用于连接两个或多个数组。该方法不会改变现有的数组，仅会返回被连接数组的一个副本。

```js	
var arr1 = [1,2,3];
var arr2 = [4,5];
var arr3 = arr1.concat(arr2);
console.log(arr1); //[1, 2, 3]
console.log(arr3); //[1, 2, 3, 4, 5]
```

##### 二、join()

join() 方法用于把数组中的所有元素放入一个字符串。元素是通过指定的分隔符进行分隔的，默认使用','号分割，不改变原数组。

```js	
var arr = [2,3,4];
console.log(arr.join()); //2,3,4
console.log(arr); //[2, 3, 4]
```

##### 三、push()

push() 方法可向数组的末尾添加一个或多个元素，并返回新的长度。末尾添加，返回的是长度，会改变原数组。

```js	
var a = [2,3,4];
var b = a.push(5);
console.log(a); //[2,3,4,5]
console.log(b); //4
```

push方法可以一次添加多个元素push(data1,data2....)

##### 四、pop()

pop() 方法用于删除并返回数组的最后一个元素。返回最后一个元素，会改变原数组。

```js	
var arr = [2,3,4];
console.log(arr.pop()); //4
console.log(arr); //[2,3]
```

##### 五、shift()

shift() 方法用于把数组的第一个元素从其中删除，并返回第一个元素的值。返回第一个元素，改变原数组。

```js	
var arr = [2,3,4];
console.log(arr.shift()); //2
console.log(arr); //[3,4]
```

##### 六、unshift()

unshift() 方法可向数组的开头添加一个或更多元素，并返回新的长度。返回新长度，改变原数组。

```js	
var arr = [2,3,4,5];
console.log(arr.unshift(3,6)); //6
console.log(arr); //[3, 6, 2, 3, 4, 5]
```

tip:该方法可以不传参数,不传参数就是不增加元素。

#####  七、slice()

返回一个新的数组，包含从 start 到 end （不包括该元素）的 arrayObject 中的元素。返回选定的元素，该方法不会修改原数组。

```js	
var arr = [2,3,4,5];
console.log(arr.slice(1,3)); //[3,4]
console.log(arr); //[2,3,4,5]
```

##### 八、splice()

splice() 方法可删除从 index 处开始的零个或多个元素，并且用参数列表中声明的一个或多个值来替换那些被删除的元素。如果从 arrayObject 中删除了元素，则返回的是含有被删除的元素的数组。splice() 方法会直接对数组进行修改。

```js	
var a = [5,6,7,8];
console.log(a.splice(1,0,9)); //[]
console.log(a); // [5, 9, 6, 7, 8]
var b = [5,6,7,8];
console.log(b.splice(1,2,3)); //[6, 7]
console.log(b); //[5, 3, 8]
```

##### 九、substring() 和 substr()

相同点：如果只是写一个参数，两者的作用都一样：都是是截取字符串从当前下标以后直到字符串最后的字符串片段。

```js	
substr(startIndex);
substring(startIndex);
var str = '123456789';
console.log(str.substr(2)); // "3456789"
console.log(str.substring(2)) ;// "3456789"
```

不同点：第二个参数

substr（startIndex,lenth）： 第二个参数是截取字符串的长度（从起始点截取某个长度的字符串）；
substring（startIndex, endIndex）： 第二个参数是截取字符串最终的下标 （截取2个位置之间的字符串,‘含头不含尾'）。

```js	
console.log("123456789".substr(2,5)); // "34567"
console.log("123456789".substring(2,5)) ;// "345"
```

##### 十、sort 排序

按照 Unicode code 位置排序，默认升序

```js	
var fruit = ['cherries', 'apples', 'bananas'];
fruit.sort(); // ['apples', 'bananas', 'cherries']
var scores = [1, 10, 21, 2];
scores.sort(); // [1, 10, 2, 21]
```

##### 十一、reverse()

reverse() 方法用于颠倒数组中元素的顺序。返回的是颠倒后的数组，会改变原数组。

```js	
var arr = [2,3,4];
console.log(arr.reverse()); //[4, 3, 2]
console.log(arr); //[4, 3, 2]
```

##### 十二、indexOf 和 lastIndexOf

都接受两个参数：查找的值、查找起始位置
不存在，返回 -1 ；存在，返回位置。indexOf 是从前往后查找， lastIndexOf 是从后往前查找。
indexOf

```js	
var a = [2, 9, 9];
a.indexOf(2); // 0
a.indexOf(7); // -1
 
if (a.indexOf(7) === -1) {
 // element doesn't exist in array
}
```
lastIndexOf
 ```js
var numbers = [2, 5, 9, 2];
numbers.lastIndexOf(2);  // 3
numbers.lastIndexOf(7);  // -1
numbers.lastIndexOf(2, 3); // 3
numbers.lastIndexOf(2, 2); // 0
numbers.lastIndexOf(2, -2); // 0
numbers.lastIndexOf(2, -1); // 3
```
##### 十三、every

对数组的每一项都运行给定的函数，每一项都返回 ture,则返回 true
```js	
function isBigEnough(element, index, array) {
 return element < 10;
} 
[2, 5, 8, 3, 4].every(isBigEnough); // true
```
##### 十四、some

对数组的每一项都运行给定的函数，任意一项都返回 ture,则返回 true
```js	
function compare(element, index, array) {
 return element > 10;
}  
[2, 5, 8, 1, 4].some(compare); // false
[12, 5, 8, 1, 4].some(compare); // true
```
##### 十五、filter

对数组的每一项都运行给定的函数，返回 结果为 ture 的项组成的数组
```js	
var words = ["spray", "limit", "elite", "exuberant", "destruction", "present", "happy"];
var longWords = words.filter(function(word){
 return word.length > 6;
});
// Filtered array longWords is ["exuberant", "destruction", "present"]
```
##### 十六、map

对数组的每一项都运行给定的函数，返回每次函数调用的结果组成一个新数组
```js	
var numbers = [1, 5, 10, 15];
var doubles = numbers.map(function(x) {
  return x * 2;
});
// doubles is now [2, 10, 20, 30]
// numbers is still [1, 5, 10, 15]
```
##### 十七、forEach 数组遍历
```js
const items = ['item1', 'item2', 'item3'];
const copy = [];  
items.forEach(function(item){
 copy.push(item)
});
```
ES6新增新操作数组的方法

##### 1、find()：

传入一个回调函数，找到数组中符合当前搜索规则的第一个元素，返回它，并且终止搜索。
```js	
const arr = [1, "2", 3, 3, "2"]
console.log(arr.find(n => typeof n === "number")) // 1
```
##### 2、findIndex()：

传入一个回调函数，找到数组中符合当前搜索规则的第一个元素，返回它的下标，终止搜索。
```js
const arr = [1, "2", 3, 3, "2"]
console.log(arr.findIndex(n => typeof n === "number")) // 0
```
##### 3、fill()：

用新元素替换掉数组内的元素，可以指定替换下标范围。
```js	
arr.fill(value, start, end)
```
##### 4、copyWithin()：

选择数组的某个下标，从该位置开始复制数组元素，默认从0开始复制。也可以指定要复制的元素范围。
```js	
arr.copyWithin(target, start, end)
const arr = [1, 2, 3, 4, 5]
console.log(arr.copyWithin(3))
 // [1,2,3,1,2] 从下标为3的元素开始，复制数组，所以4, 5被替换成1, 2
const arr1 = [1, 2, 3, 4, 5]
console.log(arr1.copyWithin(3, 1)) 
// [1,2,3,2,3] 从下标为3的元素开始，复制数组，指定复制的第一个元素下标为1，所以4, 5被替换成2, 3
const arr2 = [1, 2, 3, 4, 5]
console.log(arr2.copyWithin(3, 1, 2)) 
// [1,2,3,2,5] 从下标为3的元素开始，复制数组，指定复制的第一个元素下标为1，结束位置为2，所以4被替换成2
```
##### 5、from

将类似数组的对象（array-like object）和可遍历（iterable）的对象转为真正的数组
```js	
const bar = ["a", "b", "c"];
Array.from(bar);
// ["a", "b", "c"]
 
Array.from('foo');
// ["f", "o", "o"]
```
##### 6、of

用于将一组值，转换为数组。这个方法的主要目的，是弥补数组构造函数 Array() 的不足。因为参数个数的不同，会导致 Array() 的行为有差异。
```js	
Array() // []
Array(3) // [, , ,]
Array(3, 11, 8) // [3, 11, 8]
Array.of(7);    // [7]
Array.of(1, 2, 3); // [1, 2, 3]
Array(7);     // [ , , , , , , ]
Array(1, 2, 3);  // [1, 2, 3]
```
##### 7、entries() 返回迭代器：返回键值对
```js
	
//数组
const arr = ['a', 'b', 'c'];
for(let v of arr.entries()) {
 console.log(v)
}
// [0, 'a'] [1, 'b'] [2, 'c']
 
//Set
const arr = new Set(['a', 'b', 'c']);
for(let v of arr.entries()) {
 console.log(v)
}
// ['a', 'a'] ['b', 'b'] ['c', 'c']
 
//Map
const arr = new Map();
arr.set('a', 'a');
arr.set('b', 'b');
for(let v of arr.entries()) {
 console.log(v)
}
// ['a', 'a'] ['b', 'b']
```
##### 8、values() 返回迭代器：返回键值对的value
```js	
//数组
const arr = ['a', 'b', 'c'];
for(let v of arr.values()) {
 console.log(v)
}
//'a' 'b' 'c'
 
//Set
const arr = new Set(['a', 'b', 'c']);
for(let v of arr.values()) {
 console.log(v)
}
// 'a' 'b' 'c'
 
//Map
const arr = new Map();
arr.set('a', 'a');
arr.set('b', 'b');
for(let v of arr.values()) {
 console.log(v)
}
// 'a' 'b'
```
##### 9、keys() 返回迭代器：返回键值对的key
```js	
//数组
const arr = ['a', 'b', 'c'];
for(let v of arr.keys()) {
 console.log(v)
}
// 0 1 2
 
//Set
const arr = new Set(['a', 'b', 'c']);
for(let v of arr.keys()) {
 console.log(v)
}
// 'a' 'b' 'c'
 
//Map
const arr = new Map();
arr.set('a', 'a');
arr.set('b', 'b');
for(let v of arr.keys()) {
 console.log(v)
}
// 'a' 'b'
```
##### 10、includes

判断数组中是否存在该元素，参数：查找的值、起始位置，可以替换 ES5 时代的 indexOf 判断方式。indexOf 判断元素是否为 NaN，会判断错误。
```js
var a = [1, 2, 3];
a.includes(2); // true
a.includes(4); // false

```	
### 7 如何用原生js给一个按钮绑定两个onclick事件

### 8 js数据类型，基本数据类型有哪些
Undefined,Null,Boolean,Number,String  
有1种复杂数据类型——Object

### 9 js代码放的位置
### 10 js事件绑定的三种方法以及事件委托
1. 嵌入dom

```js
<button onclick="open()">按钮</button>
 
<script>
function open(){
    alert(1)
}
</script>
```
2. 直接绑定

```js
<button id="btn">按钮</button>
<script>
document.getElementById('btn').onclick = function(){
    alert(1)
}
</script>

```

3. 事件监听

```js
<button id="btn">按钮</button>
<script>
document.getElementById('btn').addEventListener('click',function(){
    alert(1)
})
//兼容IE
document.getElementById('btn').attachEvent('click',function(){
    alert(1)
})
</script>
```

### 11 js 中this的用法
1.在一般函数方法中使用 this 指代全局对象

```js
function test(){
　　　　this.x = 1;
　　　　alert(this.x);
　　}
　　test(); // 1
```

2.作为对象方法调用，this 指代上级对象

```js
function test(){
　　alert(this.x);
}
var o = {};
o.x = 1;
o.m = test;
o.m(); // 1
```

3.作为构造函数调用，this 指代new 出的对象

```js
function test(){
　　　　this.x = 1;
　　}
　　var o = new test();
　　alert(o.x); // 1
    //运行结果为1。为了表明这时this不是全局对象，我对代码做一些改变：
　　var x = 2;
　　function test(){
　　　　this.x = 1;
　　}
　　var o = new test();
　　alert(x); //2
```

4.apply 调用 ，apply方法作用是改变函数的调用对象，此方法的第一个参数为改变后调用这个函数的对象，this指代第一个参数

```js
var x = 0;
　　function test(){
　　　　alert(this.x);
　　}
　　var o={};
　　o.x = 1;
　　o.m = test;
　　o.m.apply(); //0
//apply()的参数为空时，默认调用全局对象。因此，这时的运行结果为0，证明this指的是全局对象。如果把最后一行代码修改为

　　o.m.apply(o); //1

```
