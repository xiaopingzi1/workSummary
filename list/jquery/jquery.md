## jQuery简介

### JavaScript库的概念

- JavaScript库
  - 把一些浏览器兼容性，或者是一些常用的函数封装到一个js文件中，就是JavaScript库
  - 我们自己封装的animate.js，就是JavaScript库
- 常见的JavaScript库： jQuery、Prototype、MooTools
  - 其中jQuery使用最流行
  - 2014年统计有57%以上的网站使用jQuery

### jQuery

- jQuery 是一个高效、精简并且功能丰富的 JavaScript 工具库。
- 它提供的 API 易于使用且兼容众多浏览器
- 方便HTML 文档遍历和操作，事件处理、动画和 Ajax 操作更加简单。

### jQuery的优点

- jQuery的宗旨
  - Write Less，Do More
- 强大的选择器
- 链式编程
- 隐式迭代
- 丰富的插件，可以自己编写插件
- 开源

### jQuery的版本

- 1.x 版本 

  - 兼容IE6,7,8

- 2.x 版本

  - 不兼容IE6,7,8

- 3.x 版本

  - 更加精简
  - 提供了精简版本，slim

  > 国内很多网站还在使用1.x版本

  - 使用JavaScript开发过程中，有许多不便之处
    - 查找元素的方法太少，麻烦。
    - 遍历伪数组很麻烦，通常要嵌套一大堆的for循环。
    - 有兼容性问题。
    - 想要实现简单的动画效果，也很麻烦
    - 代码冗余。

- 优点总结：
  - 查找元素的方法多种多样，非常灵活。
  - 拥有隐式迭代特性，因此不再需要手写for循环了。
  - 没有兼容性问题。
  - 实现动画非常简单，而且功能更加的强大。
  - 代码简单、粗暴。

### jQuery中顶级对象

jQuery中的顶级对象是$或jQuery

- 获取jQuery对象
- 入口函数

>  注意：jQuery中的$和jQuery关键字本身为同一对象；

### jQuery中页面加载事件

使用jQuery的三个步骤：

- 引入jQuery文件
- 入口函数
- 功能实现

关于jQuery的入口函数：

```javascript
// 第一种写法
$(document).ready(function() {
});
// 第二种写法
$(function() {
});
```

jQuery入口函数与window.onload的对比

- JavaScript的入口函数要等到DOM创建完毕，页面中所有资源（包括图片、文件）加载完成才开始执行。
- jQuery的入口函数只会等待文档树加载完成就开始执行，并不会等待图片、文件的加载。
- window.onload只能注册一次，jQuery入口函数可以注册多次
- jQuery的入口函数，封装了DOM中的DOMContentLoaded事件（此事件DOM加载完毕之后就执行）

$的本质

```js
console.log(typeof $);
```

​	三种常见用法，传对象、传函数、传字符串

## jQuery对象和DOM对象

### DOM对象

- 用原生JavaScript获取的DOM对象
  - 通过document.getElementById()  返回的是元素(DOM对象)


- 通过document.getElementsByTagName()获取到的是什么？
  - 伪数组(集合)，集合中的每一个对象是DOM对象

### jQuery对象

jQuery对象又可以叫做包装集(包装的DOM对象的集合)

- jQuery对象用$()的方式获取的对象
- length属性，获取对象内部的DOM元素个数

### jQuery对象和DOM对象的区别

- **jQuery对象不能使用DOM对象的成员，DOM对象不能使用jQuery对象的成员**

```javascript
// DOM对象
var box = document.getElementById('box');
// 错误
box.text('hello');
// 正确
box.innerText = 'hello';

// jQuery对象，jQuery对象加前缀$，用以区分DOM对象
var $box = $('#box');
// 错误
$box.innerText = 'hello';
// 正确
$box.text('hello');
```

### jQuery对象和DOM对象的相互转换

- DOM对象转换成jQuery对象

  把DOM对象转换成jQuery对象，让我们可以使用jQuery提供的众多的方法**方便操作**。

  - $(DOM对象) 


- jQuery对象转换成DOM对象 

  jQuery对象是包装集(集合)，从集合中取数据可以使用索引的方式

  - jQuery对象[索引值]
  - jQuery对象.get(索引值)


**总结：$常见的三种用法**

1. $('选择器')   	返回jQuery对象
2. $(DOM对象)   返回jQuery对象
3. $(function() {})   入口函数

## 选择器

- jQuery可以使用css的选择器来**获取**想要的**元素**，极大的方便了我们查找元素
  - ES5中提供的querySelector()和querySelectorAll()就是借鉴jQuery中的方式。


