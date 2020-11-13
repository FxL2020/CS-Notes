

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
js会忽略多个空格和换行<br>
字面量：不可改变的值，可以直接使用，一般使用变量保存字面量<br>
标识符一般采用驼峰命名
js是一种弱类型或动态语言，不用提前申明变量类型，程序运行根据等号右边的值会自动确定<br>
数据类型<br>
简单类型：Number,String,Boolean,null,undefined 默认值 0 “” false null undefined<br>
复杂数据类型：object,array,Function<br>
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
==：默认转化数据类型<br>
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

for(;;){}//此时会是一个死循环一直执行下去

1.1-100,7的倍数和以及个数
```js
   <script type="text/javascript">
        var sum=0;
        var count=0;
        for (var i=1;i<=100;i++){
            if (i%7==0){
                sum=sum+i;
                count++;
            }
        }
        console.log("个数"+count);
        console.log("总合:"+sum);
    </script>
  ```
2.水仙花数 一个三位数，它的每个位上的数字的三次幂次之和是它本身，请打印出所有的水仙花数
```js
   <script type="text/javascript">
        for (var i=100;i<1000;i++){
            var bai=parseInt(i/100);
            var shi=parseInt((i/10)%10);
            var ge=i%10;
            if (bai*bai*bai+shi*shi*shi+ge*ge*ge == i){
                console.log(i);
            }
        }
    </script>
 ```
 
  3.判断质数，大于1只能被1和本身整除的数
  ```js
  1
    var num=prompt("请输入一个大于1的整数");
      if (num<=1){
          alert('该参数不合法');
      }else {
          var flag= true;
          for (var i=2;i<num;i++){
              if(num%i ==0){
                  flag = false;
              }
          }
          if (flag){
              alert(num+"是质数");
          }else {
              alert("这个不是质数");
          }
  2
  //打印1-100的质数
     for (var i=2;i<=100;i++){
         var flag=true;//没执行依次flag重新置为true
         for (var j=2;j<i;j++){
             if (i%j==0){
                 flag=false;
                 break;
             }
         }
         if (flag){
             console.log(i);
         }
      }
  3 改进：
  
 ```
双重循环<br>
```js
var str=' ';
for(var i=1;i<=10;i++){
for(var j=i;j<=10;j++){
str=str+ '*";
}
str+='\n';
}
console.log(str);

效果：
*****
****
***
**
*
```
打印99乘法表<br>
```js
var str=' ';
for(var i=1;i<=9;i++){
for(var j=1;j<=i;i++){
str+=i+'x'+j+'=' i * j +'\t';
}
str+='\n';
}
console.log(str);
效果：
1x1=1	
2x1=2	2x2=4	
3x1=3	3x2=6	 3x3=9	
4x1=4	4x2=8	 4x3=12	4x4=16	
5x1=5	5x2=10	5x3=15	5x4=20	5x5=25	
6x1=6	6x2=12	6x3=18	6x4=24	6x5=30	6x6=36	
7x1=7	7x2=14	7x3=21	7x4=28	7x5=35	7x6=42	7x7=49	
8x1=8	8x2=16	8x3=24	8x4=32	8x5=40	8x6=48	8x7=56	8x8=64	
9x1=9	9x2=18	9x3=27	9x4=36	9x5=45	9x6=54	9x7=63	9x8=72	9x9=81	
```
continue:立即跳出本次循环，继续下一次循环//计算1-100除了7的倍数的和<br>
break:用户跳出整个循环<br>

#### js数组：一组数据的集合<br>
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
数组长度：对于非连续数组，使用length会获取到数组的最大索引+1<br>

数组的四个方法<br>
1.push():该方法可以向数组的末尾添加一个或多个元素，并返回数组的新的长度
```html
var arr=[1,2,3];
var len=arr.push(2,3,4,5);len=7
console.log(arr)
```
2.pop():该方法可以删除数组最后一个元素，并将被删除的元素作为返回值
3.unshift():该方法可以向数组开头添加一个或多个元素，并返回新的数组长度,其余的元素索引依次调整
```html
var arr=[1,2,3];
var len=arr.unshift("小米","xiaoming");len=5
console.log(arr)
```
4.shift():可以删除数组的第一个元素，并将删除的元素作为返回值返回
```html
var arr=[1,2,3];
var len=arr.shift();
console.log(arr)
```

