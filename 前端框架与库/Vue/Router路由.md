
### Router路由
<div id="#app">//根节点标签
  
<router-link to="/foo">go</router-link>
使用router-link组件来导航
通过to属性指定链接  组件path
默认会被渲染成一个a标签

<router-view></router-view>
路由出口，路由匹配到的组件将渲染在这里

如果要使用模块化编程，导入Vue和VueRouter,要调用Vue.use(VueRouter)

2，定义路由，每个路由应该映射一个组件，
const routers={path:'/foo',component:Foo}

3，创建router实例，然后传router配置
const router =new VueRouter({
 routers
})

4, 创建和挂载根实例
//记得要通过router配置参数注入路由
//从而让整个应用都有路由功能
const app=new Vue({
router
}).$mount('#app')
  
npm install 启动安装
npm run serve  编译项目
npm run build 打包项目










</div>
