
### promise
Promise 是异步编程的一种解决方案  <br>
promise 是⼀个有then⽅法的对象或者是函数

Promise应该有三种状态
- pending(初始状态，可改变)
- fulfilled(最终态, 不可变)
- rejected(最终态, 不可变)

状态流转
pending resolve(value) fulfilled<br>
pending reject(reason) rejected

Promise应该提供⼀个then⽅法, ⽤来访问最终的结果, ⽆论是value还是reason<br>
promise.then(onFulfilled, onRejected)

then的返回值也是一个promise

Promise构造函数接受一个函数作为参数,该函数的两个参数分别是resolve和reject。它们是两个函数

resolve,reject函数的作用是，将Promise对象的状态从“未完成”变为“成功/失败”（即从 pending 变为 resolved/rejected）<br>
在(异步操作成功时调用，并将异步操作的结果)/(在异步操作失败时调用，并将异步操作报出的错误)，作为参数传递出去

```js
 let promise =new Promise((resolve,reject)=>{
        setTimeout(()=>{
            resolve("success")
        },2000)
    })
 promise.then(value => {
        console.log(value)
    },err=>{
        console.log(err)
    })
    //success
```


Promise 新建后就会立即执行。
Promise实例的状态变为resolved，就会触发then方法绑定的回调函数。

注意，调用resolve或reject并不会终结 Promise 的参数函数的执行。

这是因为立即 resolved 的 Promise 是在本轮事件循环的末尾执行，总是晚于本轮循环的同步任务。

一般来说，调用resolve或reject以后，Promise 的使命就完成了，后继操作应该放到then方法里面，而不应该直接写在resolve或reject的后面。
所以，最好在它们前面加上return语句，这样就不会有意外。

```js
let promise =new Promise((resolve,reject)=>{
      console.log("123")
      return resolve("resolve")
      console.log("345")
  })
    promise.then((value)=>{
        console.log(value)
    })
   console.log("log")
    //123
    //log
    //resolve
```

#### then
then方法返回的是一个新的Promise实例（注意，不是原来那个Promise实例）。因此可以采用链式写法，即then方法后面再调用另一个then方法。

第一个回调函数完成以后，会将返回结果作为参数，
传入第二个回调函数如果是Promise对象（即有异步操作），这时后一个回调函数，就会等待该Promise对象的状态发生变化，才会被调用。
```js
 let promise =new Promise((resolve,reject)=>{
        setTimeout(()=>{
            resolve("success")
        },2000)
    }).then(value => {
        return value+"123"
    },err=>{

    }).then(value => {
        console.log(value)
    })
//success123
```




















### promise.all

 Promise.all可以将多个Promise实例包装成一个新的Promise实例。同时，成功和失败的返回值是不同的，  <br>
 成功的时候返回的是一个结果数组，而失败的时候则返回最先被reject失败状态的值。  <br>
 实现Promise.all 以及 race  <br>
   
 ```js
   let promiseAll=function (arr) {
        return new Promise(((resolve, reject) => {
            if (arr.length===0){
                return resolve([]);
            }else{
                let res =[]
                let count =0
                for (let i=0;i<arr.length;i++){
                    //arr数组中非promise对象 直接存
                    if (!(arr[i] instanceof Promise)){
                        res[i]=arr[i]
                        if (++count===arr.length){
                            return resolve(res)
                        }
                    }else {
                        // arr数组中promise对象把返回信息存入
                        arr[i].then(data=>{
                            res[i]=data
                            if (++count===arr.length)
                                return resolve(res)
                            },err=>{
                            reject(err)
                        })
                    }

                }
            }

        }))
    }
    // promise.race();这么简单得益于promise的状态只能改变一次，即resolve和reject都只被能执行一次
   let myRace = function (arr) {
       return new Promise((resolve, reject) => {
           for (let i = 0; i < arr.length; i++) {
               // 同时也能处理arr数组中非Promise对象
               if (!(arr[i] instanceof Promise)) {
                   Promise.resolve(arr[i]).then(resolve, reject)
               } else {
                   arr[i].then(resolve, reject)
               }
           }
       })
   }

    /*let p1 = new Promise(resolve => resolve('li'))
    let p2 = new Promise(resolve => resolve('wo'))
    let p3 = Promise.reject('p3 error')*/
   // 测试用例
   let p1 = new Promise((resolve, reject) => {
       setTimeout(() => {
           resolve(11)
       }, 2000);
   });
   let p2 = new Promise((resolve, reject) => {
       reject('asfs')

   });
   let p3 = new Promise((resolve) => {
       setTimeout(() => {
           resolve(33);
       }, 4);
   });

   myRace([p1,p3,p2]).then(result=>{
        console.log(result)
    }).catch(err=>{
        console.log(err)
    })
```
  
