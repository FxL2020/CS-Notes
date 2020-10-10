
#### JSON
JSON就是一个特殊格式的字符串，这个字符串可以被任意语言所识别，并且可以转为任意语言的对象，开发中主要用来数据交互<br>
JavaScript Object notation :JS对象表示法<br>
JSON属性名必须加双引号<br>
```html
var obj='{"name":"张三","sex":"man"}';
var arr='[1,2,"we"]'
```
JSON分类<br>
1.对象{}<br>
2.数组[]<br>

JSON值<br>
1.字符串<br>
2.数值<br>
3.布尔<br>
4.null<br>
5.对象<br>
6.数组<br>

将JSON字符串转化为JS中的对象<br>
JS中有一个工具类JSON<br>
json -> js对象<br>
```html
var obj=JSON.parse(json);
```
js对象-> json<br>
```html
var str=JSON.stringify(obj);
```
JSON对象在ie7以及一下版本不支持<br>

##### eval()
可以执行一个字符串js代码<br>
执行的字符串中有{},会把{}当着代码块，不希望当作字符串在字符串前后加()<br>
```html
var json='{"name":"wang"}'
var obj=eval("("+json+")");
```
开发中尽量不要用，性能差存在安全隐患<br>

JSON对象在ie7以及一下版本不支持解决：<br>
引入json2.js文件<br>
