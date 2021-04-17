### 模块化

### 模块化概念
将一个复杂的程序依据一定的规则(规范)封装成几个块(文件), 并进行组合在一起     <br>
块的内部数据与实现是私有的, 只是向外部暴露一些接口(方法)与外部其它模块通信

本质上就是一种提供对外通信接口，进行代码切分/组合的管理方式

### 模块化的好处
避免命名冲突(减少命名空间污染)     <br>
更好的分离, 按需加载     <br>
更高复用性     <br>
高可维护性     <br>



### 模块化机制要解决的问题

命名污染，全局污染，变量冲突等基础问题     <br>
内聚且私有，变量不能被外界污染到     <br>
怎么引入（依赖）其它模块，怎样暴露出接口给其它模块     <br>
最烦人的是依赖顺序问题，还记得以前的 Jquery 问题嘛     <br>
上述第三点可能导致的循环引用问题，等边界情况     

```js
```

#### 模块化规范

##### 重点--模块化AMD/CMD/CommonJS之间的区别
CommonJs: 运行时同步加载    <br>
AMD: 异步加载，预先加载    <br>
CMD: 异步加载，延迟加载(按需加载)

#### AMD和RequireJS

/** AMD **/
```ts
// 定义一个模块moduleA，它有dep1和dep2两个依赖，最终模块返回一个包含dep1和dep2的对象
define('moduleA', ['dep1', 'dep2'], (dep1, dep2) => {
  console.log('moduleA加载')
  return {  //暴露模块
    dep1
  }
})
// 加载并使用moduleA
require('moduleA', (moduleA) => {
  console.log(moduleA.dep1)
})
```
AMD会在初始化的时候就定义好他需要的规范dep1与dep2，并且进行依赖加载。它的执行顺序是：

dep1和dep2加载    <br>
moduleA加载    <br>
console.log(moduleA.dep1)    <br>

但是AMD这种方式会有一个弊端：虽然当模块声明了两个依赖（dep1和dep2），但是只使用了其中一个（dep1）时，另一个模块dep2也会加载。于是，一种按需加载的方式出现了，它就是CMD

```ts
/** CMD **/

// 定义一个模块moduleA，它显示依赖了dep1
define('moduleA', function (require, exports, module) {
  const dep1 = require('dep1')
  console.log('moduleA加载')
  exports.dep1 = dep1
})
// 加载并使用moduleA
seajs.use('moduleA')

```
通过这种方式我们即可完成模块的按需加载

#### CommonJs
node.js采用了此规范。一个文件便是一个模块。使用全局方法require（）加载某个模块，<br>
示例如下(在b模块中引入模块a)：
```ts
 //a.js
    var a=6;
    var mul =function (a) {
        return a*a
    }
    module.export.a=a;
    module.export.mul =mul;
```
```ts
  //b.js
   var horzon=require("./a.js")
   console.log(horzon.a)
   console.log(horzon.mul)
```
之前在对比三者的区别时有提到过，CommonJS是同步加载的，所以需要加载完成后才能执行后续操作，    <br>
所以比较适合服务器端。对于浏览器端而言，如果同步加载，    <br>
网络太差的情况下会产生页面“假死”现象。因此，只能选用异步加载。


导入&导出

CJS规范很简单：以文件作为单个模块，通过设置require与module两个私有属性分别定义模块的引入和导出。就像是这样

// studentA.js
const moduleA = require('moduleA') // 引入

module.exports = {
  name: '小A'
}
我们这里就通过CJS定义了一个studentA模块。当然你也可以这样导出

exports.name = '小A'
但是这里有个坑点，因为本质上exports是module.expots的引用。所以一旦这样写就会有问题

// 本质上为 exports = module.exports = {}，所以下面这样写就直接变成了 exports = { ... }，也就导出失效了
exports = {
  name: '小A'
}
缓存性

同时CJS会把引入的包结果进行一个本地缓存，直接操作并读取这个对象的话很有可能并不符合预期。下面我们举个例子来进行说明

// a.js
var name = '小A'
exports.name = name
exports.getName = function() {
    return name
}

// b.js
var a = require('./a.js')
console.log(a.name) // '小A'
a.name = '小C'
var b = require('./a.js')
console.log(b.name) // '小C'
console.log(b.getName()) // '小A'
可以看到，我们直接修改a.name = '小C'之后，重新读取的b.name也进行了变更，但实际上我们可以看到b.getName()返回的模块本身name并没有变化，所以这点也是需要注意的。

值拷贝

CJS还有一个很重要的特性就是：CJS导出的内容是进行值拷贝的，这也就意味着我们的CJS在下面这种场景会出现不符合预期的结果

// a.js
var age = 18
exports.name = name
exports.age = age
exports.setAge = function(a){
    age = a
}
// b.js
var a = require('a.js')
console.log(a.age) // 18
a.setAge(19)
console.log(a.age) // 18
为了避免这种情况，我们可以导出一个对象

var test = {
    age: 18
}
exports.test = test
exports.getTestAge = function() {
    return test.age
}
// b.js
var a = require('./a.js')
console.log(a.test) // '18'
a.test.age = 19
var b = require('./a.js')
console.log(b.test.age) // '19'
console.log(a.getTestAge()) // '19'
运行时加载

CommonJS是运行时进行加载模块的，我们可以从之后的循环引用例子中得出结论

循环引用

结合CommonJS运行时加载和值拷贝的特性，在循环引用时只会返回当前模块的值。即A加载B，B又加载A，则B将加载A的不完整版本。

举一个很简单的例子（例子来源于阮老师的CommonJS规范，还是对执行不结果不理解的话可以看看原文）

// a.js
exports.x = 'a1';
console.log('a.js ', require('./b.js').x);
exports.x = 'a2';

// b.js
exports.x = 'b1';
console.log('b.js ', require('./a.js').x);
exports.x = 'b2';

// main.js
console.log('main.js ', require('./a.js').x);
console.log('main.js ', require('./b.js').x);
node main.js

// b.js a1
// a.js b2
// main.js a2
// main.js b2

#### ES6模块化

ES6 模块的设计思想是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。
CommonJS 和 AMD 模块，都只能在运行时确定这些东西。
比如，CommonJS 模块就是对象，输入时必须查找对象属性。

(1)ES6模块化语法

export命令用于规定模块的对外接口，import命令用于输入其他模块提供的功能。
```ts
 //定义模块math.js
    var num=0;
    var add=function (a,b) {
        return a+b;
    }
    export {num,add}//暴露模块
    //引入模块
    import {num,add} from "./math"     //需要指定加载的变量名或函数名
    console.log(num)
    add(2,3)

```
默认输出
```ts
// export-default.js
export default function () {
      console.log('12')
  }
```
引入默认模块
```ts
import customName from './export-default';  //可以使用变量接收默认模块
customName(); // '12'
```
