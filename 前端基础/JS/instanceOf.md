### instanceOf

   instanceof 「运算符」用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上。  <br>
    object instanceof constructor   <br>
    object 某个实例对象   <br>
    construtor 某个构造函数   <br>

    原型链的向上找，找到原型的最顶端，也就是Object.prototype   <br>
     proto 一般情况指向的是该对象的构造函数的prototype  <br>
  ```js 
    function instanceOf(a,b) {
        if (typeof a!=='object' ||a===null) {return false}
        let prototypeB=b.prototype
        let protoA=a.__proto__
        let state=false
        while (true){
            if (protoA ===null){
                state= false;
                break;
            }
            if (protoA ===prototypeB){
                state =true;
                break;
            }
            protoA=protoA.__proto__;
        }
        return state

    }

    console.log(instanceOf([],Array))
```