- jQuery选择器有很多，基本兼容了CSS1到CSS3所有的选择器

- jQuery还添加了很多更加复杂的选择器。（查看jQuery文档）

  >  注意：jQuery选择器返回的是jQuery对象。
  >
  >  jQuery选择器虽然很多，但是选择器之间可以相互替代，就是说获取一个元素，你会有很多种方法获取到。所以我们平时真正能用到的只是少数的最常用的选择器。

### jQuery基本选择器

| 名称    | 用法                | 描述                     |
| ----- | ----------------- | :--------------------- |
| ID选择器 | $('#id')          | 获取指定ID的元素              |
| 类选择器  | $('.class')       | 获取同一类class的元素          |
| 标签选择器 | $('div')          | 获取同一类标签的所有元素           |
| 并集选择器 | $('div,p,li')     | 使用逗号分隔，只要符合条件之一就可。     |
| 交集选择器 | $('div.redClass') | 获取class为redClass的div元素 |

- 总结：跟css的选择器用法一模一样。



### jQuery层级选择器

| 名称    | 用法           | 描述                              |
| ----- | ------------ | :------------------------------ |
| 子代选择器 | $('ul > li') | 使用>号，获取儿子层级的元素，注意，并不会获取孙子层级的元素  |
| 后代选择器 | $('ul li')   | 使用空格，代表后代选择器，获取ul下的所有li元素，包括孙子等 |

- 跟CSS的选择器一模一样。



### jQuery过滤选择器

- 这类选择器都带冒号:

| 名称       | 用法                              | 描述                                                         |
| ---------- | --------------------------------- | :----------------------------------------------------------- |
| :eq(index) | $('li:eq(2)').css('color', 'red') | 获取到的li元素中，选择索引号为2的元素，索引号index从0开始。equal |
| :odd       | $('li:odd').css('color', 'red')   | 获取到的li元素中，选择索引号为奇数的元素                     |
| :even      | $('li:even').css('color', 'red')  | 获取到的li元素中，选择索引号为偶数的元素                     |

### jQuery筛选选择器(方法)

- 筛选选择器的功能与过滤选择器有点类似，但是用法不一样，筛选选择器主要是方法。

| 名称                 | 用法                                       | 描述                     |
| ------------------ | ---------------------------------------- | :--------------------- |
| children(selector) | $('ul').children('li')                 | 相当于('ull > i')，子类选择器 |
| find(selector)     | $('ul').find('li')                     | 相当于('ul li'),后代选择器   |
| siblings(selector) | $('#first').siblings('li')               | 查找兄弟节点，不包括自己本身。        |
| parent()           | $('#first').parent()                     | 查找父亲                   |
| eq(index)          | $$('li').eq(2)              | 相当于 $$​('li:eq(2)'),index从0开始 |                        |
| next()             | $('li').next()                           | 找下一个兄弟                 |
| prev()             | $('li').prev()                           | 找上一次兄弟                 |

## jQuery样式操作

### CSS操作

- 功能：设置或者修改样式，操作的是style属性。

- 操作单个样式

```javascript
// name：需要设置的样式名称
// value：对应的样式值
$obj.css(name, value);
// 使用案例
$('#one').css('background','gray');// 将背景色修改为灰色
```

- 设置多个样式

```javascript
// 参数是一个对象，对象中包含了需要设置的样式名和样式值
$obj.css(obj);
// 使用案例
$('#one').css({
    'background-color':'gray',
    'width':400,
    'height':400
});
```

- 获取样式

```javascript
// name:需要获取的样式名称
$obj.css(name);
// 案例
$('div').css('background-color');
```

**注意**：获取操作的时候，如果是多个元素，那么只会返回第一个元素的值。

隐式迭代：

1. 设置操作的时候，如果是多个元素，那么给所有的元素设置相同的值

### class操作

- 添加样式类

```javascript
// name：需要添 加的样式类名，注意参数不要带点.
$obj.addClass(name);
// 例子,给所有的div添加one的样式。
$('div').addClass('one');
```

- 移除样式类

```javascript
// name:需要移除的样式类名
$obj.removeClass('name');
// 例子，移除div中one的样式类名
$('div').removeClass('one');
```

- 判断是否有某个样式类

```javascript
// name:用于判断的样式类名，返回值为true false
$obj.hasClass(name)
// 例子，判断第一个div是否有one的样式类
$('div').hasClass('one');
```

- 切换样式类

```javascript
// name:需要切换的样式类名，如果有，移除该样式，如果没有，添加该样式。
$obj.toggleClass(name);
// 例子
$('div').toggleClass('one');
```


