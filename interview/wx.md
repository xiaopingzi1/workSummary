## 1 请谈谈微信小程序主要目录和文件的作用？

project.config.json 项目配置文件，用得最多的就是配置是否开启https校验；

App.js   设置一些全局的基础数据等；

App.json 底部tab, 标题栏和路由等设置；

App.wxss 公共样式，引入iconfont等；

pages 里面包含一个个具体的页面；

index.json (配置当前页面标题和引入组件等)；

index.wxml (页面结构)；

index.wxss (页面样式表)；

index.js (页面的逻辑，请求和数据处理等)；


## 2 请谈谈wxml与标准的html的异同？

都是用来描述页面的结构；  
都由标签、属性等构成；  
标签名字不一样，且小程序标签更少，单一标签更多；    
多了一些 wx:if 这样的属性以及 {{ }} 这样的表达式  
WXML仅能在微信小程序开发者工具中预览，而HTML可以在浏览器内预览  
组件封装不同， WXML对组件进行了重新封装，  
小程序运行在JS Core内，没有DOM树和window对象，小程序中无法使用window对象和document对象。

## 3 请谈谈WXSS和CSS的异同？

都是用来描述页面的样子；  
WXSS 具有 CSS 大部分的特性，也做了一些扩充和修改；  
WXSS新增了尺寸单位，WXSS 在底层支持新的尺寸单位 rpx；  
WXSS 仅支持部分 CSS 选择器；  
WXSS 提供全局样式与局部样式  

## 4 你是怎么封装微信小程序的数据请求的？

在根目录下创建utils目录及api.js文件和apiConfig.js文件；  
在apiConfig.js 封装基础的get, post 和 put， upload等请求方法，设置请求体，带上token和异常处理等；  
在api中引入apiConfig.js封装好的请求方法，根据页面数据请求的urls, 设置对应的方法并导出；  
在具体的页面中导入；

## 5 小程序页面间有哪些传递数据的方法？

使用全局变量实现数据传递  
页面跳转或重定向时，使用url带参数传递数据  
使用组件模板 template传递参数   
使用缓存传递参数  
使用数据库传递数据

## 6 请谈谈小程序的双向绑定和vue的异同？
大体相同，但小程序直接this.data的属性是不可以同步到视图的，必须调用this.setData()方法！

## 7 请谈谈小程序的生命周期函数？

onLoad() 页面加载时触发，只会调用一次，可获取当前页面路径中的参数。  
onShow() 页面显示/切入前台时触发，一般用来发送数据请求；  
onReady() 页面初次渲染完成时触发, 只会调用一次，代表页面已可和视图层进行交互。  
onHide() 页面隐藏/切入后台时触发, 如底部 tab 切换到其他页面或小程序切入后台等。  
onUnload() 页面卸载时触发，如redirectTo或navigateBack到其他页面时。

## 8 简述微信小程序原理？

小程序本质就是一个单页面应用，所有的页面渲染和事件处理，都在一个页面内进行，但又可以通过微信客户端调用原生的各种接口；  
它的架构，是数据驱动的架构模式，它的UI和数据是分离的，所有的页面更新，都需要通过对数据的更改来实现；  
它从技术讲和现有的前端开发差不多，采用JavaScript、WXML、WXSS三种技术进行开发；  
功能可分为webview和appService两个部分；  
webview用来展现UI，appService有来处理业务逻辑、数据及接口调用；  
两个部分在两个进程中运行，通过系统层JSBridge实现通信，实现UI的渲染、事件的处理等。  

## 9 请谈谈原生开发小程序、wepy、mpvue 的对比？

个人认为，如果是新项目，且没有旧的 h5 项目迁移，则考虑用小程序原生开发，好处是相比于第三方框架，坑少。  
而如果有 老的 h5 项目是 vue 开发 或者 也有 h5 项目也需要小程序开发，则比较适合 wepy 或者 mpvue 来做迁移或者开发，近期看wepy几乎不更新了，所以推荐美团的mpvue。
而如果如果团队前端强大，自己做一套框架也没问题。

## 1 聚合商城后台管理系统
该项目是以Vue全家桶搭建的电商后台管理系统，其中有登录功能、用户管理功能、权限管理功能、商品管理功能、订单管理功能以及数据统计功能。本人主要负责商品管理和数据统计功能。

1. 使用element-ui搭建商品管理页面，其中使用了element-ui中的面包屑、输入框、按钮、表格、分页等组件，其中分为商品列表，商品添加，商品分类三个子页面。
2. 商品列表页面中列表通过表格展示，通过组件库自带的分页事件，改变页码时发送新的请求来获取下一页数据，并且设置添加商品按钮通过$router.push编程式导航进入添加商品页。
3. 商品添加页面由步骤条组件以及标签页组件搭建，将两个组件的数据源绑定到同一个数据上，即可完成步骤条组件和标签页组件中的联动。
4. 标签页分为五个tab-pane，每个tab-pane中获取的数据都绑定到data中的同一个对象中，通过axios技术发送到后端，添加成功则会显示提示信息，再通过编程式导航返回到商品列表页面。
5. 商品分类页面，因为商品分类分为三级，element-ui提供的表格组件无法展开三级表格，于是采用了element-tree-grid插件（代码较少），代替了展开列的表格，完成了三级分类的展示。
6. 数据统计页面也由element-ui搭建，其中数据图表采用了echarts插件，将axios获取数据及echarts的配置项代码放入methods中的一个方法里，并用钩子函数created调用这个方法，即可点开页面展示图表。

