javascript 诞生1995 前期主要用于处理网页中前端验证
脚本语言 编程语言 解释性语言 动态语言<br>
运行在客户端的脚本语言，（script是脚本的意思）<br>
脚本语言：不需要编译，js解释器js引擎逐行解释执行<br>
也可以基于node.js技术进行服务器端编程<br>

1bit(位) 可以保存一个0或1<br>
1B(字节)=8bit<br>
1kB=1024bit<br>
CPU执行内存里的数据，把数据从硬板里读到内存<br>

浏览器执行js<br>
浏览器分为渲染引擎和js引擎<br>
渲染引擎：用来解析html，css，俗称内核 谷歌浏览器 blink<br>
js引擎：js解释器，读取网页中js代码，对其处理后运行 谷歌浏览器V8<br>

js的组成部分<br>
1 ECMAScript js语法<br>
2 DOM 页面文档对象模型<br>
标准编程接口，通过DOM提供的接口对页面上的各种元素进行处理，(大小，位置，颜色)<br>
3 BOM 浏览器对象模型<br>
通过BOM可以操作浏览器窗口，比如弹窗，获取分辨率<br>

js位置<br>
行内，内嵌，外部<br>
```html
<script type="text/script" src="位置"
```
单行注释 // 快捷键 ctrl+ /<br>
多行 /* */ shift+ alt+a<br>