## jQuery操作属性

### attr操作

- 设置单个属性

```javascript
// 第一个参数：需要设置的属性名
// 第二个参数：对应的属性值
$obj.attr(name, value);
// 用法举例
$('img').attr('title','哎哟，不错哦');
$('img').attr('alt','哎哟，不错哦');
```

- 设置多个属性

```javascript
// 参数是一个对象，包含了需要设置的属性名和属性值
$obj.attr(obj)
// 用法举例
$('img').attr({
    title:'哎哟，不错哦',
    alt:'哎哟，不错哦',
    style:'opacity:.5'
});
```

- 获取属性

```javascript
// 传需要获取的属性名称，返回对应的属性值
$obj.attr(name)
// 用法举例
var oTitle = $('img').attr('title');
alert(oTitle);
```

- 移除属性

```javascript
// 参数：需要移除的属性名，
$obj.removeAttr(name);
// 用法举例
$('img').removeAttr('title');
```

**案例**：美女相册

### prop操作

- 在jQuery1.6之后，对于checked、selected、disabled这类boolean类型的属性来说，不能用attr方法，只能用prop方法。

```javascript
// 设置属性
$(':checked').prop('checked', true);
// 获取属性
$(':checked').prop('checked');// 返回true或者false
```


### val()/text/()html()

```javascript
$obj.val()		获取或者设置表单元素的value属性的值
$obj.html() 	对应innerHTML
$obj.text()		对应innerText/textContent，处理了浏览器的兼容性
```

## jQuery动画

- jQuery提供了三组基本动画，这些动画都是标准的、有规律的效果，jQuery还提供了自定义动画的功能。
- 演示动画效果 

### 三组基本动画

- 显示(show)与隐藏(hide)是一组动画toggle：
- 滑入(slideUp)与滑出(slideDown)与切换(slideToggle)，效果与卷帘门类似
- 淡入(fadeIn)与淡出(fadeOut)与切换(fadeToggle)

```javascript
$obj.show([speed], [callback]);
// speed(可选)：动画的执行时间
	 // 1.如果不传，就没有动画效果。如果是slide和fade系列，会默认为normal
	 // 2.毫秒值(比如1000),动画在1000毫秒执行完成(推荐)
     // 3.固定字符串，slow(600)、normal(400)、fast(200)，如果传其他字符串，则默认为normal。
// callback(可选):执行完动画后执行的回调函数

slideDown()/slideUp()/slideToggle();同理
fadeIn()/fadeOut()/fadeToggle();同理
```

### 自定义动画

- animate: 自定义动画

```javascript
$(selector).animate({params},[speed],[easing],[callback]);
// {params}：要执行动画的CSS属性，带数字（必选）
// speed：执行动画时长（可选），默认400
// easing:执行效果，默认为swing（缓动）慢快慢  可以是linear（匀速）
// callback：动画执行完后立即执行的回调函数（可选）
```

### 动画队列与停止动画

- 在同一个元素上执行多个动画，那么对于这个动画来说，后面的动画会被放到动画队列中，等前面的动画执行完成了才会执行（联想：火车进站）。

```javascript
// stop方法：停止动画效果
stop(clearQueue, jumpToEnd);
// 第一个参数：是否清除队列
// 第二个参数：是否跳转到最终效果
```

### 案例

- 下拉菜单-动画
- 开关机动画
- 手风琴特效

## jQuery节点操作

### 创建节点

```javascript
// $(htmlStr)
// htmlStr：html格式的字符串 返回jQuery对象
$('<span>这是一个span元素</span>');
```

### 添加节点

```javascript
append  appendTo	在被选元素的结尾插入内容
prepend prependTo	在被选元素的开头插入内容
before				在被选元素之后插入内容
after				在被选元素之前插入内容
```

**案例**：

- 动态生成英雄列表


- 作业：城市选择案例
- 作业：动态创建表格，学生成绩表

### 清空节点与删除节点

- empty：清空指定节点的所有元素，自身保留(清理门户)

```javascript
$('div').empty(); // 清空div的所有内容（推荐使用，会清除子元素上绑定的内容，源码）
$('div').html('');// 使用html方法来清空元素。
```

- remove：相比于empty，自身也删除（自杀）

```javascript
$('div').remove();
```

### 克隆节点

- 作用：复制匹配的元素

```javascript
// 复制$(selector)所匹配到的元素（深度复制）
// cloneNode(true)
// 返回值为复制的新元素，和原来的元素没有任何关系了。即修改新元素，不会影响到原来的元素。
$(selector).clone();
```


