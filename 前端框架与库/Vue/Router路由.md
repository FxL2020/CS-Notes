
### Router路由
#### 单html路由
```js
<div id="#app">//根节点标签<br>
```
```js
<router-link to="/foo">go</router-link><br>
```
使用router-link组件来导航<br>
通过to属性指定链接  组件path<br>
默认会被渲染成一个a标签<br>
```js
<router-view></router-view><br>
```
路由出口，路由匹配到的组件将渲染在这里<br>

如果要使用模块化编程，导入Vue和VueRouter,要调用Vue.use(VueRouter)<br>

2，定义路由，每个路由应该映射一个组件，<br>
const routers={path:'/foo',component:Foo}<br>

3，创建router实例，然后传router配置<br>
const router =new VueRouter({<br>
 routers<br>
})<br>

4, 创建和挂载根实例<br>
//记得要通过router配置参数注入路由<br>
//从而让整个应用都有路由功能<br>
const app=new Vue({<br>
router<br>
}).$mount('#app')<br>
  
npm install 启动安装<br>
npm run serve  编译项目<br>
npm run build 打包项目<br>

#### 脚手架路由
index.js/router.js文件中引入element-ui

import Vue from 'vue';  <br>
import Router from 'vue-router';  <br>
import ElementUI from 'element-ui';  <br>

Vue.use(Router)  <br>
Vue.use(ElementUI)  <br>
外面的插件包都需要使用Vue.use()  <br>
```js
new Vue
(
{
router,   //es6语法相当于router：router；
render: h->h<APP>
}
).$mount('#app');
```


使用 <router-link> 创建 a 标签来定义导航链接，我们还可以借助 router 的实例方法，通过编写代码来实现。即：通过js动态的进行导航链接。
```js
   声明式		                 编程式
<router-link :to="...">   	router.push(...)
  ```
注意：在 Vue 实例内部，你可以通过 $router 访问路由实例。因此你可以调用 this.$router.push。

想要导航到不同的 URL，则使用 router.push 方法。这个方法会向 history 栈添加一个新的记录，所以，当用户点击浏览器后退按钮时，则回到之前的 URL。

```js
//字符串
this.$router.push('h-json')
//对象
this.$router.push(path:'h-json')
//命名路由 
this.$router.push(name:'h-json')
//会在地址栏暴露参数
this.$router.push(path:'h-json',query:{age:24})
 path: "/ConsumptionActivityInquiry",
$router.push({name:'damage-query-detail', query: {id:item.id}})
获取参数
this.$route.query.id
//不会在地址栏暴露参数
router.js
  router
  path: "/ConsumptionActivityInquiry/:name/:id/:deadline",
  this.$router.push({name: 'ConsumptionActivityInquiry', params: {name: item.name,id: item.id,deadline: item.deadline}})">
this.$router.push(name:'h-json',params:{name:name,id:this.id,deadline:time})
获取传递参数
this.$route.params.id,
```
this.$router.go()    <br>
在history记录中向前，向后退多少步,相当于window.history.go(n)    <br>
router.go(1)在history记录中向前进一步    <br>
router.go(-1)在history记录中向后退一步    <br>
```js
Vue.prototype.btnBack = () => {
  if (window.history.length <= 1) {
    router.push({path:'/'});
    return false
  } else {
    router.go(-1)
  }
};
```
路由重定向
```js
 {
        path: "*",
        name: "any",
        redirect: '/login'
      //输入不存在的路由会跳转到登录页面
      },
 ```  
 组件传值
 ```js
 router.js
   path: "/ActivityPaymentDetail/:id",
   name: "ActivityPaymentDetail",
   component: ActivityPaymentDetail,
   props: {news: 'Nwes'},
 
 {{news}}
  export default {
        name: "ActivityPaymentDetail",
        components:{WebSelect,Paginator,Checkbox,Footer},
        props:['news'],
        methods:{},
 ```  
 vue-router全局守卫 局部守卫
 #### 全局前置守卫
 ```js
 router.beforeEach((to, from, next) => {
  /*路由发生改变修改页面的title */
  if(to.meta.title) {
    document.title = to.meta.title
  }
 ```
 局部组件导航守卫    <br>
 写在组件内   <br>
  ```js
 components:{WebSelect,Paginator,Checkbox,Footer},
 router.beforeRouterEnter((to, from, next) => {
 if(false){next()}
  }
  methods:{},
 ```
 
#### 获取数据loading
 导航获取数据loading功能
- 导航完成之后获取
先完成导航，在接下来的组件生命周期钩子函数中获取数据，在数据获取期间显示"加载中"之类的提示
- 导航完成之前获取
 导航完成前，在路由进入守卫中获取数据，获取成功之后导航
 router.js
  {path: "/loading",
  component: Loading,}
  
  









