
### promise
Promise 是异步编程的一种解决方案
promise 是⼀个有then⽅法的对象或者是函数

Promise应该有三种状态
- pending(初始状态，可改变)
- fulfilled(最终态, 不可变)
- rejected(最终态, 不可变)

状态流转
pending resolve(value) fulfilled
pending reject(reason) rejected

Promise应该提供⼀个then⽅法, ⽤来访问最终的结果, ⽆论是value还是reason
promise.then(onFulfilled, onRejected)

then的返回值也是一个promise

Promise构造函数接受一个函数作为参数,该函数的两个参数分别是resolve和reject。它们是两个函数

resolve,reject函数的作用是，将Promise对象的状态从“未完成”变为“成功/失败”（即从 pending 变为 resolved/rejected），在(异步操作成功时调用，并将异步操作的结果)/(在异步操作失败时调用，并将异步操作报出的错误)，作为参数传递出去

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
```js






















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
  
