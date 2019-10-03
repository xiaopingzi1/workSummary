### 1 vuex是什么，如何使用，那种功能场景使用
 * 专为 Vue.js 应用程序开发的状态管理模式，它采用集中式存储管理应用的所有组件的状态，并以相应的    规则保证状态以一种可预测的方式发生变化。
  
### 2 vue解决跨域的方法？详细说明
  * 1 后台更改header  
    header('Access-Control-Allow-Origin:*');  允许所有来源访问   
    header('Access-Control-Allow-Method:POST,GET');  允许访问的方式 　 　

  * 2 使用JQuery提供的jsonp 
    
    ```js
    methods: { 
      getData () { 
        var self = this 
        $.ajax({ 
          url: 'http://f.apiplus.cn/bj11x5.json', 
          type: 'GET', 
          dataType: 'JSONP', 
          success: function (res) { 
            self.data = res.data.slice(0, 3) 
            self.opencode = res.data[0].opencode.split(',') 
          } 
        }) 
      } 
    }  

    ```

  * 3 使用http-proxy-middleware 代理解决（项目使用vue-cli脚手架搭建）  
    例如请求的url: “http://f.apiplus.cn/bj11x5.json”

    ```js
    //打开config/index.js,在proxyTable中添写如下代码
    proxyTable: { 
     '/api': {  //使用"/api"来代替"http://f.apiplus.c" 
    target: 'http://f.apiplus.cn', //源地址 
    changeOrigin: true, //改变源 
    pathRewrite: { 
      '^/api': 'http://f.apiplus.cn' //路径重写 
      } 
    } 
  }
    //使用axios请求数据时直接使用“/api”
    getData () { 
     axios.get('/api/bj11x5.json', function (res) { 
       console.log(res) 
     })

    //通过这中方法去解决跨域，打包部署时还按这种方法会出问题。解决方法如下：
    let serverUrl = '/api/'  //本地调试时 
    // let serverUrl = 'http://f.apiplus.cn/'  //打包部署上线时 
    export default { 
       dataUrl: serverUrl + 'bj11x5.json' 
    }
    ```

### 3 vue常用的指令和用法

### 4 对于MVVM的理解

   * MVVM 是 Model-View-ViewModel 的缩写。

     Model 代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑。   
     View 代表UI 组件，它负责将数据模型转化成UI 展现出来。  
     ViewModel 监听模型数据的改变和控制视图行为、处理用户交互，简单理解就是一个同步View 和 Model的对象，连接Model和View。  

     在MVVM架构下，View 和 Model 之间并没有直接的联系，而是通过ViewModel进行交互，Model 和 ViewModel 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到View 上。

     ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM，不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

### 4.1 对于MVC的理解
  * MVC的全名是Model View Controller，是模型(model)－视图(view)－控制器(controller)的缩写，是一种软件设计典范。它是用一种业务逻辑、数据与界面显示分离的方法来组织代码，将众多的业务逻辑聚集到一个部件里面，在需要改进和个性化定制界面及用户交互的同时，不需要重新编写业务逻辑，达到减少编码的时间。

    MVC开始是存在于桌面程序中的，M是指业务模型，V是指用户界面，C则是控制器。

    在网页当中，

    V即View视图是指用户看到并与之交互的界面。比如由html元素组成的网页界面，或者软件的客户端界面。MVC的好处之一在于它能为应用程序处理很多不同的视图。在视图中其实没有真正的处理发生，它只是作为一种输出数据并允许用户操纵的方式。

    M即model模型是指模型表示业务规则。在MVC的三个部件中，模型拥有最多的处理任务。被模型返回的数据是中立的，模型与数据格式无关，这样一个模型能为多个视图提供数据，由于应用于模型的代码只需写一次就可以被多个视图重用，所以减少了代码的重复性。

    C即controller控制器是指控制器接受用户的输入并调用模型和视图去完成用户的需求，控制器本身不输出任何东西和做任何处理。它只是接收请求并决定调用哪个模型构件去处理请求，然后再确定用哪个视图来显示返回的数据。  

