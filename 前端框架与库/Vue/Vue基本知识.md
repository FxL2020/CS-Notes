#### 1.方法和函数
方法：method //定义在类里面      <br>
函数：function   <br>

#### 2.生命周期
一个事物从诞生到消亡的过程   <br>
hook:钩子   <br>
回调函数   <br>

#### 3.MVVM概念

#### 4.代码规范
缩进 2个空格   <br>
westrom ->setting ->Editor->Code Style ->html/js ->tab size/intent设置成2   <br>

#### 5.v-html
{{}}：会将html代码一起显示出来   <br>
v-html:会将string的html解析出来并且进行渲染   <br>
{{src}}   <br>
<h2 v-html="src"></h2>   <br>
vue p16
#### 6.v-bind:
动态绑定属性 简写 :     <br>
- 对象语法
- 数组语法
```js
<tr :class="{'类名': boolean1,'类目2'：boolean2}">Hello World</tr>   
<tr :class="['ie','rt']">Hello World</tr>   
```

#### 7.v-style
```js
<h2 :style="{'fontSize': '50px'}">Hello World</h2>
<h2 :style="{'fontSize': 50px}">Hello World</h2>  //会把50px当成变量
```
#### 8.计算属性
```js
computed:{
totalprice(){
return this.m1+' '+this.m2
}，
{{totalprice}}
//每个计算属性都包含一个getter和一个setter,一般只使用getter
fullname:{  简写    fullname()
get(){            {return 123}
return 123;
}
}
}
```
{{totalprice}}      <br>
{{totalprice}}     <br>
计算属性会进行缓存，如果多次使用时，计算属性只会调用一次

#### 9.事件监听
v-on:click 简写 @click      <br>
修饰符      <br>
.stop 阻止冒泡      <br>
```js
<div @click="divClick">
    aaa
    <button @click.stop="butClick">点我</button>
</div>  //点击按钮阻止divClick方法执行
```
.prevent 阻止默认行为
```js
<form action="baidu">
    <input type="submit" value="12" @click.prevent="">
</form>  //阻止点击默认提交手动提交
```
keyup监听某个键盘的键帽
```js
<input type="text" @keyup.enter="submit">   //监听回车键
```
#### 10.v-on 参数
@click调用methods里面的方法时，不需要参数可以不带()      <br>
1，如果方法本身中有一个参数，那么会默认将原生事件event参数传递进去      <br>
2，如果需要同时传递某个参数，同时需要event时，可以通过$event传入事件


#### 11.对象增强写法

### 12 v-if,v-else,v-else-if
```js
 <span v-if="flag">用户账号
  <input key="username"></span>
 <span v-else>用户邮箱
  <input key="address"></span>
 <button @click="flag=!flag">切换</button>
```
切换小问题：有输入内容的情况下，切换了类型，我们会发现文字依然显示之前的输入的内容。  <br>
原因：Vue在进行DOM渲染时，出于性能考虑，会尽可能的复用已经存在的元素，而不是重新创建新的元素。  <br>
解决：我们不希望Vue出现类似重复利用的问题，可以给对应的input添加key  <br>
```js
<span v-if="<input v-model="" >
<span v-if="<input v-model="" >
```


### 13 v-show,v-if
v-if当条件为false时，压根不会有对应的元素在DOM中    <br>
v-show当条件为false时，仅仅是将元素的display属性设置为none而已，DOM元素还是存在的。    <br>
如何选择：    <br>
当需要在显示与隐藏之间切片很频繁时，使用v-show    <br>
当只有一次切换时，通过使用v-if    <br>

### 14 v-for
```js
 <li v-for="(item,index) in data">
        {{index}}.{{item}}
    </li>
```
### 15 v-for绑定key
vue中列表循环需加:key="唯一标识" 唯一标识可以是item里面id index等，因为vue组件高度复用增加Key可以标识组件的唯一性，为了更好地区别各个组件 key的作用主要是为了高效的更新虚拟DOM

简单地理解，无：key属性时，状态默认绑定的是位置；有：key属性时，状态根据key的属性值绑定到了相应的数组元素。

链接：https://www.jianshu.com/p/4bd5e745ce95

