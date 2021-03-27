### call
可以指定函数的this，可以执行函数并传参   <br>
参数：第一个参数：this指向的对象，第二个参数及以后是函数的实参   <br>
返回值：就是函数自己的返回值   <br>


```js
    在函数调用的时候，浏览器每次都会传递进两个隐式参数：
    1. 函数的上下文对象this
    2. 封装实参的对象arguments
    Function.prototype.defineCall = function(){
        let context = arguments[0] || window; //context上下文
        context.fn = this;  //context上下文定义一个属性fn
        let args = [...arguments].slice(1);
        let result = context.fn(...args);
        delete context.fn;
        return result;
    }
    let say=function (age) {
        console.log(age)
        console.log(this)
    }
    let obj={
        name: 'liming'
    }
    say.defineCall(obj,2) //obj 2
    say(2) //window 2
```

### apply

改变this指向，唯一区别就是跟call传递参数不同

```js
  Function.prototype.defineApply=function (context,arr) {
        context =context || window
        context.fn=this
        let result;
        if (!arr){
            result=context.fn()
        }else {
            let args=[]
            for(let i=1;i<arguments.length;i++){
                args.push(arguments[i])
            }
            result=context.fn(args.join(','))
        }
        return result
    }
    let obj=['we','er']
    let say=function (age) {
        console.log(age)
        console.log(this)
    }
    say.defineApply(obj,[1,3])
    
  ```
  
  ### bind
 
  可以指定函数的this，不可以执行函数，但可以传参  <br>
  返回值：返回一个新的指定了this的函数，也可以叫绑定函数  <br>
    
  ```js
  Function.prototype.bind=function (context) {
        let self = this     // 保存函数的引用
        return function () { // 返回一个新的函数
            console.log(arguments)
           // return self.apply(context, arguments);
            return self.call(context, arguments);
        }
    }
    let obj={
        name: 'liming'
    }
    let func =function () {
        console.log(this.name)
    }.bind(obj)

    func('li',20)
    
    ```