### 5 Vue的生命周期
  * beforeCreate（创建前），在数据观测和初始化事件还未开始

    created（创建后），完成数据观测，属性和方法的运算，初始化事件， $el 属性还没有显示出来

    beforeMount（载入前），在挂载开始之前被调用，相关的render函数首次被调用。实例已完成以下的配置：编译模板，把data里面的数据和模板生成html。注意此时还没有挂载html到页面上。

    mounted（载入后），在el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用。实例已完成以下的配置：用上面编译好的html内容替换el属性指向的DOM对象。完成模板中的html渲染到html页面中。此过程中进行ajax交互。

    beforeUpdate（更新前），在数据更新之前调用，发生在虚拟DOM重新渲染和打补丁之前。可以在该钩子中进一步地更改状态，不会触发附加的重渲染过程。

    updated（更新后），在由于数据更改导致的虚拟DOM重新渲染和打补丁之后调用。调用时，组件DOM已经更新，所以可以执行依赖于DOM的操作。然而在大多数情况下，应该避免在此期间更改状态，因为这可能会导致更新无限循环。该钩子在服务器端渲染期间不被调用。

    beforeDestroy（销毁前），在实例销毁之前调用。实例仍然完全可用。

    destroyed（销毁后），在实例销毁之后调用。调用后，所有的事件监听器会被移除，所有的子实例也会被销毁。该钩子在服务器端渲染期间不被调用。

  * 1、什么是vue生命周期？  
    Vue 实例从创建到销毁的过程，就是生命周期。从开始创建、初始化数据、编译模板、挂载Dom→渲染、更新→渲染、销毁等一系列过程，称之为 Vue 的生命周期。

  * 2、vue生命周期的作用是什么？  
    它的生命周期中有多个事件钩子，让我们在控制整个Vue实例的过程时更容易形成好的逻辑。

  * 3、vue生命周期总共有几个阶段？  
    它可以总共分为8个阶段：创建前/后、载入前/后、更新前/后、销毁前/销毁后。

  * 4、第一次页面加载会触发哪几个钩子？  
   会触发下面这几个beforeCreate、created、beforeMount、mounted 。

  * 5、DOM 渲染在哪个周期中就已经完成？  
    DOM 渲染在 mounted 中就已经完成了。

### 6 Vue实现数据双向绑定的原理：Object.defineProperty()
vue.js 则是采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty()来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调。
```js
var obj  = {};
Object.defineProperty(obj, 'name', {
        get: function() {
            console.log('我被获取了')
            return val;
        },
        set: function (newVal) {
            console.log('我被设置了')
        }
})
obj.name = 'fei';//在给obj设置name属性的时候，触发了set这个方法
var val = obj.name;//在得到obj的name属性，会触发get方法
```
示意图

![](../assets/img/双向绑定.png)

a、Observer实现对MVVM自身model数据劫持，监听数据的属性变更，并在变动时进行notify  
b、Compile实现指令解析，初始化视图，并订阅数据变化，绑定好更新函数  
c、Watcher一方面接收Observer通过dep传递过来的数据变化，一方面通知Compile进行view update。

observer用来实现对每个vue中的data中定义的属性循环用Object.defineProperty()实现数据劫持，以便利用其中的setter和getter，然后通知订阅者，订阅者会触发它的update方法，对视图进行更新。

在vue中v-model，v-name，{{}}等都可以对数据进行显示，也就是说假如一个属性都通过这三个指令了，那么每当这个属性改变的时候，相应的这个三个指令的html视图也必须改变，于是vue中就是每当有这样的可能用到双向绑定的指令，就在一个Dep中增加一个订阅者，其订阅者只是更新自己的指令对应的数据，也就是v-model='name'和{{name}}有两个对应的订阅者，各自管理自己的地方。每当属性的set方法触发，就循环更新Dep中的订阅者。

### 7 Vue组件间的参数传递
1、父组件与子组件传值