### 16 v-model
v-model其实是一个语法糖，它的背后本质上是包含两个操作：     <br>
1.v-bind绑定一个value属性    <br>
2.v-on指令给当前元素绑定input事件    <br>
```js
<input type="text" v-model="message">
等同于
<input type="text" v-bind:value="message" v-on:input="message = $event.target.value">
```
$event.target.value    <br>
触发input事件时，$event是当前的事件对象，$event.target.value指的是当前input的值    <br>

修饰符
- lazy  lazy修饰符可以让数据在失去焦点或者回车时才会更新
- number  number修饰符可以让在输入框中输入的内容自动转成数字类型
- trim  trim修饰符可以过滤内容左右两边的空格
```js
v-model.trim="message"
```
v-model结合radio 多个单选框


```js
v-for="(item,index) in array" :class="{active:currentIndex===index}" @click="change(index)"
{{item.price | showPrice}}
change(index){this.currentIndex=index}
```
### 过滤器
```js
filters:{
   showPrice(price){return '￥'+price.toFixed(2);}
}
```

P43

### 16 数组中哪些方法是响应式的
push    <br>
pop :删除数组最后一个元素    <br>
shift: 删除数组第一个元素    <br>
unshift: 在数组前面添加元素    <br>
splice: 删除元素/插入元素/替换元素    <br>
splice(index,len):从第index那个元素起删除len个元素 只传一个index就删除后面所有的元素    <br>
splice(index,len,'a','b','c'): 替换    <br>
splice(index,0,'a','b','c'): 插入    <br>
sort: 排序    <br>
reverse(): 反转

注意：通过索引修改数组中的值不会渲染dom不是响应式的
array.splice(0,1,'a'): 通过索引修改第一个元素



vue P38
vue P52
### 组件
提供了一种抽象，让我们可以开发出一个个独立可复用的小组件来构造我们的应用    <br>
任何的应用都会被抽象成一颗组件树    <br>

注册组件基本步骤
- 创建组件构造器对象
- 注册组件
- 使用组件
1.调用Vue.extend()方法创建组件构造器  <br>
调用Vue.extend()创建的是一个组件构造器。   <br>
通常在创建组件构造器时，传入template代表我们自定义组件的模板。  <br>
该模板就是在使用到组件的地方，要显示的HTML代码。  <br>

2.调用Vue.component()方法注册组件  <br>
需要传递两个参数：1、注册组件的标签名 2、组件构造器  <br>
3.再Vue实例的范围内使用组件  <br>
#### 全局组件和局部组件
全局组件：可以在Vue多个实例下使用
局部组件：在某个Vue实例里创建
components:{
cpn:cpn
}
开发中一般局部组件用的多
#### 父组件和子组件
可以在父组件中注册子组件//Vue实例也可以看成一个组件

#### 组件的语法糖注册方式

```js
- 注册全局组件
Vue.component(组件标签名,{
    template:'
    <div>
   </div>
    '
})
- 注册局部组件
components:{
cpn:{
 template:'
    <div>
   </div>
    '
}
- 创建组件构造器
const myComponent = Vue.extend({
 template:'
    <div>
   </div>
    '
})
注册组件
Vue.component('my-con',myComponent);
```
#### 组件模板分离写法
Vue提供了两种方案来定义HTML模块内容：  <br>
使用<script>标签  <br>
使用<template>标签  <br>
```js
- 注册局部组件
    
<template id="myCnp">
    div>
   </div>
</template> 
components:{
cpn:{
 template:'#myCnp'
}

```

#### 为什么组件data必须是函数
组件是一个单独功能模块的封装，不能直接访问Vue实例数据
data必须是一个函数，并且这个函数返回一个对象，数据保存在对象里面
一个组件可以有多个组件实例对象
在于Vue让每个组件对象都返回一个新的对象，因为如果是同一个对象的，组件在多次使用后会相互影响
内存地址不一样

### 父子组件间通信
1.通过props(properties)向子组件传递数据  <br>
2.通过事件(自定义事件$emit)向父组件发送消息  <br>
注意：v-bind:不支持驼峰命名，
需要把myName->my-name
props:[`myName`]
:my-name="父组件值"

