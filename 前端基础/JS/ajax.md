ajax:<br>
分为下面四部：<br>
1.创建ajax对象<br>
2.连接到服务器<br>
3.发送请求（告诉服务器我要什么数据）<br>
4.接受返回值<br>

XMLHttpRequest对象简介<br>
用于实现浏览器实现ajax的底层对象<br>
使得js可以直接发起HTTP请求<br>
XMLHttpRequest：是一个构造构造函数，是windows下的一个全局对象，可以new XMLHttpRequest来使用<br>


let myConsole //变量：{仿控制台组件实例对象}
$(function()) {
     myConsole = fnConsole({id : "#id_console"})//初始化控制台，并且赋值给myConsole
//变量：{需要扩展的对象}
$("#id_btn1").on("click",function(){
let request = new XMLHttpRequest() //变量：{XMLHttpRequest对象}
//准备发送请求的数据：url
var url = "https:www.ertt.cn/json/?jsonid=1034";
var method ="Get";
//调用XMLHttpRequest对象的open方法
request.open(method,url,true);
//调用XMLHttpRequest对象的send方法,get请求参数为null
request.send(null);
//为XMLHttpRequest对象添加onreadystatechange响应函数
request.onreadystatechange = function(){
//判断响应是否完成，xmlhttpprequest对象的readystate属性值为4
    if(request.readyState ==4){
//再判断响应是否可用，xmlhttprequest对象status属性值为200
      if(request.status == 200){
myConsole.print(request.responseText);
  }
}
}
}