父组件传给子组件：父传子的实现方式就是通过props属性，子组件通过props属性接收从父组件传过来的值，而父组件传值的时候使用 v-bind 将子组件中预留的变量名绑定为data里面的数据即可

* 1 子组件在props中创建一个属性，用来接收父组件传过来的值
* 2 在父组件中注册子组件
* 3 在子组件标签中添加子组件props中创建的属性
* 4 把需要传给子组件的值赋值给该属性

子组件的代码

```js
<template>
    <div id="container">
        {{msg}}
    </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props:{
    msg: String
  }
};
</script>
<style scoped>
#container{
    color: red;
    margin-top: 50px;
}
</style>
```

父组件的代码

```js
<template>
    <div id="container">
        <input type="text" v-model="text" @change="dataChange">
        <Child :msg="text"></Child>
    </div>
</template>
<script>
import Child from "@/components/Child";
export default {
  data() {
    return {
      text: "父组件的值"
    };
  },
  methods: {
    dataChange(data){
        this.msg = data
    }
  },
  components: {
    Child
  }
};
</script>
<style scoped>
</style>
```

2 子组件传给父组件： 子传父的实现方式就是用了 this.$emit 来遍历 getData 事件，首先用按钮来触发 setData 事件，在 setData 中 用 this.$emit 来遍历 getData 事件，最后返回 this.msg

总结：

    子组件中需要以某种方式例如点击事件的方法来触发一个自定义事件
    将需要传的值作为$emit的第二个参数，该值将作为实参传给响应自定义事件的方法
    在父组件中注册子组件并在子组件标签上绑定对自定义事件的监听

    this.$on('abc',()=>{}) 绑定事件  
    this.$emit('abc') 触法事件

子组件代码

```js
<template>
    <div id="container">
        <input type="text" v-model="msg">
        <button @click="setData">传递到父组件</button>
    </div>
</template>
<script>
export default {
  data() {
    return {
      msg: "传递给父组件的值"
    };
  },
  methods: {
    setData() {
      this.$emit("getData", this.msg);
    }
  }
};
</script>
<style scoped>
#container {
  color: red;
  margin-top: 50px;
}
</style>

```
父组件代码

```js
<template>
    <div id="container">
        <Child @getData="getData"></Child>
        <p>{{msg}}</p>
    </div>
</template>
<script>
import Child from "@/components/Child";
export default {
  data() {
    return {
      msg: "父组件默认值"
    };
  },
  methods: {
    getData(data) {
      this.msg = data;
    }
  },
  components: {
    Child
  }
};
</script>
<style scoped>
</style>

```


2、非父子组件间的数据传递，兄弟组件传值

eventBus，就是创建一个事件中心，相当于中转站，可以用它来传递事件和接收事件。项目比较小时，用这个比较合适（虽然也有不少人推荐直接用VUEX，具体来说看需求咯。技术只是手段，目的达到才是王道）。

> child-a>child-b
> 前置条件->js绑定+触发事件
1. 绑定事件 this.$on(事件名,函数(接收的形参){})
2. 触发事件 this.$emit(事件名,数据)

>A
1. 点击按钮触发方法->触发事件vm.$emit(事件名,数据)
  
>B
1. 绑定事件vm.$on(事件名,接收的参数)

> A和B中导入共同的vm实例
> 注意:提供共有的vm实例->利用模块->导出一个vm实例


### 8 Vue的路由实现：hash模式 和 history模式
 hash模式：在浏览器中符号“#”，#以及#后面的字符称之为hash，用 window.location.hash 读取。特点：hash虽然在URL中，但不被包括在HTTP请求中；用来指导浏览器动作，对服务端安全无用，hash不会重加载页面。vue-router默认是hash模式

 history模式：history采用HTML5的新特性；且提供了两个新方法： pushState()， replaceState()可以对浏览器历史记录栈进行修改，以及popState事件的监听到状态变更。

### 9 vue路由的钩子函数
首页可以控制导航跳转，beforeEach，afterEach等，一般用于页面title的修改。一些需要登录才能调整页面的重定向功能。

