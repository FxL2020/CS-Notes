### 常⻅浏览器 JS 对象常⻅ API 及⽤法

#### 一、什么是浏览器对象模型
DOM: Document   <br>
BOM: Browser Object Model（浏览器对象模型）,浏览器模型提供了独⽴于内容的、可以与浏览器
窗⼝进⾏滑动的对象结构，就是浏览器提供的 API   <br>
主要对象有：

1. window 对象——BOM 的核⼼，是 js 访问浏览器的接⼝，也是 ES 规定的 Global 对象(浏览器独有)   <br>
     小程序没有window对象     <br>
     node中使用global     <br>

2. location 对象：提供当前窗⼝中的加载的⽂档有关的信息和⼀些导航功能。既是 window 对象属
性，也是 document 的对象属性    <br>
常用：    <br>
     location.href  : 可以返回到上一个页面    <br>
     location.replace : 无法返回到上一个页面  

3. navigation 对象：获取浏览器的系统信息    <br>
    window.navigation.online//判断网络
```ts
setInterval(()=>{
   window.navigation.online;
}，1000
)
```
     
4. screen 对象：⽤来表⽰浏览器窗⼝外部的显⽰器的信息等    <br>
5. history 对象：保存⽤⼾上⽹的历史信息




#### ⼆、详解浏览器事件捕获，冒泡
浏览器事件模型中的过程主要分为三个阶段：捕获阶段、⽬标阶段、冒泡阶段。<br>
如图<br>
<img src="https://user-images.githubusercontent.com/45973908/114682642-db24f700-9d41-11eb-94ce-f66c2ac9553f.jpg" width="225"  alt="知识"/>

```ts
window.addEventListener("click",()=>{},false)
```
第三个参数：    <br>
false: 在冒泡阶段进行    <br>
true: 在捕获阶段执行    <br>

实例：<br>
<img src="https://user-images.githubusercontent.com/45973908/114686270-34425a00-9d45-11eb-95eb-769737207b23.png" width="225"  alt="知识"/>

点击页面中son模块经历过程：
从顶层window开始捕获，->parent->child->到达son也即目标（目标阶段）开始向上冒泡->child->parent->window

代码实现如下：

```ts
<body>
<div id="parent">
    <p id="child">
        <span id="son">
            点我<a></a>
        </span>
    </p>
</div>
<script>
    const parent=document.getElementById('parent');
    const child=document.getElementById('child');
    const son=document.getElementById('son');
     /*
     * 场景：
     * 如果现在有一个历史页面，页面上有巨多的按钮，其他元素，都绑定了自己的click事件
     * user banned->true alert("你被封禁"),阻止原有的click事件触发
     * false 不做任何处理
     *
     * 方案
     * 1，进入页面的时候,banned,写一个全屏的透明元素，z-index:10000
     * 2，最外层的元素 或者window上，绑定事件，做事件流的拦截
     * */
     const banned=false
    window.addEventListener("click",function (e) {
        console.log('window捕获'+e.target.nodeName+e.currentTarget.nodeName)
    },true)
    parent.addEventListener("click",function (e) {
        if (banned){
            e.stopPropagation();
            window.alert("你被封禁了")
            return;
        }
        console.log('parent捕获'+e.target.nodeName+e.currentTarget.nodeName)
    },true)
    child.addEventListener("click",function (e) {
        console.log('child捕获'+e.target.nodeName+e.currentTarget.nodeName)
    },true)
    son.addEventListener("click",function (e) {
        console.log('son捕获'+e.target.nodeName+e.currentTarget.nodeName)
    },true)

    //e.target: 指当前点击的元素
    //e.currentTarget: 指绑定监听事件的元素

    window.addEventListener("click",function (e) {
        e.stopPropagation()
        console.log('window冒泡'+e.target.nodeName+e.currentTarget.nodeName)
    },false)
    parent.addEventListener("click",function (e) {
        console.log('parent冒泡'+e.target.nodeName+e.currentTarget.nodeName)
    },false)
    child.addEventListener("click",function (e) {
        console.log('child冒泡'+e.target.nodeName+e.currentTarget.nodeName)
    },false)
    son.addEventListener("click",function (e) {
        console.log('son冒泡'+e.target.nodeName+e.currentTarget.nodeName)
    },false)
</script>

控制台打印结果：

      window捕获 SPA Nundefined
      parent捕获 SPAN DIV
      child捕获 SPAN P
      son捕获 SPAN SPAN
      son冒泡 SPAN SPAN
      child冒泡 SPAN P
      parent冒泡 SPAN DIV
      window冒泡 SPAN undefined
```

#### 阻止事件传播
stopPropagation：阻止事件的传播  <br>
终止事件在传播过程的捕获、目标处理或起泡阶段进一步传播

#### 阻止默认行为
preventDefault  <br>
比如a标签跳转 <br>
点击表单的提交按钮

#### 兼容性

### 三、浏览器请求有关 ajax 及 fetch API 详解
##### ajax
1.new一个XMLHttpRequest对象    <br>
2.使用open方法创建一个新的http请求，并指定此请求的方法，url    <br>
3.给onreadystatechange属性设置一个回调函数,当readyState==4时(代表完成请求)    <br>
status等于200,请求成功，得到返回值内容    <br>
status不等于200，得到返回状态以及状态信息    <br>
4使用send方法发送请求    <br>

代码:

```ts
let xhr = new XMLHttpRequest();
xhr.open('GET', 'http://domain/service');

// request state change event
xhr.onreadystatechange = function () {
   
    if (xhr.readyState !== 4) return;//4代表完成了

    if (xhr.status === 200) {
        // request successful - show response
        console.log(xhr.responseText);
    } else {
        // request error
        console.log('HTTP error', xhr.status, xhr.statusText);
    }
};

// xhr.timeout = 3000; // 3 seconds
// xhr.ontimeout = () => console.log('timeout', xhr.responseURL);

xhr.send();
```

##### fetch
常用： node-fetch   <br>
fetch特点：   <br>
##### 1.默认不带cookie，要想自动发送cookie，加上credentials   <br>
同域：                credentials: "same-origin"   <br>
对于CORS请求：credentials: "include"   <br>

##### 2.错误不会reject，HTTP错误比如404，500不会导致fetch返回的promise标记为reject.catch()也不会被执行<br>
想要精确的判断 fetch是否成功，需要包含 promise resolved 的情况，此时再判断 response.ok是不是为 true

```ts
fetch(
        'http://domain/service', {
            method: 'GET',
           credentials: "same-origin"
        }
    )
    .then(response => {
        if (response.ok) {
            return response.json();
        }
        throw new Error('Network response was not ok.');
    })
    .then(json => console.log(json))
    .catch(error => console.error('error:', error));
```
##### 3.不支持超时
 不支持直接设置超时, 可以用promise<br>
promise中fetch()和setTimeout同时执行，谁先执行完就用谁的状态
```ts
function fetchTimeout(url, init, timeout = 3000) {
    return new Promise((resolve, reject) => {
      //1s 不超时的情况，fetch ->resolve/reject
      //3s 超时reject
        fetch(url, init)
            .then(resolve)
            .catch(reject);
        setTimeout(reject, timeout);
    })
}
```
4.中止 fetch
```ts
const controller = new AbortController();

fetch(
        'http://domain/service', {
            method: 'GET',
            signal: controller.signal
        })
    .then(response => response.json())
    .then(json => console.log(json))
    .catch(error => console.error('Error:', error));

controller.abort();

```