子组件发生点击事件，父组件需要知道点击那个  <br>
在子组件中，通过$emit('事件',item)来触发事件。  <br>
在父组件中，通过v-on来监听子组件事件。  <br>

props的值有两种方式：  <br>
方式一：字符串数组，数组中的字符串就是传递时的名称。  <br>
方式二：对象，对象可以设置传递时的类型，也可以设置默认值等。  <br>
```js
- 字符串数组
<cpn :message="message1"></cpn>
<template id="myCnp">
    div>
   </div>
</template> 
components:{
data:{
message1:"123"
}
cpn:{
 template:'#myCnp',
 props: ['message']
}

```
- 对象类型
需要对props进行类型等验证时，  <br>
验证都支持哪些数据类型呢  <br>
String
Number
Boolean
Array
Object
Date
Function
Symbol
```js
props:{
//多个可能的类型
propa:[String,Number]，
```

自定义事件的流程：  <br>
在子组件中，通过$emit()来触发事件。  <br>
在父组件中，通过v-on来监听子组件事件。  <br>
```js
父组件中
<cpn @increate="change"></cpn>
子组件中
increate()
{this.counter++;
this.$emit('increate',this.counter)
}
//通过@increate监听事件
```
v-on:click   //监听click事件  <br>
v-on:increate/@increate    //监听自定义事件increate  <br>

### 父子组件之间访问方式
父组件访问子组件：使用$children或$refs  <br>
子组件访问父组件：使用$parent  <br>
this.$children是一个数组类型，它包含所有子组件对象。  <br>
遍历，访问子组件的属性和方法  <br>
- 一般使用$refs
- 子访问父组件
this.$parent  开发中不建议这么做




### Vue中 $ref 的用法
vm.$refs 一个对象，持有已注册过 ref 的所有子组件（或HTML元素）  <br>
使用：在 HTML元素 中，添加ref属性，然后在JS中通过vm.$refs.属性来获取  <br>
注意：如果获取的是一个子组件，那么通过ref就能获取到子组件中的data和methods  <br>
```js
<div id="app">
<h1 ref="h1Ele">这是H1</h1>

<button @click="getref">获取H1元素</button>
</div>
获取注册过 ref 的所有组件或元素
methods: {
getref() {
// 表示从 $refs对象 中, 获取 ref 属性值为: h1ele DOM元素或组件
console.log(this.$refs.h1Ele.innerText);
this.$refs.h1ele.style.color = 'red';// 修改html样式
console.log(this.$refs.ho.msg);// 获取组件数据
console.log(this.$refs.ho.test);// 获取组件的方法
}
}
```



### 插槽 slot
组件的插槽也是为了让我们封装的组件更加具有扩展性。  <br>
让使用者可以决定组件内部的一些内容到底展示什么  <br>
在子组件中，使用特殊的元素<slot>就可以为子组件开启一个插槽。  <br>
该插槽插入什么内容取决于父组件如何使用。  <br>
    具名插槽
```js
 <slot name="left">12</slot>   
    使用
  <span slot="">34</span>
```
    作用域插槽
    父组件替换插槽的标签，但是内容由子组件来提供

### 前端模块化


vue P74 P75之后补上

-》P91
vue-cli

### vue-router
路由（routing）就是通过互联的网络把信息从源地址传输到目的地址的活动。  <br>

### 后端渲染和前端渲染
后端渲染：  <br>
JSP  <br>
后端路由：  <br>
后端处理url和和页面之间的映射关系  <br>

前后端分离  <br>
后端只负责提供数据，不负责任何阶段的内容  <br>

前端渲染：  <br>
浏览器中显示网页大部分中内容，都是由前端写的js代码在浏览器中执行，最终渲染的网页  <br>

单页面富应用阶段:  <br>
其实SPA最主要的特点就是在前后端分离的基础上加了一层前端路由.  <br>
也就是前端来维护一套路由规则.  <br>
前端路由的核心是什么呢？  <br>
改变URL，但是页面不进行整体的刷新。  <br>

