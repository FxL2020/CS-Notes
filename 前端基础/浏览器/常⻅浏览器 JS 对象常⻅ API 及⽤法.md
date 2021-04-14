### 常⻅浏览器 JS 对象常⻅ API 及⽤法

### 常见浏览器 JS对象 常见API以及用法

#### 什么是浏览器对象模型
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