遍历数组
var arr=[per1,per2,per3];
```html
function get(){
var newArr=[];
for(var i=0;i<arr.length;i++){
var p=arr[i];
if(p.age>=18){
  newArr.push(p);}
}                               
}//把age大于18的对象放入新的数组
```
forEach()//只支持ie8以上的浏览器
forEach()需要一个函数作为参数<br>
又我们创建，不由我们调用的函数，回调函数
浏览器会在回调函数中传递三个参数
```html
arr.forEach(function(vakue,index,obj){
});
第一个参数：当前遍历的元素
第二个参数：当前遍历的元素的索引
第三个元素：当前遍历的数组
```
slice():截取数组元素从开始索引位置到结束索引位置，不会改变原有数组而是封装到一个新数组中返回
```html
var resulr=arr.slice(1,2)//包括开始不包括结束索引，只有一个参数的话后面的都包括
索引可以为负，-1倒数第一个

splice():可以删除数组中的指定元素，影响原数组，并将被删除的元素作为返回值返回
第一个参数：表示开始位置的索引
第二个参数：表示删除的数量
第三个以后表示插入到开始索引（第一个参数）前面的元素
```
数组去重
```html
var arr=[1,2,3,4,4,4,5,3,4,8,9,6,7,5];
for(var i=0;i<arr.length;i++){
for(var j+1;j<arr.length;j++){
if(arr[i]==arr[j]){//如果相等说明出现了重复删除j位置的元素
arr.splice(j,1);//删除j位置的元素后面的元素会自动补位,会漏掉
j--;//重新跟j位置的元素比较
}
}}
```
concat():可以连接两个或多个数组，并返回新的数组，该方法不会对原有数组造成影响
```html
var arr1=[""];
var arr2=["",""];
var result=arr1.concat(arr2,arr3,"","");//多种类型都可以
console.log(result);
```
join():该方法可以把数组转为字符串，不会对原数组造成影响返回字符串
join(“@”)//连接符，默认,连接符


reverse():反转数组<br>
arr.reverse()//直接修改原数组<br>

sort():直接对数组排序，也会影响原数组，默认会按照Unicode编码进行排序<br>
对于纯数字排序也可能出现错误，//11，2，3，5，8
```html
arr.sort();//我们可以自己指定排序规则
sort()添加一个回调函数，来指定排序规则，定义两个形参，浏览器会分别使用数组中的元素作为实参去调用回调函数，返回大于0，则会交换位置，0位置不变，小于0也不会交换位置
//11，2，3，5，8
arr.sort(function(a,b){
return a-b;//升序排序
return b-a;//降序排序
})
```
#### 字符串方法
在底层字符串是以字符数组的形式保存的<br>
split()//可以将一个字符串转化为一个数组，需要一个字符串（split("")为空则每个字符）作为数组<br>
toUpperCase()//将一个字符串转为大写并返回<br>
toLowerCase()//将一个字符串转为小写并返回<br>
```html
var str="hello world"
length:属性//获取字符串长度
charAt:返回字符串指定位置字符
str[i]:返回字符串指定位置字符
result =String.fromCharCode(20025)//根据字节编码获取字节
charCodeAt():获取指定位置字符的字符编码（Unicode编码）
str.charCodeAt(0)
concat():可以连接两个或多个字符串，并返回新的字符串
result=str.concat("","");
indexOf()//检索一个字符串是否含有指定内容
str.indexOf("h")//如果有则返回第一次出现的索引，如果没有找到返回-1
slice():截取字符串从开始索引位置到结束索引位置，不会改变原有字符串而是封装到一个新的字符串中返回
substring()
str="122,234,34,3"
result = str.split(",")
```


call()和apply():这两个方法都是函数对象的方法，需要函数对象来调用，当函数调用call()和apply()，都会调函数执行<br>
fun.call()<br>
都可以将一个对象指定为第一个参数，此时这个对象会成为函数执行时的this<br>
call()可以将实参在对象之后依次传递<br>
apply()可以将实参封装到一个数组里统一传递
```html
fun.call(obj,1,2,3);
fun.apply(obj,[1,2,3]);
```
this的情况：1.以函数形式调用时，this永远都是window
2.以方法的形式调用时，this是调用方法的对象
3.以构造函数形式调用时，this就是新创建的那个对象
4.使用call()和apply()调用时，this就是指定的那个对象

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

在调用函数时，浏览器每次都会都会传递两个隐含的参数<br>
1.函数的上下文对象this<br>
2.封装实参的对象arguments<br>
arguments是一个类数组对象，他也可以通过索引来操作数据，也可以获取长度<br>
即使不定义形参，我们也可以通过arguments来使用实参
arguments[0]:表示第一个实参
arguments[1]:表示第二个实参

