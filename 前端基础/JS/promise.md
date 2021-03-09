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
  
