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
```