所遇困难：编码时，每页都要引入axios并且每发送一次axios请求就要给请求头配置一次token，极为不便。

解决方法： 思路是将axios自制为vue的插件。首先建立一个单独js模块，里面建立一个空对象，使用vue的install方法，在其中将axios加入到Vue的原型链上，将其变为Vue的一个方法。并且采用axios的导航守卫，在除登录页外，每次发送axios请求前，给其请求头配置好token。最后在main.js中导入，通过vue.use配置，即可在所有页面中直接使用请求，不用引入axios也不用配置请求头。

优点：采用此种方式后，减少了许多重复的编码。

负责的模块

> 登录部分

    将axios变成vue的插件-在登录组件中直接发送请求，
    利用async和await来处理异步请求
    登录成功时，用户信息中有一个加密字符串token，
    用localStorage.setItem('token',data.token)来保存token的值

> 退出部分-清除token的值

> 进入首页需要进行权限验证-判断是否有token的值

> 遇到的坑：在设置过滤器的时候，prop后面不能直接使用过滤器

```js
<el-table-column
  prop="create_time | fmtDate" //不能用
  label="创建日期"
  width="80"
></el-table-column>

```
 * 解决方法  
   当单元格里的数据展示不是一些文本时(如：插值表达式)，需要给展示数据的外面套< template >容器

```js
//slot-scope作用是上下级传数据
<el-table :data="tableData">
  <el-table-column label="创建日期" width="80">
    <template slot-scope="scope">//slot-scope中的值会自动锁定外层的数据源,template中的组件不能使用上一级组件中的值
      {{scope.row.create_time | fmtDate}} //scope有自带属性.row,自动找到scope数组里面的对象
    </template>
  </el-table-column>
</el-table>
  ```
> 用户管理-用户列表(编辑，删除，分配角色)-添加用户  

    通过element-ui里面的面包屑（显示当前页面的路径，快速返回之前的任意页面。），
    以及搜索框(el-input)，列表(e-table)来展示页面。
    页面中有编辑，删除，以及分配角色操作

角色管理-角色列表
       -权限列表

> 数据统计

    统计报表->echarts

1. 使用Vue的组件搭建登陆，用户列表等公用页面
2. 依赖Vue中的vue-router模块和监听route，通过路由配置文件页面之间的跳转.
3. 结合Element UI实现加载动画和顶部的显示和返回
4. 使用全局的自定义过滤器Filter对涉及时间部分的数据进行处理
5. 项目中使用了axios模块，实现与后台的数据交互
6. 使用git进行版本控制管理，使用webpack进行代码压缩


## 2 小鹿森林
负责部分:用户登录，首页展示，公司介绍


1. 运用rem和flex弹性盒模型布局页面 适配不同的设备屏幕
2. 运用zepto,swiper等插件,完成移动端页面的交互以及轮播效果
3. 通过ajax技术完成数据请求并渲染页面
4. 运用iscroll插件实现页面下拉弹性效果; 
5. 与产品经理以及UI沟通讨论,优化网站的用户体验

> rem 

```html
<!-- width=device-width ：表示宽度是设备屏幕的宽度
initial-scale=1.0：表示初始的缩放比例
minimum-scale=1.0：表示最小的缩放比例
maximum-scale=1.0：表示最大的缩放比例
user-scalable=no：表示用户是否可以调整缩放比例 -->
让网页的宽度自动适应手机屏幕的宽度
   <meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no" />

<!-- 针对各个分辨率范围在html上设置font-size的代码： -->
html{font-size:10px}  
@media screen and (min-width:321px) and (max-width:375px){html{font-size:11px}}  
@media screen and (min-width:376px) and (max-width:414px){html{font-size:12px}}  
@media screen and (min-width:415px) and (max-width:639px){html{font-size:15px}}  
@media screen and (min-width:640px) and (max-width:719px){html{font-size:20px}}  
@media screen and (min-width:720px) and (max-width:749px){html{font-size:22.5px}}  
@media screen and (min-width:750px) and (max-width:799px){html{font-size:23.5px}}  
@media screen and (min-width:800px){html{font-size:25px}}

动态计算html的font-size

document.documentElement.style.fontSize = document.documentElement.clientWidth / 10 + 'px';

rem取值分为两种情况，设置在根元素时和非根元素时，举个例子

    /* 作用于根元素，相对于原始大小（16px），所以html的font-size为32px*/
    html {font-size: 2rem}
     
    /* 作用于非根元素，相对于根元素字体大小，所以为64px */
    p {font-size: 2rem}
```

## 3 鸿合科技
负责部分：首页内容展示，公司动态，产品方案里面的内容。项目为响应式开发，实现不同尺寸下的展示,用template模板引擎进行数据渲染
1. 根据 UI 设计稿，使用 bootstrap 栅格来实现页面的整体布局
2. 运用 jquery 发送ajax请求,进行前后端数据的交互
3. 运用Jquery 插件完成首页轮播图功能；
4. 运用 CSS3 变换（transform）实现元素位移等、缩放特效
5. 运用 @media 媒体查询技术，实现不同终端设备的不同渲染。
6. 运用 bootstrap 的插件 transition，实现网页自定义动画

## 10 微信小程序怎么设置转发
在app.js入口文件当中设置
```js
wx.showShareMenu({
  withShareTicket: true
})
```