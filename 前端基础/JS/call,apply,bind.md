
### call
可以指定函数的this，可以执行函数并传参   <br>
参数：第一个参数：this指向的对象，第二个参数及以后是函数的实参   <br>
返回值：就是函数自己的返回值   <br>



    在函数调用的时候，浏览器每次都会传递进两个隐式参数：
    1. 函数的上下文对象this
    2. 封装实参的对象arguments
### 实现call
```js
   Function.prototype.myCall = function(){
        let context = arguments[0] || window; //context上下文
        context.fn = this;  //context上下文定义一个属性fn
        let args = [...arguments].slice(1);
        let result = context.fn(...args);
        delete context.fn; //删除添加的属性
        return result;
    }
    function show() {
        console.log(...arguments);
        console.log(this.name);
    }
    show.myCall({name: 'liming'},'a','b','c')
```

### apply

改变this指向，唯一区别就是跟call传递参数不同，传参是一个数组

```js
    Function.prototype.myApply = function () {
        let context = arguments[0] || window;
        context.fn = this;
        let result;
        //判断是否有第二个参数
        if(arguments[1]){
            result = context.fn(...arguments[1]);
        }else{
            result = context.fn();
        }
        delete context.fn;
        return result;
    }

    function show() {
        console.log(...arguments);
        console.log(this.name);
    }
    show.myApply({name: 'liming'},['a','b','c'])

  ```
  
  ### bind
 
  可以指定函数的this，不可以执行函数，但可以传参  <br>
  返回值：返回一个新的指定了this的函数，也可以叫绑定函数  <br>
    
  ```js
  Function.prototype.myBind=function (context,...args1) {
        return (...args2)=>{
            let fn=Symbol(1)
            context[fn]=this
            context[fn](...args1.concat(args2))
            delete context[fn]
        }

    }
   function show() {
       console.log(...arguments);
       console.log(this.name);
   }
   let bind=show.myBind({name: 'liming'},'a','b')
    bind('c')
    
 ```

优化：
由于每一个 Symbol 的值都是不相等的，所以 Symbol 作为对象的属性名，可以保证属性不重名。
Symbol 作为对象属性名时不能用.运算符，要用方括号。
不会删除已有的属性fn

//实现call
  ```js
  Function.prototype.myCall = function(){
        let context = arguments[0] || window; //context上下文
        let fn=Symbol(1)
        context[fn] = this;  //context上下文定义一个属性fn
        let args = [...arguments].slice(1);
        let result = context[fn](...args);
        delete context[fn];
        return result;
    }
    function show() {
        console.log(...arguments);
        console.log(this.name);
    }
    show.myCall({name: 'liming'},'a','b','c')

  ```

 // 实现apply
  ```js
    Function.prototype.myApply = function () {
        let context = arguments[0] || window;
        let fn=Symbol(1)
        context[fn] = this;
        let result;
        //判断是否有第二个参数
        if(arguments[1]){
            result = context[fn](...arguments[1]);
        }else{
            result = context[fn]();
        }
        delete context[fn];
        return result;
    }

    function show() {
        console.log(...arguments);
        console.log(this.name);
    }
    show.myApply({name: 'liming'},['a','b','c'])
  ```