输入输出<br>
alert(msg)<br>
console.log(smg) 浏览器控制台输出打印信息<br>
prompt(info） 浏览器弹出输入框，用户可以输入<br>
一个网页就是一个文档document//可以向body中输入一个内容
```html
document.write("内容");
```


变量<br>
内存中存放数据的空间<br>
var age;<br>
var age,name,sex;<br>
未赋值，undefined未定义<br>
var myname=prompt('');取过来的值是字符串<br>
变量未声明，未赋值使用会报错<br>
未定义，直接赋值可以使用不推荐<br>
严格区分大小写<br>
每一条语句都已分号结尾;<br>
js会忽略多个空格和换行<br
字面量：不可改变的值，可以直接使用，一般使用变量保存字面量<br>
标识符一般采用驼峰命名
js是一种弱类型或动态语言，不用提前申明变量类型，程序运行根据等号右边的值会自动确定<br>
数据类型<br>
简单类型：Number,String,Boolean,null,undefined 默认值 0 “” false null undefined<br>
复杂数据类型：object<br>
进制<br>
八进制：数字前面加0表示八进制 010 表示十进制8<br>
十六进制：数字前面加0x表示十六进制，oxa 表示十进制10<br>
number范围 Number.max_value Number.min_value<br>
NAN：代表一个非数值<br>
isNaN(12)：判断是否为数值，不是返回true,是返回false<br>

字符串<br>
js推荐使用单引号<br>
转义字符都是 \开头<br>
\n：换行<br>
\b：空格<br>
1 检测获取字符串长度 length str.length<br>
2 字符串拼接 字符串+任意类型=新的字符串<br>
3 字符串+变量<br>
boolean<br>
true+1=2<br>
false+1=1<br>
4 typeof 值 判断数据类型<br>

数据类型转换<br>
转为字符串：<br>
1 toString()//null unfinded没有toString()方法<br>
2 String() a=String(a) null unfinded也可以<br>
3 和字符串拼接 +<br>
转为数字<br>
Number()<br>
空字符串->0
非数字->NAN

转为数值型<br>
1 parseInt(‘23’)//把字符串转为数字<br>
parseInt(a,10)转为10进制
2 parseFloat(‘23.34’)<br>

把其他类型转为boolean类型<br>
boolean()<br>
代表空，否定的词被转为false，其他被转为true<br>

解释型语言和编译型语言<br>
解释型语言：解释一行执行一行<br>
编译型语言：生成中间文件<br>

前置自增：先加一然后 21<br>
后置自增：先返回原值，在加1 20<br>
单独使用效果一样<br>
var i=10<br>
console.log(++i +10)<br>

比较运算符<br>
=：赋值<br>
==：默认转化数据类型，会把字符串转化为数字<br>
===：全等 类型和值都相同<br>

逻辑运算符<br>
&& 逻辑与 and<br>
|| 逻辑或 or<br>
！逻辑非<br>
逻辑与短路运算<br>
如果表达式1为真，返回表达式2.如果表达式1为假，则返回表达式1<br>
console.log(123&&345) //345<br>
0 ' ' undefined null NAN为假<br>
逻辑或短路运算<br>
如果表达式1为真，返回表达式1.如果表达式1为假，则返回表达式2<br>
console.log(123||345) //123<br>
逻辑中断会影响程序运行结果<br>
console.log(123 || num++) //num++不会执行<br>

运算符优先级<br>
1 小括号（） 2 一元运算符++，-- ！ 3 算术运算符* 4 关系>= 5 相等 == 6 逻辑运算符 && 7 赋值=<br>

流程控制<br>
三种结构：顺序，分支(条件判断)，循环<br>
js中分支<br>
if<br>
switch<br>
var num=12;<br>
switch(表达式num）<br>
{<br>
case value1:<br>
执行语句1；<br>
break;<br>
default:<br>
执行最后的语句；<br>
注意:1必须是全等才能匹配 2如果没有break，则会继续执行下一个case<br>
switch分支多效率比if else if高<br>

三元表达式 //针对变量设置一些列特定值<br>
条件表达式 ？ 表达式1：表达式2<br>

循环<br>
1 for 2 while 3 do while<br>

断点调试<br>
可以帮我们认识程序运行过程<br>
浏览器f12---source--找到需要调试文件--在程序某一行前面设置断点--刷新一次<br>

双重循环<br>
var str=' ';<br>
for(var i=1;i<=10;i++){<br>
for(var j=i;j<=10;j++){<br>
str=str+ '*";<br>
}<br>
str+='\n';<br>
}<br>
console.log(str);<br>
打印99乘法表<br>
var str=' ';<br>
for(var i=1;i<=9;i++)//外层循环控制层数{<br>
for(var j=1;j<=i;i++){//内层循环控制每行的个数<br>
str+=i+'x'+j+'=' i * j +'\t';<br>
}<br>
str+='\n';<br>
}<br>
console.log(str);<br>

continue:立即跳出本次循环，继续下一次循环//计算1-100除了7的倍数的和<br>
break:用户跳出整个循环<br>

js数组：一组数据的集合<br>
创建数组<br>
1 new var arr=new Array();<br>
2 利用数组字面量创建数组 var arr= [];<br>
可以存放不同数据类型的元素<br>
遍历<br>
for(var i=0;i<arr.length;i++)<br>

数组转化为分割字符串<br>

增加数组长度<br>
var arr=[1,2,3]<br>
arr.length=5;<br>
没赋值默认undefined<br>
不能直接给数组名赋值，否则会覆盖之前的内容<br>
undefined——表示变量声明过但并未赋过值。<br>
null——表示一个变量将来可能指向一个对象。<br>
一般用于主动释放指向对象的引用<br>

js函数<br>
封装了一段可被重复调用执行的代码块，通过此代码块可以实现大量代码的重复使用<br>
函数<br>
1 声明函数<br>
function 函数名(){<br>
函数体<br>
}<br>
函数名一般用动词<br>
2 调用函数<br>
函数名()<br>

函数的参数<br>
1 形参<br>
2 实参<br>
function 函数名(形参1，形参2..){<br>
return 返回的结果；<br>
}<br>
函数名(实参1，实参2...)=返回的结果<br>
//形参接受实参的,形参可以看做不用声明的变量<br>

js实参和形参个数不匹配问题
实参个数大于形参，会取到形参的个数<br>
实参个数小于形参个数，数据+undefined（没定义的变量） -->NAN<br>

return 终止函数（renturn之后的代码不会执行了）<br>
return只能返回一个值，最后一个：num1，num2会返回num2/也可以返回一个数组<br>
函数没有return，返回undefined<br>

不确定有多少参数传递的时候，可以使用arguments来获取，js中,arguments就是函数的一个内置对象，存储了传递的所有实参。<br>
使用：在方法中console.log(arguments/arguments.length)<br>

利用函数求任意个数的最大值<br>
function getMax(){<br>
var max=arguments[0];<br>
for(var i=1;i<arguments.length;i++){<br>
if(max<arguments[i])<br>
max=arguments[i]<br>
}<br>
return max;<br>
}<br>

函数可以调用另外一个函数<br>

函数两种命名方式<br>
1 命名函数 function fu(){}<br>
2 表达式函数 var num=function(){}:匿名表达式也可以传参 num(1)<br>

js作用域：局部，全局<br>
es6新增快级作用域{}<br>

js引擎运行js分为两步，预解析和代码执行<br>
预解析：会把js里面var function提升到当前作用域的最前面<br>
代码执行：从上到下执行<br>
变量提升：提升声明，不提升赋值<br>
函数提升：<br>

js创建对象<br>
1 字面量创建对象{} var obj={<br>
name: ‘张三’,<br>
sayHi: function(){},<br>
};<br>
2 new object<br>
var obj=new Object()<br>
3 构造方法<br>
function 构造方法名(){<br>
this.属性=值，<br>
this.方法=function(){}<br>
}<br>
new 构造方法名（）;<br>
不需要return 就可以返回值<br>

函数单独声明，调用 函数名（）<br>
方法在对象中使用 对象.方法名()<br>

new关键字的执行过程<br>
1在内存中创建一个·新的对象<br>
2this就会指向刚创建的空对象<br>
3指向构造函数里面的代码<br>
4返回这个对象<br>

遍历对象<br>
for in 对象<br>
for(var i in obj){<br>
console.log(i);:得到属性名<br>
console.log(obj[i]):得到属性值<br>
}<br>

js对象分为三种，自定义对象，内置对象，浏览器对象<br>
内置对象:js自带的对象<br>
Math,Date,String,Array<br>

webapi 是浏览器提供的一套操作浏览器功能和页面元素的api(BOM和BOM）<br>
api是为程序员提供的一个接口，帮助我们实现某个功能<br>

dom document object model可处理可扩展标记语言html/xml的标准编程接口<br>
通过dom接口可以改变网页的内容，结构和样式<br><br>
dom树<br>
页面中的所以标签都是元素，dom中用element表示<br>
网页中的所以内容都可以看做节点，node<br>

获取网页元素<br>
1 通过id获取<br>
2 通过标签名获取<br>
3 通过h5新增的方法获取<br>

4 特殊元素获取<br>
```html
var timer=document.getElementById('id');//得到一个对象<br>
comsole.dir(timer)//打印返回的对象<br>
```