beforeEach主要有3个参数to，from，next。  

to：route即将进入的目标路由对象。

from：route当前导航正要离开的路由。

next：function一定要调用该方法resolve这个钩子。执行效果依赖next方法的调用参数。可以控制网页的跳转。

### 10 vuex是什么？怎么使用？哪种功能场景使用它？
  * 只用来读取的状态集中放在store中； 改变状态的方式是提交mutations，这是个同步的事物； 异步逻辑应该封装在action中。

    在main.js引入store，注入。新建了一个目录store，… export 。

    场景有：单页应用中，组件之间的状态、音乐播放、登录状态、加入购物车
  
  ![](../assets/img/vuex1.png)

  * state：Vuex 使用单一状态树,即每个应用将仅仅包含一个store 实例，但单一状态树和模块化并不冲突。存放的数据状态，不可以直接修改里面的数据。

  * mutations：mutations定义的方法动态修改Vuex 的 store 中的状态或数据。

  * getters：类似vue的计算属性，主要用来过滤一些数据。

  * action：actions可以理解为通过将mutations里面处里数据的方法变成可异步的处理数据的方法，简单的说就是异步操作数据。view 层通过 store.dispath 来分发 action。

```js
  const store = new Vuex.Store({
    state:{
      count:0
    },
    mutations:{
      increment (state) {
        state.count++
      }
    },
    actions:{
      increment (context) {
        context.commit('incremnet')
      }
    }
  })
```

  * modules：项目特别复杂的时候，可以让每一个模块拥有自己的state、mutation、action、getters，使得结构非常清晰，方便管理。

```js
  const moduleA = {
    state:{},
    actions:{},
    getters:{},
  }
  const moduleB = {
  state:{},
  actions:{},
  getters:{},
  }
  const store = new Vuex.store({
    modules：{
      a:moduleA,
      b:moduleB
    }
  })
```

### 11 CSS只在当前的组件起作用
  在style标签中写入scoped即可

### 12 $route和$router的区别
 $route是“路由信息对象”，包括path，params，hash，query，fullPath，matched，name等路由信息参数。

 $router为VueRouter的实例，相当于一个全局的路由器对象，里面含有很多属性和子对象，例如history对象。。。经常用的跳转链接就可以用this.$router.push，和router-link跳转一样
 编程式导航

 ### 13vue中缓冲
 * keep-alive是Vue的内置组件，能在组件切换过程中将状态保留在内存中，防止重复渲染DOM。
   keep-alive 包裹动态组件时，会缓存不活动的组件实例，而不是销毁它们。和 <transition> 相似，keep-alive 是一个抽象组件：它自身不会渲染一个 DOM 元素，也不会出现在父组件链中。

  Props：  
      include - 字符串或正则表达式。只有名称匹配的组件会被缓存。  
      exclude - 字符串或正则表达式。任何名称匹配的组件都不会被缓存。  
      max - 数字。最多可以缓存多少组件实例。  

在app.vue组件里面
```js
<keep-alive exclude="moviesDetail">
   <router-view></router-view>
</keep-alive>

```
keep-alive生命周期钩子函数：activated、deactivated

使用keep-alive会将数据保留在内存中，如果要在每次进入页面的时候获取最新的数据，需要在activated阶段获取数据，承担原来created钩子中获取数据的任务。

### 14 如何让选择vue和react
1 数据方面

* react整体是函数式的思想，把组件设计成纯组件，状态和逻辑通过参数传入，所以在react中，是单向数据流，推崇结合immutable来实现数据不可变。
* vue的思想是响应式的，也就是基于是数据可变的，通过对每一个属性建立Watcher来监听，当属性变化的时候，响应式的更新对应的虚拟dom。

2 通过js来操作一切，还是用各自的处理方式
* react的思路是all in js，通过js来生成html，所以设计了jsx，还有通过js来操作css，社区的styled-component、jss等，
* vue是把html，css，js组合到一起，用各自的处理方式，vue有单文件组件，可以把html、css、js写到一个文件中，html提供了模板引擎来处理。

