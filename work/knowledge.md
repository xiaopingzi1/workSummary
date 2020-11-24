## 1 createElement函数中，模板中属性的写法
```js
  {
  // 与 `v-bind:class` 的 API 相同，
  // 接受一个字符串、对象或字符串和对象组成的数组
  'class': {
    foo: true,
    bar: false
  },
  // 与 `v-bind:style` 的 API 相同，
  // 接受一个字符串、对象，或对象组成的数组
  style: {
    color: 'red',
    fontSize: '14px'
  },
  // 普通的 HTML 特性
  attrs: {
    id: 'foo'
  },
  // 组件 prop，这个属性是当createElement渲染的是一个组件时使用
  props: {
    myProp: 'bar'
  },
  // DOM 属性
  domProps: {
    innerHTML: 'baz'
  },
  // 事件监听器在 `on` 属性内，
  // 但再也不支持如 `v-on:keyup.enter` 这样的修饰器。
  // 须要在处理函数中手动检查 keyCode。
  on: {
    click: this.clickHandler
  },
  // 仅用于组件，用于监听原生事件，而不是组件内部使用
  // 组件内的原生事件触发时，使用`vm.$emit` 触发的事件。
  nativeOn: {
    click: this.nativeClickHandler
  },
  // 自定义指令。注意，你没法对 `binding` 中的 `oldValue`
  // 赋值，由于 Vue 已经自动为你进行了同步。
  directives: [
    {
      name: 'my-custom-directive',
      value: '2',
      expression: '1 + 1',
      arg: 'foo',
      modifiers: {
        bar: true
      }
    }
  ],
  // 做用域插槽的格式为
  // { name: props => VNode | Array<VNode> }
  scopedSlots: {
    default: props => createElement('span', props.text)
  },
  // 若是组件是其它组件的子组件，需为插槽指定名称
  slot: 'name-of-slot',
  // 其它特殊顶层属性
  key: 'myKey',
  ref: 'myRef',
  // 若是你在渲染函数中给多个元素都应用了相同的 ref 名，
  // 那么 `$refs.myRef` 会变成一个数组。
  refInFor: true
}

```
## 2 scoped实现私有化样式

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