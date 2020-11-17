
#### 枚举对象中的属性<br>
for(var 变量 in 对象){}<br>
for(var n in 对象)
{
console.log(n)//属性名
console.log(对象[n])//属性值
}<br>

#### this
解析器在调用函数每次都会向函数内部传递一个隐含的参数this,this指向一个对象，函数执行的上下文对象<br>
根据函数的调用方式不同，this会指向不同的对象<br>
1 以函数形式调用，this永远都是window<br>
2 以方法形式调用，this就是调用方法的那个对象<br>

```html
var obj={
name:"",
say:function(){}
}
```

#### toString()
当我们直接再页面中打印一个对象时，页面上输出的对象的toString()方法的返回值
```html
var per=new People()
console.log(per._proto_.proto.hasOwnProperty("toString"))//true,说明这个对象的原型的原型有toString
per.toString=function()
{People[name="+this.name+" ,age="+this.age+"]}
People.prototype.toString=function()
{People[name="+this.name+" ,age="+this.age+"]}//修改per原型的toString，所以对象toString全都改
```
#### 垃圾回收
垃圾过多会导致程序运行速度变慢，所以需要垃圾回收机制处理程序运行过程中产生的垃圾<br>
当一个对象没有任何的变量或一个属性对它进行引用，此时我们永远无法操作该对象此时对象就是垃圾，占用内存空间<br>
js有自动的垃圾回收机制，会自动地将这些垃圾从内存中销毁<br>
我们需要做的就是把不在使用的对象设置为null即可<br>
obj=null<br>

#### 数据类型相关问题
1.undefined 和 null的区别<br>
undefined：代表定义未赋值<br>
null：定义并赋值了，只是值为空<br>
2.什么时候给变量赋值为null尼<br>
初始赋值，表明将要赋值为对象
结束赋值，让对象成为垃圾对象(被垃圾对象回收)
```html

```
#### 函数高级

#### js中数据类型判断typeof、instanceof、Object.prototype.toString.call()、constructor
https://blog.csdn.net/zjy_android_blog/article/details/81023177
- typeof
```html
console.log(typeof 2);               // number
console.log(typeof true);            // boolean
console.log(typeof 'str');           // string
console.log(typeof []);              // object     []数组的数据类型在 typeof 中被解释为 object
console.log(typeof function(){});    // function
console.log(typeof {});              // object
console.log(typeof undefined);       // undefined
console.log(typeof null);            // object
```
数组 和 null 的判断不准确  <br>
- instanceof: 运算符用来测试一个对象在其原型链中是否存在一个构造函数的 prototype 属性。其意思就是判断对象是否是某一数据类型（如Array）的实例
```html
console.log([] instanceof Array);   //true
console.log(2 instanceof Number);    //false
console.log(new Number(2) instanceof Number);    //true
```
不能判断undefined,null  <br>
- constructor
```html
console.log((2).constructor === Number);
console.log((true).constructor === Boolean);
```
如果我创建一个对象，更改它的原型，这种方式也变得不可靠了
```html
function Fn(){};
Fn.prototype=new Array();
var f=new Fn();
console.log(f.constructor===Fn);    // false
console.log(f.constructor===Array); // true
```
- Object.prototype.toString.call()
在JS中，可以通过Object.prototype.toString方法，判断某个对象之属于哪种内置类型。
```html
Object.prototype.toString.call(null); // "[object Null]"
Object.prototype.toString.call(undefined); // "[object Undefined]"
Object.prototype.toString.call(“abc”);// "[object String]"
Object.prototype.toString.call(123);// "[object Number]"
Object.prototype.toString.call(true);// "[object Boolean]"
Object.prototype.toString.call(fn); // "[object Function]"
Object.prototype.toString.call(arr); // "[object Array]"
Object.prototype.toString.call(arr); // "[object Object]"
```
#### 闭包 