### 15 vue-router的钩子函数
vue路由钩子大致可以分为三类:

1.全局钩子

主要包括beforeEach和aftrEach,
    beforeEach函数有三个参数：

    to:router即将进入的路由对象
    from:当前导航即将离开的路由
    next:Function,进行管道中的一个钩子，如果执行完了，则导航的状态就是 confirmed （确认的）
    否则为false，终止导航。

    afterEach函数不用传next()函数

这类钩子主要作用于全局,一般用来判断权限,以及以及页面丢失时候需要执行的操作,例如:
```js
//使用钩子函数对路由进行权限跳转
router.beforeEach((to, from, next) => {
    const role = localStorage.getItem('ms_username');
    if(!role && to.path !== '/login'){
        next('/login');
    }else if(to.meta.permission){
        // 如果是管理员权限则可进入，这里只是简单的模拟管理员权限而已
        role === 'admin' ? next() : next('/403');
    }else{
        // 简单的判断IE10及以下不进入富文本编辑器，该组件不兼容
        if(navigator.userAgent.indexOf('MSIE') > -1 && to.path === '/editor'){
            Vue.prototype.$alert('vue-quill-editor组件不兼容IE10及以下浏览器，请使用更高版本的浏
            览器查看', '浏览器不兼容通知', {
                confirmButtonText: '确定'
            });
        }else{
            next();
        }
    }
})

```
2.单个路由里面的钩子beforeEnter,beforeLeave

主要用于写某个指定路由跳转时需要执行的逻辑
```js
   {
    path: '/dashboard',
    component: resolve => require(['../components/page/Dashboard.vue'], resolve),
    meta: { title: '系统首页' },
    beforeEnter: (to, from, next) => {
        
      },
    beforeLeave: (to, from, next) => {
        
    }
 },
```
3.组件路由

    主要包括 beforeRouteEnter和beforeRouteUpdate ,beforeRouteLeave
    这几个钩子都是写在组件里面也可以传三个参数(to,from,next),作用与前面类似.
```js
beforeRouteEnter(to, from, next) {
    next(vm => {
      if (
        vm.$route.meta.hasOwnProperty('auth_key') &&
        vm.$route.meta.auth_key != ''
      ) {
        if (!vm.hasPermission(vm.$route.meta.auth_key)) {
          vm.$router.replace('/admin/noPermission')
        }
      }
    })
  },
```
### 16 插槽
插槽，也就是slot，是组件的一块HTML模板，这块模板显示不现实、以及怎样显示由父组件来决定。

插槽模板是slot，它是一个空壳子，因为它显示与隐藏以及最后用什么样的html模板显示由父组件控制。但是插槽显示的位置由子组件自身决定，slot写在组件template的哪块，父组件传过来的模板将来就显示在哪块。这样就使组件可复用性更高，更加灵活。我们可以随时通过父组件给子组件加一些需要的东西。

### 17 如何用vuex使axios获取到的数据替换store中的数据
### 18 vue计算属性和watch在什么情况下使用
共同点是：都是希望在依赖数据发生改变的时候，被依赖的数据根据预先定义好的函数，发生“自动”的变化。  
但watch和computed也有明显不同的地方：  
watch和computed各自处理的数据关系场景不同  
(1).watch擅长处理的场景：一个数据影响多个数据  
(2).computed擅长处理的场景：一个数据受多个数据影响。总价受到单价和数量的影响

### 19 spa页面
SPA的优点

页面之间的切换非常快  
一定程度上减少了后端服务器的压力（不用管页面逻辑和渲染）  
后端程序只需要提供API，完全不用管客户端到底是Web界面还是手机等  

SPA的缺点

首屏打开速度很慢，因为用户首次加载需要先下载SPA框架及应用程序的代码，然后再渲染页面。  
不利于SEO

SEO：搜索引擎优化。SEO是一种通过了解搜索引擎的运作规则（如何抓取网站页面，如何索引以及如何根据特定的关键字展现搜索结果排序等）来调整网站，以提高该网站在搜索引擎中某些关键词的搜索结果排名。