### URL的hah 和html5的history
URL的hash  <br>
URL的hash也就是锚点(#), 本质上是改变window.location的href属性.  <br>
我们可以通过直接赋值location.hash来改变href, 但是页面不发生刷新  <br>

HTML5的history模式：pushState 
压栈  改变href, 但是页面不发生刷新  <br>
HTML5的history模式：replaceState  <br>
替换上一个url  <br>
HTML5的history模式：go  <br>
因为 history.back() 等价于 history.go(-1)  <br>//移除栈顶元素
history.forward() 则等价于 history.go(1)  <br>
这三个接口等同于浏览器界面的前进后退。  <br>
URL的hash
HTML5的history
默认情况下, 路径的改变使用的URL的hash.
如果希望使用HTML5的history模式, 非常简单, 进行如下配置即可:
```js
const router = new VueRouter({
  routes,
  mode: 'history'
});
```

### router-link router-view
<router-link>: 该标签是一个vue-router中已经内置的组件, 它会被渲染成一个<a>标签.  <br>
<router-view>: 该标签会根据当前的路径, 动态渲染出不同的组件.  <br>
网页的其他内容, 比如顶部的标题/导航, 或者底部的一些版权信息等会和<router-view>处于同一个等级.  <br>
在路由切换时, 切换的是<router-view>挂载的组件, 其他内容不会发生改变  <br>
    
### 代码跳转路由
Vue-router给每个组件都添加一个$router
```js
data(){return {
$router: ""
}}
```
$router就是new Router()对象
```js
this.$router.push('/home')
this.$router.place('/home')
```
this.$route           <br>
那个路由活跃就是那个路由   <br>
This.$route.params.userid 获取id
### 动态路由
```js
<router-link :to="'/user/'+userid">用户</router-link>
  {
            path: '/user/:id',
            component: ShopNumBing,       
          },
 This.$route.params.userid 获取id
 ```
 

 
 ### 懒加载
 当打包构建应用时，Javascript 包会变得非常大，影响页面加载。          <br>
如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样就更加高效了          <br>

路由懒加载的主要作用就是将路由对应的组件打包成一个个的js代码块.          <br>
只有在这个路由被访问到的时候, 才加载对应的组件          <br>
```js
const Home =()=>import("./");
```
一个懒加载路由，打包之后js下就多一个js文件

### 嵌套路由


在home页面中, 我们希望通过/home/news和/home/message访问一些内容.          <br>
一个路径映射一个组件, 访问这两个路径也会分别渲染两个组件.          <br>

实现嵌套路由有两个步骤:          <br>
创建对应的子组件, 并且在路由映射中配置对应的子路由.          <br>
在组件内部使用<router-view>标签.          <br>

### vue-router 参数传递
传递参数主要有两种类型: params和query         <br>
1 动态路由         <br>
params的类型:         <br>
配置路由格式: /router/:id         <br>
传递的方式: 在path后面跟上对应的值         <br>
传递后形成的路径: /router/123, /router/abc         <br>
```js
取值：
 This.$route.params.userid
 ```
 2 
query的类型:         <br>
配置路由格式: /router, 也就是普通配置        <br>
传递的方式: 对象中使用query的key作为传递方式        <br>
传递后形成的路径: /router?id=123, /router?id=abc        <br>
```js
1,
this.$router.push('/user/'+userid)
this.$router.push({path: `/TeamremuDetail/${item.id}/02`})
${}  插入变量
2,
this.$router.push({name:'ItemDetail', query: {id:item.id,num:item.num,status:item.dishesStatus}})

this.$router.push({
  path:'/profile',
  query: {
    id: id,
    name: name
  }
})
取值
 This.$route.query.id
```

### vue-router router和route
router为VueRouter的实例，相当于一个全局的路由器对象，里面含有很多属性和子对象，例如history对象..经常用的跳转链接就可以用this.$router.push，和router-link跳转一样        <br>
this.$router.push会往history栈中添加一个新的记录        <br>
route相当于当前正在跳转(处于活跃)的路由对象。。可以从里面获取name,path,params,query等        <br>

所有的组件都继承Vue类的原型        <br>


### 组件使用
两种写法，默认第二种        <br>
1 <HomeNew></HomeNew>            <br>
2 <home-new></home-new>        <br>

### 全局导航守卫
vue-router提供的导航守卫主要用来监听监听路由的进入和离开的.        <br>
vue-router提供了beforeEach和afterEach的钩子函数, 它们会在路由即将改变前和改变后触发.        <br>

meta: 元数据(描述数据的数据)
```js
export type NavigationGuard<V extends Vue = Vue> = (
  to: Route,
  from: Route,
  next: NavigationGuardNext<V>
) => any

前置守卫
//路由跳转
router.beforeEach((to, from, next) => {
//从from跳转到to
  next();
})
后置钩子
router.afterEach((to, from, next) => {
//从from跳转到to
})
不需要next()

```
导航钩子的三个参数解析:        <br>
to: 即将要进入的目标的路由对象.        <br>
from: 当前导航即将要离开的路由对象.        <br>
next: 调用该方法后, 才能进入下一个钩子.        <br>


render函数挂载在dom上后调mounted函数

P119-P125

### promise
Promise是异步编程的一种解决方案        <br>
一种很常见的场景应该就是网络请求        <br>
	封装一个网络请求的函数，因为不能立即拿到结果        <br>
    往往我们会传入另外一个函数，在数据请求成功时，将数据通过传入的函数回调出去。        <br>
    异步操作
  ```js
    <script>
    setTimeout(()=>{
        console.log("hello world")
    },9000)
</script>
```
promise对异步操作进行封装
  ```js
<script>
  /*  setTimeout(()=>{
        console.log("hello world")
    },9000)*/
//promise是一个对象，传一个函数，函数里面两个参数resolve,reject又是函数
  new Promise((resolve,reject)=>{
      setTimeout(()=>{
          console.log("wait 第一次1秒");//等待两秒第一个执行
          setTimeout(()=>{
              console.log("wait 第二次");//等待五秒第二个执行
              setTimeout(()=>{
                  console.log("第三个")//等待1秒第三个执行
              },1000)
          },5000)
      },2000)
  })
</script>
  ```
  
  //链式编程
  
 ```js
 
 new Promise((resolve,reject)=>{
     //第一次请求
     setTimeout(()=> {
         resolve()
     },2000)
 }).then(()=>{
     //第一次结果
     console.log("wait 第一次1秒");//等待两秒第一个执行
     return new Promise((resolve,reject)=>{
         //第二次请求
         setTimeout(()=>{
         //异步操作完成调用resolve
             resolve()
         },5000)
     }).then(()=>{
         //第二次结果
         console.log("wait 第二次");//等待五秒第二个执行
     })
 })
 
```
 一般情况下，有异步操作，使用promise对这个异步操作进行封装        <br>
 异步操作之后会有三种状态        <br>
我们一起来看一下这三种状态:        <br>
pending：等待状态，比如正在进行网络请求，或者定时器没有到时间。        <br>
fulfill：满足状态，当我们主动回调了resolve时，就处于该状态，并且会回调.then()        <br>
reject：拒绝状态，当我们主动回调了reject时，就处于该状态，并且会回调.catch()        <br>
第二中写法，then传入两个方法一个是成功，一个是失败
  ```js
new Promise((resolve,reject)=>{
      //第一次请求
      setTimeout(()=> {
          resolve();
          reject();
      },2000)
  }).then((data)=>{

  },(err)=>{

  })
  ```
  
  promise的all方法<br>
  当两个结果都获得时进入then方法
  
   ```js
   Promise.all([
      new Promise((resolve,reject)=>{
        /*  $.ajax({
              url:'url1',
              success:function (data) {
                  resolve(data)
              }
          })*/
          setTimeout(()=>{
              resolve('result1')
          },3000)

      }),
      new Promise((resolve,reject)=>{
        /*  $.ajax({
              url:'url2',
              success:function (data) {
                  resolve(data)
              }
          })*/
          setTimeout(()=>{
              resolve('result2')
          },1000)
      })
  ]).then(results=>{
      console.log(results);
  })
  ```
  
  P129-P142
  
  ### 网络模块封装
  axios        <br>
  在浏览器中发送 XMLHttpRequests 请求        <br>
在 node.js 中发送 http请求        <br>
支持 Promise API        <br>
拦截请求和响应        <br>
转换请求和响应数据        <br>
等等        <br>
支持多种请求方式:       <br>
axios(config)       <br>
axios.request(config)       <br>
axios.get(url[, config])       <br>
axios.delete(url[, config])       <br>
axios.head(url[, config])       <br>
axios.post(url[, data[, config]])       <br>
axios.put(url[, data[, config]])       <br>
axios.patch(url[, data[, config]])       <br>

1安装
   ```js
npm install axios --save
   ```
   简单的封装请求
   //使用全局的axios和相关配置
   ```js
    axios({
        url:''
	method: ''  //指定请求方式
    }).then(data=>{
        console.log(data)
    })
 
    默认get请求
    
     //axios发送并发请求
    axios.all([axios({
        url: ''
    }),axios({
        url: '',
        params:{

        }
    })]).then(data=>{

    })
    
    //设置axios全局配置
    axios.defaults.baseURL='http://12.34.34.45:8000';
    axios.defaults.timeout=5000

   ```
get ->params:{key:'value'}    <br>
post  ->请求体 data:{key:'value'}

模块化封装请求接口

 ```js
 export function quest(config) {
        return new Promise((resolve,reject)=>{
            //创建axios实例
            const instant1= axios.create({
                baseURL: 'http:23.45.23.13:9000',
                timeout: 4000
            })
	      //axios拦截器
	      //instant1.interceptors.response 响应拦截
            instant1.interceptors.request.use(config=>{
                //拦截请求
                console.log(config)
                return config  //返回
            },err=>{
                console.log(err)
            })
	   /*  instant1.interceptors.response.use(res=>{
                //拦截响应
                console.log(res)
		console.log(res.data)
                return res.data  //返回
            },err=>{
                console.log(err)
            })*/
            //发送真正的网络请求
            instant1(config).then(res=>{
                resolve(res)
            }).catch(err=>{
                reject(err)
            })
        })
    }
    
 ```
    调用   
 ```js 
     quest({
        url:'/home/data',
    }).then(res=>{
        console.log(res)
    }).catch(err=>{
        console.log(err)
    })
   ```
    
    
### axios拦截器

axios提供了拦截器，用于我们在发送每次请求或者得到相应后，进行对应的处理              <br>
请求拦截作用：              <br>
1 某些config中的信息不符合服务器要求需要转化              <br>
2 每次发送网络请求时，都希望在界面中显示一个请求的图标              <br>
3 某些网络请求比如登录(token),必须携带一些特殊信息，如登录信息              <br>

  P148  
  
  ### Vuex
  
  #### 概述

使用Vuex统一管理状态的好处<br>             <br>
好处：             <br>
- 能够在vuex中集中管理共享的数据，易于开发和后期维护             <br>
- 高效的实现组件之间的数据共享，提高效率             <br>
- 存储在vuex中的数据都是响应式的，能够实时保持数据与页面的             <br>
Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。             <br>
它采用 集中式存储管理 应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。             <br>
Vuex 也集成到 Vue 的官方调试工具 devtools extension，提供了诸如零配置的 time-travel 调试、状态快照导入导出等高级调试功能。             <br>

可以简单的将其看成把需要多个组件共享的变量全部存储在一个对象里面。             <br>
然后，将这个对象放在顶层的Vue实例中，让其他组件可以使用。             <br>
Vuex就是为了提供这样一个在多个组件间共享状态的插件 响应式             <br>

所有的组件都继承Vue prototype            <br>
加入一个对象所有组件共享，但不是响应式的            <br>

多个组件间共享的呢？            <br>
如果你做过大型开放，你一定遇到过多个状态，在多个界面间的共享问题。            <br>
比如用户的登录状态、用户名称、头像、地理位置信息等等。            <br>
比如商品的收藏、购物车中的物品等等。            <br>
这些状态信息，我们都可以放在统一的地方，对它进行保存和管理，而且它们还是响应式的            <br>

- 单界面的状态管理

单个组件State：不用多说，就是我们的状态。（你姑且可以当做就是data中的属性）            <br>
View：视图层，可以针对State的变化，显示不同的信息。（这个好理解吧？）            <br>
Actions：这里的Actions主要是用户的各种操作：点击、输入等等，会导致状态的改变。            <br>

1,引用插件
 ```js 
npm install vuex --save
 ```
2,新建store文件夹
 ```js 
import Vue from "vue";
import Vuex from "vuex";
//安装插件
Vue.use(Vuex);
//创建对象
//导出对象
export default new Vuex.Store({
  state: {},
  mutations: {},
  actions: {},
  modules: {}
});

在main.js挂载
import store from "./store";
new Vue({
  router,
  store,
  render: h => h(App)
}).$mount("#app");
 ```
 全局单例模式（大管家）            <br>
我们现在要做的就是将共享的状态抽取出来，交给我们的大管家，统一进行管理。            <br>
之后，你们每个试图，按照我规定好的规定，进行访问和修改等操作。            <br>

devtools Vue开发的一个浏览器插件
记录每次更改vuex状态

vue建议通过 (actions 异步操作 网络请求) -> mutations(同步操作)修改vuex状态值

 ```js 
 
export default new Vuex.Store({
  state: {
    counter: 1000
  },
  mutations: {
    //方法 方法会默认传递一个state
    increment(state){
      state.counter++;
    },
     increment(state,count){
      state.counter+count;
    },
    decrement(state){
      state.counter--;
    }
  },
  actions: {},
  modules: {}，
  getters: {}
});

组件中
this.$store.commit('increment');
this.$store.commit('decrement');
2
fun(5){this.$store.commit('increment',count);}

devtools Vue可以跟踪每次状态变化

 ```
 
 将共享的状态抽取出来，统一进行管理，每个视图，按照我规定好的规定，进行访问和修改等操作            <br>
 Vuex背后的基本思想            <br>
 
 单一状态树           <br>
 
  ```js
  
 getters   //计算属性 方法中第二个参数是getters
 double(state,getters){
 return state.students.filter(s=>s.age>20)
 }
 使用
 组件中
 this.$store.getters.double
 
  ```
  
  mulation
  Vuex的store状态的更新唯一方式：提交Mutation            <br>
Mutation主要包括两部分：            <br>
字符串的事件类型（type）            <br>
一个回调函数（handler）,该回调函数的第一个参数就是state。            <br>

在通过mutation更新数据的时候, 有可能我们希望携带一些额外的参数
参数被称为是mutation的载荷(Payload)
 ```js

fun(5){this.$store.commit('increment',count);}

 ```
 
Vuex的store中的state是响应式的, 当state中的数据发生改变时, Vue组件会自动更新            <br>
提前在store中初始化好所需的属性.           <br>
当给state中的对象添加新属性时, 使用下面的方式:           <br>
方式一: 使用Vue.set(obj, 'newProp', 123)           <br>
方式二: 用心对象给旧对象重新赋值           <br>

	
 ```js
state.info['name']='xiaom'  //不是响应式


 ```

mutation类型常量

Vuex要求我们Mutation中的方法必须是同步方法.          <br>
主要的原因是当我们使用devtools时, 可以devtools可以帮助我们捕捉mutation的快照.          <br>
但是如果是异步操作, 那么devtools将不能很好的追踪这个操作什么时候会被完成.          <br>


 ```js
 
//导出对象
export default new Vuex.Store({
  state: {
    counter: 1000
  },
  mutations: {
    //方法 方法会默认传递一个state
    increment(state){
      state.counter++;
    },
    decrement(state){
      state.counter--;
    }
  },
  actions: {
    //context 上下文（store）
    update(context){
      setTimeout(()=>{
        context.commit('increment')
      },1000)
    }
  },
  modules: {}
});

组件中
this.$store.dispatch('update')

 ```
 
 modules模块
 
  ```js
  
modules: {
modules1:{
state
getters
..
}
}，

 ```
应用变得非常复杂时,store对象就有可能变得相当臃肿.          <br>
为了解决这个问题, Vuex允许我们将store分割成模块(Module), 而每个模块拥有自己的state、mutations、actions、getters等          <br>

使用
 ```js
 1 $store.state.a.name
 2 $store.getters.fullName
 3 
  ```
  在模块定义的对象也是在store第一层store state,getters...里

P141

    