## jQuery尺寸和位置操作

### width方法与height方法

- 设置或者获取高度，不包括内边距、边框和外边距

```javascript
// 带参数表示设置高度
$('img').height(200);
// 不带参数获取高度
$('img').height();
```

获取网页的可视区宽高

```javascript
// 窗口大小发生变化的事件
window.onresize = function () {};
// 获取可视区宽度
$(window).width();
// 获取可视区高度
$(window).height();
```

### innerWidth/innerHeight/outerWidth/outerHeight

```javascript
innerWidth()/innerHeight()	方法返回元素的宽度/高度（包括内边距）。
outerWidth()/outerHeight()  方法返回元素的宽度/高度（包括内边距和边框）。
outerWidth(true)/outerHeight(true)  方法返回元素的宽度/高度（包括内边距、边框和外边距）。
```

### scrollTop与scrollLeft

- 设置或者获取垂直滚动条的位置

```javascript
// 当页面滚动的时候 - 事件
// window.onscroll 

// 获取页面被卷曲的高度
$(window).scrollTop();
// 获取页面被卷曲的宽度
$(window).scrollLeft();

// 设置滚动动画
$('body,html').animate({
    scrollTop: 0
}, 100)
```

### offset方法与position方法

- offset方法获取元素距离document的位置，position方法获取的是元素距离有定位的父元素(offsetParent)的位置。

```javascript
// 获取或设置元素距离document的位置,返回值为对象：{left:100, top:100}
$(selector).offset();
// 获取相对于其最近的有定位的父元素的位置。
$(selector).position();
```


## jQuery事件机制

- JavaScript中已经学习过了事件，jQuery对JavaScript事件进行了封装，增加并扩展了事件处理机制。jQuery不仅提供了更加优雅的事件处理语法，而且极大的增强了事件的处理能力。

### jQuery事件发展历程(了解)

简单事件绑定--bind事件绑定--delegate事件绑定--on事件绑定(推荐)

- 简单事件注册

```javascript
click(handler)			单击事件
mouseenter(handler)		鼠标进入事件
mouseleave(handler)		鼠标离开事件
```

缺点：不能同时注册多个事件 bind方式注册事件

```javascript
// 第一个参数：事件类型
// 第二个参数：事件处理程序
$('p').bind('click mouseenter', function(){
    // 事件响应方法
});
```

缺点：不支持动态事件绑定

- delegate注册委托事件

```javascript
// 第一个参数：selector，要绑定事件的元素
// 第二个参数：事件类型
// 第三个参数：事件处理函数
$('.parentBox').delegate('p', 'click', function(){
    // 为 .parentBox下面的所有的p标签绑定事件
});
```

缺点：只能注册委托事件，因此注册时间需要记得方法太多了

- on注册事件

### on注册事件(重点)

- jQuery1.7之后，jQuery用on统一了所有事件的处理方法。
- 最现代的方式，兼容zepto(移动端类似jQuery的一个库)，强烈建议使用。

on注册简单事件

```javascript
// 表示给$(selector)绑定事件，并且由自己触发，不支持动态绑定。
$(selector).on( 'click mouseover', function() {});
```

on注册事件委托

```javascript
// 表示给$(selector)绑定代理事件，当必须是它的内部元素span才能触发这个事件，支持动态绑定
$(selector).on( 'click', 'span', function() {});
```

事件委托原理

```javascript
// 事件委托的原理
var ul = document.querySelector('#ul');
ul.onclick = function (e) {
  // console.log(e.target.tagName);
  if (e.target.tagName.toLowerCase() === 'li') {
    console.log(e.target);
  }
}
```

on注册事件的语法：

```javascript
// 第一个参数：events，绑定事件的名称可以是由空格分隔的多个事件（标准事件或者自定义事件）
// 第二个参数：selector, 执行事件的后代元素（可选），如果没有后代元素，那么事件将有自己执行。
// 第三个参数：data，传递给处理函数的数据，事件触发的时候通过event.data来使用（不常使用）
// 第四个参数：handler，事件处理函数
$(selector).on(events[,selector][,data],handler);
```

- 通过源码查看 bind click delegate on 注册事件的区别

### 事件解绑

- unbind方式（不用）

```javascript
$(selector).unbind(); // 解绑所有的事件
$(selector).unbind('click'); // 解绑指定的事件
```

- undelegate方式（不用）

```javascript
$( selector ).undelegate(); // 解绑所有的delegate事件
$( selector).undelegate( 'click' ); // 解绑所有的click事件
```

- off方式（推荐）

