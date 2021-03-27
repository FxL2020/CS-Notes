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
