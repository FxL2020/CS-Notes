### this
this 是和执行上下文绑定的，也就是说每个执行上下文中都有一个 this。

执行上下文主要分为三种——全局执行上下文、函数执行上下文和 eval 执行上下文，所以对应的 this 也只有这三种——全局执行上下文中的 this、函数中的 this 和 eval 中的 this。

全局执行上下文中的this
全局执行上下文中的 this 是指向 window 对象的。这也是 this 和作用域链的唯一交点，作用域链的最底端包含了 window 对象，全局执行上下文中的 this 也是指向 window 对象

函数执行上下文中的
 默认情况下调用一个函数，其执行上下文中的 this 也是指向 window 对象的。<br>
三种方式来设置函数执行上下文中的 this 值<br>
1. 通过函数的 call,bind,apply方法设置<br>
2. 通过对象调用方法设置<br>
使用对象来调用其内部的一个方法，该方法的 this 是指向对象本身的。<br>
3. 通过构造函数中设置<br>
```js
function CreateObj(){
  this.name = " 极客时间 "
}
var myObj = new CreateObj()
```

当执行 new CreateObj() 的时候，JavaScript 引擎做了如下四件事：

首先创建了一个空对象 tempObj；<br>
接着调用 CreateObj.call 方法，并将 tempObj 作为 call 方法的参数，这样当 CreateObj 的执行上下文创建时，它的 this 就指向了 tempObj 对象；<br>
然后执行 CreateObj 函数，此时的 CreateObj 函数执行上下文中的 this 指向了 tempObj 对象；<br>
最后返回 tempObj 对象。<br>
```js
var tempObj = {}
CreateObj.call(tempObj)
return tempObj
```

我们就通过 new 关键字构建好了一个新对象，并且构造函数中的 this 其实就是新对象本身

this 的设计缺陷以及应对方案
#### 1. 嵌套函数中的 this 不会从外层函数中继承
```js
 var myObj = {
        name : "123 ",
        showThis: function(){
            console.log(this)  //myObj
            function bar(){console.log(this)}   //window
            bar()
        }
    }
    myObj.showThis()
```
1.showThis 函数中声明一个变量 self 用来保存 this，然后在 bar 函数中使用 self
```js
var myObj = {
  name : " 极客时间 ", 
  showThis: function(){
    console.log(this)
    var self = this
    function bar(){
      self.name = " 极客邦 "
    }
    bar()
  }
}
myObj.showThis()
console.log(myObj.name)
console.log(window.name)
```
2.使用箭头函数
这是因为 ES6 中的箭头函数并不会创建其自身的执行上下文，所以箭头函数中的 this 取决于它的外部函数。
```js
var myObj = {
  name : " 极客时间 ", 
  showThis: function(){
    console.log(this)
    var bar = ()=>{
      this.name = " 极客邦 "
      console.log(this)
    }
    bar()
  }
}
myObj.showThis()
console.log(myObj.name)
console.log(window.name)
```
第一种是把 this 保存为一个 self 变量，再利用变量的作用域机制传递给嵌套函数。<br>
第二种是继续使用 this，但是要把嵌套函数改为箭头函数，因为箭头函数没有自己的执行上下文，所以它会继承调用函数中的 this<br>

#### 2. 普通函数中的 this 默认指向全局对象 window
因为在实际工作中，我们并不希望函数执行上下文中的 this 默认指向全局对象，因为这样会打破数据的边界，造成一些误操作。<br>
如果要让函数执行上下文中的 this 指向某个对象，最好的方式是通过 call 方法来显示调用。<br>
这个问题可以通过设置 JavaScript 的“严格模式”来解决。在严格模式下，默认执行一个函数，其函数的执行上下文中的 this 值是 undefined<br>



