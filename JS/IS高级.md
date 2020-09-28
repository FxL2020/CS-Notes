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
