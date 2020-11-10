
### Router路由
```js
<div id="#app">//根节点标签<br>
```
```js
<router-link to="/foo">go</router-link><br>
```
使用router-link组件来导航<br>
通过to属性指定链接  组件path<br>
默认会被渲染成一个a标签<br>

<router-view></router-view><br>
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










</div>