```javascript
// 解绑匹配元素的所有事件
$(selector).off();
// 解绑匹配元素的所有click事件
$(selector).off('click');
```

### 触发事件

```javascript
$(selector).click(); // 触发 click事件
$(selector).trigger('click');
```

### Hover

```js
$(selector).hover(fnEnter, fnLeave);
// 下面的简写形式
$(selector).mouseenter(function () {
}).mouseleave(function () {
})
```

### jQuery事件对象

jQuery事件对象其实就是js事件对象的一个封装，处理了兼容性。

```javascript
// screenX和screenY	对应屏幕最左上角的值
// offsetX和offsetY  获取鼠标在元素中的位置
// clientX和clientY	距离页面左上角的位置（忽视滚动条）
// pageX和pageY	距离页面最顶部的左上角的位置（会计算滚动条的距离）

// event.keyCode	按下的键盘代码
// event.data	存储绑定事件时传递的附加数据

// event.stopPropagation()	阻止事件冒泡行为
// event.preventDefault()	阻止浏览器默认行为
// return false:既能阻止事件冒泡，又能阻止浏览器默认行为。
```

## jQuery补充知识点

### 链式编程

- 通常情况下，只有设置操作才能把链式编程延续下去。因为获取操作的时候，会返回获取到的相应的值，无法返回 jQuery对象。

```javascript
end(); // 筛选选择器会改变jQuery对象的DOM对象，想要回复到上一次的状态，并且返回匹配元素之前的状态。
```

### each方法

- jQuery的隐式迭代会对所有的DOM对象设置相同的值，但是如果我们需要给每一个对象设置不同的值的时候，就需要自己进行迭代了。

作用：遍历jQuery对象集合，为每个匹配的元素执行一个函数

```javascript
// 参数一表示当前元素在所有匹配元素中的索引号
// 参数二表示当前元素（DOM对象）
$(selector).each(function(index,element){});
```

### 多库共存

- jQuery使用$作为标示符，但是如果与其他框架中的$冲突时，jQuery可以释放$符的控制权.

```javascript
var c = $.noConflict();// 释放$的控制权,并且把$的能力给了c
```

### 常用插件

- 弹出层插件 layer
- 放大镜插件
- 轮播图插件
- 图片懒加载插件
- jQueryUI
  - 常用的2-3个功能演示


## jQuery插件开发

- 给jQuery增加方法的两种方式

```javascript
$.method = fn		静态方法
$.fn.method = fn	实例方法
```

- 增加一个静态方法，实现两个数的和，插件

```javascript
(function ($) {
  $.add = function (a, b) {
    return a + b;
  }
}(jQuery))

$.add(5, 6);
```

- tab栏插件

```javascript
(function ($) {
  // {tabMenu: '#aa'}
  $.tab = function (options) {
    // 默认参数
    var defaults = {
      tabMenu: '#tab',
      activeClass: 'active',
      tabMain: '#tab-main',
      tabMainSub: '.main',
      selectedClass: 'selected'
    }
    // 把options中的属性，把对应属性的值赋给defaults对应的属性
    // defaults.tabMenu = options.tabMenu || defaults.tabMenu;
    // for(var key in options) {
    //   defaults[key] = options[key];
    // }
    $.extend(defaults, options);

    $(defaults.tabMenu).on('click', 'li', function () {
      $(this)
        .addClass(defaults.activeClass)
        .siblings()
        .removeClass(defaults.activeClass);

      //
      var index = $(this).index();
      //
      $(defaults.tabMain + ' ' + defaults.tabMainSub)
        .eq(index)
        .addClass(defaults.selectedClass)
        .siblings()
        .removeClass(defaults.selectedClass);
    })
  }
}(window.jQuery))
```

- 表格插件

```javascript
(function($) {
  // 内部的变量，外部无法访问，防止变量名冲突
  var a = 0;
  // 给$增加了一个实例方法
  $.fn.table = function (header, data) {
    var array = [];
    array.push('<table>');
    array.push('<tr>');

    // 生成表头
    $.each(header, function () {
      array.push('<th>' + this + '</th>');
    })
    array.push('</tr>');


    // 生成数据行
    $.each(data, function (index) {
      // this是当前遍历到的数组中的每一个对象
      // 拼数据行
      array.push('<tr>');
      array.push('<td>' + (index + 1) + '</td>');

      // 遍历对象，拼表格
      for (var key in this) {
        array.push('<td>' + this[key] + '</td>');
      }

      array.push('</tr>');
    })
    array.push('</table>');

    this.append(array.join(''));
  }

}(window.jQuery))
```

- 插件开发的原理