不确定有多少参数传递的时候，可以使用arguments来获取，js中,arguments就是函数的一个内置对象，存储了传递的所有实参。<br>
使用：在方法中console.log(arguments/arguments.length)<br>
利用函数求任意个数的最大值<br>
```html
function getMax(){
var max=arguments[0];
for(var i=1;i<arguments.length;i++){
if(max<arguments[i])
max=arguments[i]
}
return max;
}
```
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
1 字面量创建对象{} 
```html
var obj={
name: ‘张三’,
sayHi: function(){},
};
2 new object<br>
var obj=new Object()<br>
```
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

#### js对象分为三种，自定义对象，内置对象，浏览器对象<br>
内置对象:js自带的对象<br>
Math,Date,String,Array<br>

Date对象
```html
var date=new Date();//封装当前时间<br>
Math和其他对象不一样，他不是一个构造函数，她属于一个工具类不用创建对象，它里面封装了数学运算相关的属性和方法<br>
Math.PI:表示圆周率
Math.abs():计算一个数的绝对值
Math.ceil():向上取整
Math.floor():可以对一个数向下取整
Math.round():对一个数进行四舍五入
Math.random():可以用来生成一个0-1之间的随机数
Math.max(10,34,67,34):可以获取多个数最大值
Math.min(10,34,67,34):可以获取多个数最小值
Math.pow(x,y):返回x的y次方
Math.sqrt(x):用于对一个数进行开方运算
```
webapi 是浏览器提供的一套操作浏览器功能和页面元素的api(BOM和BOM）<br>
api是为程序员提供的一个接口，帮助我们实现某个功能<br>

#### 包装类
js中有三个包装类：可以将基本数据类型的数据转化为对象
```html
String()
Number()
Boolean()
var num=new Number(3);
console.log(typeof num)//Object
num.name="12"//向num添加一个属性
```

#### DOM
dom document object model可处理可扩展标记语言html/xml的标准编程接口<br>
通过dom接口可以改变网页(一个html)的内容，结构和样式<br><br>
对象表示：将网页中的每一个部分都转化为一个对象<br>
model:对象之间的关系<br>
节点：将网页中的每一个部分都转化为一个对象<br>
文档节点：网页<br>
元素节点：标签<br>
属性节点：属性名<br>
文本节点：text<br>
文档节点：document 浏览器提供，是window属性，可以在页面中直接使用，文档节点代表整个网页<br>

dom树<br>
页面中的所以标签都是元素，dom中用element表示<br>
网页中的所以内容都可以看做节点，node<br>

获取网页元素<br>
通过document对象调用
1 通过id获取一个元素节点对象<br>
2 通过标签名获取一组<br>
getElementsByTagName()<br>
通过name属性获取一组元素节点对象<br>
getElementsByName()<br>
3 通过h5新增的方法获取<br>
4 特殊元素获取<br>

获取元素节点子节点<br>
通过元素节点调用
getElementsByTagName() //返回当前节点的指定标签名后代节点<br>
childNode <br>
firstChild  <br>
lastChild  <br>

获取父节点和兄弟节点  <br>
通过具体的节点调用  <br>
parentNode  //当前节点的父亲节点  <br>
previousSibling   //当前节点的前一个兄弟节点  <br>
nextSibling       //当前节点的后一个兄弟节点  <br>


```html
<button id="id">按钮<button>
var but=document.getElementById('id');//得到一个对象<br>
修改按钮文字：but.innerHTML="按钮是我"；
console.log(but.innerHTML) //打印标签内容
comsole.dir(timer)//打印返回的对象<br>
innerHTML：获取元素内部html代码，对于自闭标签没有意义
如果需要读取元素节点属性：
直接使用元素.属性名
```
事件：用户和浏览器之间的交互<br>
点击，鼠标移动，关闭窗口<br>
在事件属性中放入js代码
点击onclick=""<br>
鼠标移动：onmousemove<br>
绑定单击事件<br>
```html
but.onclick=function(){}
```
单选框：通过id获取一个元素节点对象<br>
多选框：通过name属性获取一组元素节点对象<br>
```html
//全选
items=getElementsByName()
for(){
items[i].checked=true;
}
```
document中有一个属性body，它保存body的引用
```html
var body=document.body
```
document.documentElement保存着html根标签
```html
var html=document.documentElement;
```
document.all：代表页面中所有元素

##### 文档的加载
浏览器在加载一个网页时，是按照自上而下的顺序加载的，读取到一行就运行一行<br>
将js代码放在页面下面就是为了页面加载完毕后在执行js代码<br>
onload事件：整个页面加载完之后执行<br>
window.onload=function(){所有js代码}  然后js代码可以放在网页上面<br>

#### 事件对象






