### 1 ES6
ES6 既是一个历史名词，也是一个泛指，含义是 5.1 版以后的 JavaScript 的下一代标准，涵盖了 ES2015、ES2016、ES2017 等等，而 ES2015 则是正式名称，特指该年发布的正式版本的语言标准。一般是指 ES2015 标准，但有时也是泛指“下一代 JavaScript 语言”。 

### 2 变量声明 const、let

`var` 

- 作用:声明变量
- 变量提升
- 全局作用域和函数级作用域
- 可以重复命名
- 无块级作用域

`let` 

- 作用:声明变量
- **块级作用域**{}
- 必须先声明后使用
- 在同一个块内不允许重复命名
- 没有变量提升

`const`

- 作用:声明**常量**
- **块级作用域**
- **声明的同时必须赋值** !!!!
- 声明的常量不能被重新赋值
- 必须先声明后使用
- 在同一个块内不允许重复命名



### 3 解构赋值

> 解构: 从数组和对象中提取值，把值赋值给变量

1. 数组解构赋值

   1. 有顺序问题
   2. 可以指定默认值
   3. 被赋值的变量和数组中的元素个数可以不相等

2. 对象解构赋值

   1. 无顺序问题
   2. 可以指定默认值
   3. 被赋值的变量和对象中的key-value个数可以不相等
   4. **有两种写法**

   - 被赋值的变量名和对象中的key名一致
   - 可以给被赋值的变量**起别名**, {key名:别名}={key:value}

```js
// 练习
const node = {
  loc: {
    start: {
      line: 1,
      column: 5
    }
  }
};

let { loc, loc: { start }, loc: { start: { line }} } = node;
// 输出 
line // 
loc  // 
start //
```



### 4 模板字符串 

``` js
// 采用模板字符串的做法
// `${变量}`

var str2 = `
你好,我叫${person.name},
我今年${person.age}岁了,
我是${person.gender}生
`;
console.log(str2);
// 使用场景:如果需要拼接字符串或者换行了,那就用模板字符串
// 'abc';
// `abc`;
```

### 5 函数扩展!!(重要)

1. 函数参数的默认值

   - 函数参数不能同名
   - 参数默认值不是传值,而是惰性求值
   - 函数参数默认是声明的,不能在函数体中再次声明

2. 函数参数默认值与解构赋值结合

3. rest参数

   ``` js
   // 写法:在函数参数位置 写: ...参数名
   
   // 注意: 与rest参数搭配使用的形参abc是一个数组
   
   // 作用: 将多余的参数放在数组中
   
   // 好处:如果使用了rest参数,那么就不需要使用arguments对象
   
   // 场景:利用rest参数就可以向函数传任意数量的参数啦!
   
   // 小细节: ...values后面不能再写其他参数!->rest参数要写在参数列表的末尾!
   ```

4. 箭头函数

   - ES6允许使用箭头 => 去定义函数

   - 基本用法

     ```js
     // 箭头函数基本用法
     // 之前的写法
     var f = function(a) {
         return a;
     };
     // 现在的写法
     // fNew是函数名
     // =>前面的a是形参名
     // => 后面的a是函数体
     var fNew = a => a;
     // console.log((fNew(10)));
     
     // 考虑函数参数和函数体的不同写法,箭头函数的写法就有了不同的组合
     // 1. 函数只有一个参数时,函数体只有一代码并且没有返回值时
     var fn1 = x => console.log(x);
     // fn1(20);
     // 2. 函数没有参数时,函数体只有一句代码并且有返回值
     var fn2 = () => { return 10; };
     // console.log(fn2());
     // 3. 函数有多个参数时,函数体只有一句代码并且有返回值
     var fn3 = (x, y) => { return x + y; };
     // console.log(fn3(10, 20));
     // 4. 函数体有多行代码时,函数只有一个参数时
     var fn4 = x => {
         var y = 10;
         return y + x;
     };
     console.log(fn4(20));
     
     // 注意:
     // 1. 参数只有一个时 ()省略不写
     // 2. 没有参数时 ()不能省略
     // 3. 多个参数时, ()不能省略
     // 4. 函数体只有一句代码时并且有返回时 {}不能省略
     // 5. 函数体有多行代码时,{}不能省略, 多行代码写在{}里面啊
     // 6. 函数体只有一句代码时,并且没返回值,{}可以省略
     // 建议: 所有的匿名函数 改成箭头函数的写法
     ```

