
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
 
