<!--
 * @Author: fengzp
 * @Date: 2020-09-15 12:55:14
 * @LastEditors: fengzp
 * @LastEditTime: 2020-11-25 19:42:10
 * @Introduce: Do not edit
-->
### 1 vue dom diff
虚拟dom优点：
1. 减少dom操作，

### 1 点击图片跳转到其他小程序的h5页面
```js
 my.navigateToMiniProgram({
    appId: '2018032002411058', //要跳转小程序的id
	  path:'pages/camera/camera',//要跳转小程序的具体页面
  )}
```
### 2 h5页面和小程序的双向通信
```js
// h5页面
function isAlipay(){
  return navigator.userAgent.indexOf('AlipayClient') > -1;
}
function gobackapp(id){
  if(isAlipay()){
		window.location.href = 'alipays://platformapi/startapp?
    appId=2018122662690921&
    page=%2fpages%2fproduct%2fdetail%2fdetail%3fid%3d'+id+'';
  }else{
    bridge(id);
  }
}
function bridge(a){
  window.location.href = 'https://www.zux2.com/goods/details/-1/'+a+''
}

```
```js
//小程序页面
<view a:if="{{url != ''}}">
  <web-view id="web-view-1" src="{{url}}" onMessage="messageEvent" />
</view>

```