标题： 即HTML的 < title >标签，例如： < title>浅谈SPA、SEO、SSR | XXX 的博客< /title> 

描述： 即HTML<meta>标签的description，例如百度百科的一个词条的 description

关键字： 即HTML<meta>标签的keywords

SSR  
概述：SSR是 Server-Side Rendering(服务器端渲染)的缩写，在普通的SPA中，一般是将框架及网站页面代码发送到浏览器，然后在浏览器中生成和操作DOM（这里也是第一次访问SPA网站在同等带宽及网络延迟下比传统的在后端生成HTML发送到浏览器要更慢的主要原因），但其实也可以将SPA应用打包到服务器上，在服务器上渲染出HTML，发送到浏览器，这样的HTML页面还不具备交互能力，所以还需要与SPA框架配合，在浏览器上“混合”成可交互的应用程序。所以，只要能合理地运用SSR技术，不仅能一定程度上解决首屏慢的问题，还能获得更好的SEO。

SSR的优点

更快的响应时间，不用等待所有的JS都下载完成，浏览器便能显示比较完整的页面了。

更好的SSR，我们可以将SEO的关键信息直接在后台就渲染成HTML，而保证搜索引擎的爬虫都能爬取到关键数据。

SSR的缺点

相对于仅仅需要提供静态文件的服务器，SSR中使用的渲染程序自然会占用更多的CPU和内存资源

一些常用的浏览器API可能无法正常使用，比如window、docment和alert等，如果使用的话需要对运行的环境加以判断

开发调试会有一些麻烦，因为涉及了浏览器及服务器，对于SPA的一些组件的生命周期的管理会变得复杂
可能会由于某些因素导致服务器端渲染的结果与浏览器端的结果不一致。

![](../assets/img/服务端渲染.png)

ssr 有两个入口文件，client.js 和 server.js， 都包含了应用代码，webpack 通过两个入口文件分别打包成给服务端用的 server bundle 和给客户端用的 client bundle. 当服务器接收到了来自客户端的请求之后，会创建一个渲染器 bundleRenderer，这个 bundleRenderer 会读取上面生成的 server bundle 文件，并且执行它的代码， 然后发送一个生成好的 html 到浏览器，等到客户端加载了 client bundle 之后，会和服务端生成的DOM 进行 Hydration(判断这个DOM 和自己即将生成的DOM 是否相同，如果相同就将客户端的vue实例挂载到这个DOM上， 否则会提示警告)。

## 20 vue 预渲染  prerender-spa-plugin
这个配置只需要在 build 的时候可以生成预渲染好的html，所以应该配置在 build/webpack.prod.conf.js 这个文件里。
```js
// 在vue-cli生成的文件的基础上，只有下面这个才是我们要配置的
new PrerenderSPAPlugin({
    // 生成文件的路径，也可以与webpakc打包的一致。
    // 下面这句话非常重要！！！
    // 这个目录只能有一级，如果目录层次大于一级，在生成的时候不会有任何错误提示，在预渲染的时候只会卡着不动。
    staticDir: path.join(__dirname, '../dist'),
    
    // 对应自己的路由文件，比如index有参数，就需要写成 /index/param1。
    routes: ['/', '/index', '/skin', '/slimming', '/exercise', '/alPay', '/wxPay'],
    
    // 这个很重要，如果没有配置这段，也不会进行预编译
    renderer: new Renderer({
        inject: {
          foo: 'bar'
        },
        headless: false,
        // 在 main.js 中 document.dispatchEvent(new Event('render-event'))，两者的事件名称要对应上。
        renderAfterDocumentEvent: 'render-event'
    })
```
在 webpack.prod.conf.js 配置完成之后，然后再 main.js 里改成如下所示：
```js
new Vue({
    el: '#app',
    router,
    store,
    render: h => h(App),
    
    /* 这句非常重要，否则预渲染将不会启动 */
    mounted () {
        document.dispatchEvent(new Event('render-event'))
    }
})
```