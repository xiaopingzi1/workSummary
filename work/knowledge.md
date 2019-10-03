## 1 Vue.nextTick
```js
new Vue({
  el: '#app',
  data: {
    count: 0,
    list: []
  },
  methods:{
    add() {
      this.count += 1
      this.list.push(1)
      this.$nextTick(()=&gt;{
          let li = this.$refs.ul.querySelectorAll('li')
          li.forEach(item=&gt;{
          item.style.color = 'red';
        })
      })
    }
  }
})
```
如果希望在DOM更新后再更新样式，可以在nextTick的回调中执行更新样式的操作。
* 数据更新时，并不会立即更新DOM。如果在更新数据之后的代码执行另一段代码，有可能达不到预想效果。将视图更新后的操作放在nextTick的回调中执行，其底层通过微任务的方式执行回调，可以保证DOM更新后才执行代码。

## 2 scoped实现私有化样式
总结一下scoped三条渲染规则

    给HTML的DOM节点加一个不重复data属性(形如：data-v-2311c06a)来表示他的唯一性
    在每句css选择器的末尾（编译后的生成的css语句）加一个当前组件的data属性选择器（如[data-v-2311c06a]）来私有化样式
    如果组件内部包含有其他组件，只会给其他组件的最外层标签加上当前组件的data属性

## 3 路由懒加载
```js
{
    name: 'signInStu',
    path: '/signInStu',
    meta: {
      // title: '签到加分'
    },
    component: function (resolve) {
      require(['./page/stu/signInStu.vue'], resolve)
    }
  },
  ```

  如果用import引入的话，当项目打包时路由里的所有component都会打包在一个js中，造成进入首页时，需要加载的内容过多，时间相对比较长。
当你用require这种方式引入的时候，会将你的component分别打包成不同的js，加载的时候也是按需加载，只用访问这个路由网址时才会加载这个js。

## 4 qs
1. qs.parse()将URL解析成对象的形式
```js
const Qs = require('qs'); 
let url = 'method=query_sql_dataset_data&projectId=85&appToken=7d22e38e-5717-11e7-907b-a6006ad3dba0'; 
Qs.parse(url); 
console.log(Qs.parse(url));
```

2. qs.stringify()将对象 序列化成URL的形式，以&进行拼接

```js
const Qs = require('qs'); 
let obj= 
{ method: "query_sql_dataset_data", 
projectId: "85", 
appToken: "7d22e38e-5717-11e7-907b-a6006ad3dba0", 
datasetId: " 12564701" 
};
 Qs.stringify(obj); 
 console.log(Qs.stringify(obj));

```
那么当我们需要传递数组的时候，我们就可以通过下面方式进行处理：
默认情况下，它们给出明确的索引，如下代码：
```js
qs.stringify({ a: ['b', 'c', 'd'] });
// 'a[0]=b&a[1]=c&a[2]=d'

```
## 5 vue项目移动端的适配问题
px2rem-loader
```js
在bulid文件中的utils.js
const px2remLoader = {
    loader: 'px2rem-loader',
    options: {
      remUnit: 75
    }
  }
在generateLoaders方法中添加px2remLoader

```

## 6 HTML xmlns 属性
xmlns 属性

xmlns 属性可以在文档中定义一个或多个可供选择的命名空间。该属性可以放置在文档内任何元素的开始标签中。
该属性的值类似于 URL，它定义了一个命名空间，浏览器会将此命名空间用于该属性所在元素内的所有内容。