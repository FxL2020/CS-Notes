
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
#### 使用工厂方式创建对象
批量创建对象
```html
var obj=createObj()
function(name){}
{
name:name,
say:function(){}
}
```
#### 构造函数
调用方式不同，普通函数直接调用，构造函数要使用new关键字调用<br>
构造函数的执行流程<br>
1.立即创建一个新的对象<br>
2.将新建的对象设置为函数中的this，再构造函数中可以使用this来引用新建的对象<br>
3.逐行执行函数中的代码<br>
4.将新建的对象作为返回值返回<br>
```html
var obj=new Object()
function Object(name){}
{
this.name=name
}
```
使用instanceof可以检查一个对象是否是一个类的实例<br>
```html
console.log(对象 instanceof 构造函数)//是返回true,否则返回false
console.log(对象 instanceof People)
//通过一个构造函数创建的对象是一类对象
```
#### 原型对象prototype
我们所创建的每一个函数，解析器就会向函数中添加一个属性,这个属性对应一个对象 原型对象prototype<br>
如果函数作为普通函数调用，prototype没有任何作用，当函数以构造函数形式调用时，它所创建的对象中都有一个隐含的属性，指向该构造函数的原型对象，可以使用_proto_来访问该属性<br>
原型对象相当于一个公共区域，所有同一个类的实例都可以访问这个原型对象，可以将对象中共有的内容，设置在原型对象中<br>
当我们访问某个属性或方法时，他首先再对象中寻找，如果有返回，没有则回去原型对象中去寻找
```html
function MyClass(){}
MyClass.prototype.a=123
MyClass.prototype.say=function(){}
var mc=new MyClass()
var m1=new MyClass()
console.log(mc.a)
console.log(mc.say)
console.log(MyClass.prototype==mc_prototype==m1_prototype)

```
可以使用in来检查对象中是否有某个属性，如果对象中没有但原型有也会返回true
可以使用对象的hasOwnProperty()来检查对象自身中是否有该属性有返回true
原型对象也是对象，它也有原型，原型中没有也会去原型的原型中去寻找，直到Object对象的原型，Object对象的原型没有原型，如果Objedt没有找到则返回undefined
```html
console.log("name" in mc)
console.log(mc.hasOwnProperty("name))
console.log(mc._proto_._proto.hasOwnProperty("name"))
console.log(mc.sex)
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






