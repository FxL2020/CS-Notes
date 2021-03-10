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

open(method, url, async, username, password)

method 参数是用于请求的 HTTP 方法。值包括 GET、POST 和 HEAD。大小写不敏感。   <br>
POST：用"POST"方式发送数据,可以大到4MB   <br>
GET：用"GET"方式发送数据,只能256KB   <br>
如果请求带有参数的化实用POST方式，POST方式将参数放置在页面的隐藏控件内   <br>
没有参数使用GET方式   <br>
对于请求的页面在中途可能发生更改的，也最好用POST方式   <br>

url 参数是请求的主体。大多数浏览器实施了一个同源安全策略，并且要求这个 URL 与包含脚本的文本具有相同的主机名和端口。<br>

async 参数指示请求使用应该异步地执行。如果这个参数是 false，请求是同步的，后续对 send() 的调用将阻塞，直到响应完全接收。   <br>
如果这个参数是 true 或省略，请求是异步的，且通常需要一个 onreadystatechange 事件句柄。   <br>



```js

let request = new XMLHttpRequest() //变量：{XMLHttpRequest对象}
//准备发送请求的数据：url
var url = "https:www.ertt.cn/json/?jsonid=1034";
var method ="GET";
//调用XMLHttpRequest对象的open方法
request.open(method,url,true); //初始化 HTTP 请求参数
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

```
