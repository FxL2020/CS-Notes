# Vue 路由及异步组件

## 前端路由 router 原理及表现

### 背景

路由全部都是由服务端控制的，前端代码和服务端代码过度融合在一起。

客户端/前端发起 http 请求 -> 服务端 -> url 路径去匹配不同的路由/返回不同的数据。

优点：ssr，因为直接返回一个 html，渲染了页面结构。SEO 的效果非常好，首屏时间特别快。

在浏览器输入一个 url 开始 < - > 页面任意元素加载出来/渲染出来 => 首屏时间

缺点：前端代码和服务端代码过度融合在一起，开发协同非常的乱。服务器压力大，因为把构建 html 的工作放在的服务端。

### Ajax

 异步请求，浏览器端异步请求获取所需数据。

### 单页应用

页 -> html 文件
单页 -> 单个 html 文件。 （以前 user/index.html, foods/index.html）

特点：

1. 页面中的交互是不刷新的页面的，比如/home -> /about ,比如点击按钮，比如点击出现一个弹窗
2.加载过的公共资源，无需再重复加载。除了首页之外的其他页面，都通过异步组件的方式注册

支撑起单页应用这种特性的是什么？


### 多页
一个团队可能维护多个业务，业务又存在一些共同点没办法拆分为多个项目


## vue.js router 使用详解


# 前端路由 router 原理及表现

vue -> hash, history
react -> hash, history

1. 页面间的交互不刷新页面
2. 不同 Url/路由 会渲染不同的内容

路由有两种

Hash 和 History

1. hash 有#,history 没有
2. hash 的#部分内容不会给服务端， history 的所有url内容都会给服务端
3. history路由，应用在部署的时候，需要注意html文件的访问
4. hash 通过 hashchange 监听变化，history 通过 popstate 监听变化

## Hash

### 特性

1. url 中带有一个#符号，但是#只是浏览器端/客户端的状态，不会传递给服务端。

www.baidu.com/#/user -> http -> www.baidu.com/
www.baidu.com/#/list/detail/1 -> http -> www.baidu.com/

2. hash 值的更改，不会导致页面的刷新

location.hash = '#aaa';
location.hash = '#bbb';
从#aaa 到#bbb，页面是不会刷新的

3. hash 值的更改，会在浏览器的访问历史中添加一条记录。所以我们才可以通过浏览器的返回、前进按钮来控制 hash 的切换

4. hash 值的更改，会触发 hashchange 事件
   location.hash = '#aaa';
   location.hash = '#bbb';

   window.addEventLisenter('hashchange', () => {})

### 如何更改 hash

1. location.hash

location.hash = '#aaa';
location.hash = '#bbb';

2. html 标签的方式


```js
<a href="#user"> 点击跳转到 user </a>

location.hash = '#user';


```
## History

hash 有个#符号，不美观，服务端无法接受到 hash 路径和参数

html5 history

```js
window.history.back(); // 后退  <br>
window.history.forward(); // 前进 <br>
window.history.go(-3); // 接收number参数，后退三个页面 <br>
window.history.pushState(null, null, path); //push一个记录  页面的浏览记录里面会添加一个历史记录 <br>
window.history.replaceState(null, null, path); //替换掉当前的历史记录 <br>

history api不会刷新页面
```

### pushState/replaceState 的参数

1. state, 是一个对象，是一个与指定网址相关的对象，当 popstate 事件触发的时候，该对象会传入回调函数  <br>
2. title, 新页面的标题，浏览器支持不一，null  <br>
3. url, 页面的新地址  <br>

pushState, 页面的浏览记录里添加一个历史记录  <br>
replaceState, 替换当前历史记录  <br>

### History 的特性

！！面试题
pushState 时，会触发 popstate 吗？

1. 不会#
2. pushState/replaceState 并不会触发 popstate 事件， 这时我们需要手动触发页面的重新渲染。  <br>
3. 我们可以使用 popstate 来监听 url 的变化  <br>
4. popstate 到底什么时候才能触发。  <br>
   4.1 点击浏览器后退按钮  <br>
   4.2 点击浏览器前进按钮  <br>
   4.3 js 调用 back 方法  <br>
   4.4 js 调用 forward 方法  <br>
   4.5 js 调用 go 方法  <br>


### Nginx配置

1. index.html存在服务器本地
 访问www.xiao.com/a/
 访问www.xiao.com/a/

 访问main会去访问，当前这个目录下index.html文件
```nginx
location / {
     try_files $uri $uri/ /home/dist/index.html
}
```

2. index.html 存在远程地址. oss/cdn

nginx 配置再a服务器， index.html 被传到cdn上

www.xiao.com/main/a/

www.xiao-cdn.com/file/index.html

```nginx
location /main/  {
     rewrite ^ /file/index.html break
     proxy_pass https://www.xiao-cdn.com
}
```
