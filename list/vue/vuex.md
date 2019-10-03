### 01-基础-vuex-状态管理流程

> 复杂vue项目中传值

1. 父->子 props
2. 子->父 $emit
3. 兄弟->$on和$emit

> 状态管理->数据管理->组件传值

> vuex把数据相关的代码交给不同的对象

1. state : 数据的声明 相当于data (响应式)
2. actions: 异步操作 比如ajax
3. mutations: 方法 相当于之前methods

> 注意: actions中的ajax结果不是直接给组件

> vuex是vue插件

> 扩展
>
> vue 状态管理 vuex
>
> react 状态管理 redux
>
> vuex和redux->flux(底层框架)

### 2-基础-vuex-state 和 mapState

1. npm i vuex
2. 导入
3. Vue.use(Vuex)
4. 实例化仓库store
5. newVue选项挂载store

> state:数据声明->响应式+所有组件直接可以使用,具体怎么用?

> 导入辅助函数

1. template {{$store.state.count}}
2. 计算属性 

```js
computed:mapState({
    count(state){return state.count}
    
    count:"count"
    
    count(state){
    return state.count+this.num
	}
})

computed:mapState(["count"])

```



### 3 基础-vuex-getters 和 mapGetters

> 场景:如果state中的数据a很复杂 ,此时需要把a的声明写在getters

`store`

```js
getters: {
        a(state) {
            return state.msg + 'xyz'
        }
    }
```

`组件中使用`

```js
computed: {
    // a() {
    //   return this.$store.getters.a;
    // },

    ...mapGetters({
      a: "a"
    })
  }
```

> 注意: getters不是vuex核心组成部分(state状态/actions行为/mutations方法)

### 4-基础-vuex-mutations 和 mapMutations

> mutations:修改state的数据

1. 写方法 mutations:{fn(state){修改state}} -> 声明了方法fn
2. 在组件methods中提交mutations中的方法fn this.$store.commit("fn",实参)

> 在组件methods中 :{...mapMutations({fn5:"fn5"})}



### 5-基础-vuex-actions 和 mapActions

> mutations 同步的修改state的方法
>
> actions:写方法->异步的获取数据的方法,比如ajax

```js
 //定时器/ajax/jsonp请求
    actions: {
        setTitle(context) {
            // context指仓库对象
            // ajax
            setTimeout(() => {
                // 异步结果
                // 比如 结果 2
                const temp = 2;
                context.commit("setTitle", temp);
            }, 1000);
        }

    }
```

`组件/methods`

```js
methods: {
    // ...mapMutations(["setTitle"]),
    ...mapActions(["setTitle"])
  }
```



### 6 基础-vuex-总结

> 场景:复杂的vue项目 

> 组成:三部分 
>
> state:数据声明   -> 计算属性
>
> mutations:同步方法 修改state->methods
>
> actions:方法 和后台交互的异步方法,比如ajax -> methods

> getters:声明复杂的state数据->计算属性

### 7-案例-vuex-豆瓣电影-效果演示

1. 头部
2. 侧边栏->导航->routerlink
3. 列表+详情

> 目的:练习vuex在vue项目开发是如何使用的!

#### 01-案例-vuecli3-搭建项目

>  vue create 项目名
>
> default(babel+eslint) + 自己选择功能
>
> cd 目录
>
> npm run serve->
>
> 1. localhost:8080
> 2. http://10.254.2.123:8082/  -> 使用第二个
>
> 快速调整模板内容

#### 02-案例-vuex-豆瓣电影-准备代码分析

> 02-其他资源/douban文件夹->放在cli3的目录下的对应位置

1. main.js 入口 挂载路由
2. router/index.js  路由配置文件
3. views/非公共组件 
   1. 列表.vue
   2. 详情.vue
4. components/公共组件
   1. 头部
   2. 侧边栏 -> router-link
5. assets/css/自己的样式文件

> 注意:  bootstrap@3.3.7 

#### 03-案例-vuex-豆瓣电影-安装第三方资源

1. npm i vue-router vuex bootstrap@3.3.7

#### 04-案例-vuex-豆瓣电影-配置 vuex

1. 新建store/index.js -> 仓库入口文件  modules:{}
2. 新建store/movielist.js->专门管理列表组件的数据的模块 -> state/action/mutations

#### 05-案例-vuex-豆瓣电影-配置列表数据处理模块

> store/movielist.js -> 配合movie-list.vue组件使用的

```js
 state: {
        title: "",
        subjects: []
    },
    mutations: {
        setTitle(state, payload) {
            state.title = payload.title;

        },
        setSubjects(state, payload) {
            state.subjects = payload.subjects;
        }
    },
    actions: {
        setTitle(context) {
            // 异步操作
        },
        setSubjects(context) {
            // 异步操作
        }
    }

```

> state中的数据 -> 计算属性



#### 06-案例-vuex-豆瓣电影-列表-state-mutations-actions-jsonp

1. 获取数据->异步操作->ajax->actions
2. 豆瓣api有效->支持jsonp->axios不支持jsonp->安装jsonp

```js
 actions: {
        setMovie(context) {
            // 异步操作->发送请求获取数据 -> axios -> 自带的api不支持jsonp -> jsonp包
            // 豆瓣API 支持jsonp 
            jsonp(`http://api.douban.com/v2/movie/in_theaters`, (err, data) => {
                console.log(data); // title subjects
                // context.commit("setTitle",data);
                // context.commit("setSubjects",data);
                context.commit("setMovie", data);

            })


        },
        setSubjects(context) {
            // 异步操作
        }
    }
```

`列表组件`

```js
 methods: {
    ...mapActions(["setMovie"])
  },
   created() {
    this.setMovie();
  },

```



#### 7-案例-vuex-豆瓣电影-列表-开启命名空间

1. 数据管理模块  movielist.js  开启命名空间 namespaced:true
2. 使用的组件中  ...mapState("store/index.js/modules/模块名" , ["title"])

#### 88-案例-vuex-豆瓣电影-列表-watch 监测路由

> 场景: 不同path对应同一个组件->列表组件->组件会被复用->钩子函数created不会再次执行->
>
> 解决方案: watch监测$route -> 点击不同link时->path不同->触发watch->this.$setMovie(to)->重新按照新标识发请求



#### 9-案例-vuex-豆瓣电影-列表-渲染数据

1. state 声明数据 subjects:[]
2. mutaions->setMovei(state,payload){修改状态state.subjects=payload.subjects}
3. actions->setMovie(context,payload){异步操作获取结果->commit("mutations中的方法",异步操作的结果data)}
4. 把actons中的setMovie->组件methods方法->this.setMovie("路由配置对象->path")
5. state->变成组件的计算属性 -> {{subjects}}

#### 10-案例-vuex-豆瓣电影-列表-vuex-router-sync

> vuex默认管理组件数据->vuex管理路由数据->vuex-router-sync

1. npm 
2. main.js 配置
3. 仓库对象context里面有了路由数据

#### 11-案例-vuex-豆瓣电影-详情-配置路由

```html
 <router-link 
      :to="{name:'moviedetail',params:{id:item.id}}">
        <div class="media-left">
          <img :src="item.images.small" alt="海报点击链接">
        </div>
      </router-link>
```



#### 12-案例-vuex-豆瓣电影-详情-渲染数据

1. 提供了详情组件的数据管理模块->moviedetail.js
2. state:{movie}   -> 组件的计算属性
3. mutations:{setMovie(state,payload)}
4. actions:{setMovie(context){jsonp+提交mutations}}  -> 组件的methods

> 测试时 详情图片无法获取  -> 和代码无关 -> 豆瓣接口的问题