### 6 箭头函数使用注意及this问题  

```js
var per = {
    name: "TOM",
    sayHi: function() {
        console.log(this.name);
        // 1. 
        // setTimeout(function() {
        //     console.log(this.name);
        // }, 1000);
        // 2.
        // var _this = this;
        // setTimeout(function() {
        //     console.log(_this.name);
        // }, 1000);
        // 3.
        // setTimeout(function() {
        //     console.log(this.name);
        // }.bind(this), 1000);
        // 4.
        // setTimeout(() => {
        //     console.log(this.name);
        // }, 1000);
    }
}

per.sayHi();
```

> 注意事项:

1. 箭头函数中的this自动绑定外部环境的this
2. 箭头函数中没有自己的this
3. 箭头函数不能用于构造函数
4. 箭头函数中的没有arguments对象,可以用剩余参数...rest代替
5. 箭头函数通常用于匿名函数



###  7 导出模块成员

#### 1> 导出多个成员：写法一

```
// 导出多个成员：写法一
module.exports.a = 123;
module.exports.b = 456;
module.exports.c = 789;
```

#### 2> 导出多个成员：写法二

为了降低开发人员的痛苦，所以为 `module.exports` 提供了一个别名 `exports` （下面写法等价于上面的写法）。

```
console.log(exports === module.exports) // => true
exports.a = 123;
exports.b = 456;
exports.c = 789;
console.log(exports);
// 但是最终导出的依然是module.exports!
```

#### 3> 导出多个成员：写法三

```
// module.exports = {
//   d: 'hello',
//   e: 'world',
//   fn: function () {
//     // fs.readFile(function () {

//     // });
//   }
// }
```

#### 4> 导出单个成员

```
// 导出单个成员：错误的写法
// 因为每个模块最终导出是 module.exports 而不是 exports 这个别名
// exports = function (x, y) {
//   return x + y;
// };


// 导出单个成员：必须这么写
module.exports = function (x, y) {
  return x + y;
};
```

> 注意：导出单个只能导出一次，下面的情况后者会覆盖前者：

```
module.exports = 'hello';

// 以这个为准，后者会覆盖前者
module.exports = function (x, y) {
  return x + y;
};
```

> 最终导出的依然是module.exports!!!!
>
> exports是对module.exports的引用
>
> require导入的是模块的module.exports

## 8 filter,map,方法
filter

filter也是一个常用的操作，它用于把Array的某些元素过滤掉，然后返回剩下的元素。

和map()类似，Array的filter()也接收一个函数。和map()不同的是，filter()把传入的函数依次作用于每个元素，然后根据返回值是true还是false决定保留还是丢弃该元素。
```js
var arr = [1, 2, 4, 5, 6, 9, 10, 15];
var r = arr.filter(function (x) {
    return x % 2 !== 0;
});
 r; // [1, 5, 9, 15]

```
回调函数

filter()接收的回调函数，其实可以有多个参数。通常我们仅使用第一个参数，表示Array的某个元素。回调函数还可以接收另外两个参数，表示元素的位置和数组本身：
```js
var arr = ['A', 'B', 'C'];
var r = arr.filter(function (element, index, self) {
    console.log(element); // 依次打印'A', 'B', 'C'
    console.log(index); // 依次打印0, 1, 2
    console.log(self); // self就是变量arr
    return true;
});
数组去重
arr.filter(function (element, index, self) {
    return self.indexOf(element) === index;
 });
console.log(r.toString());

去除重复元素依靠的是indexOf总是返回第一个元素的位置，后续的重复元素位置与indexOf返回的位置不相等，因此被filter滤掉了。
```
