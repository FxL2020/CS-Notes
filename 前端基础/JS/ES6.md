更详细的点击ECMAScript 6 入门 https://es6.ruanyifeng.com/#docs/reflect
# ES6

### ES6和JS关系
ECMAScript 6规范<br>
js对这个规范的实现<br>
TS是js的超集<br>
babel转码器：把ES6转为浏览器识别的ES5

### var、let 及 const 区别？
定义变量
变量提升：
JavaScript 中，函数及变量的声明都将被提升到函数的最顶部。
- 全局申明的 var 变量会挂载在 window 上，而 let 和 const 不会
- <b>var 声明变量存在变量提升，let 和 const 不会</b>
- let、const 的作用范围是块级作用域，而 var 的作用范围是函数作用域
- <b>同一作用域下 let 和 const 不能声明同名变量，而 var 可以</b>
- 同一作用域下在 let 和 const 声明前使用会存在暂时性死区
- const
  - 一旦声明必须赋值,不能使用 null 占位
  - 声明后不能再修改
  - 如果声明的是复合类型数据，可以修改其属性
  
 ### 作用域
 全局作用域   局部作用域
 ES6新增块级作用域
 
 ### Es6 新增箭头函数与普通函数的区别？
语法糖 简化了函数的定义<br>
- 普通 function 的声明在变量提升中是最高的，箭头函数没有函数提升
- 箭头函数没有属于自己的`this`，`arguments`
- 箭头函数不能作为构造函数，不能被 new，没有 property
- 不可以使用 yield 命令，因此箭头函数不能用作 Generator 函数
- 不可以使用 new 命令，因为：
  - 没有自己的 this，无法调用 call，apply
  - 没有 prototype 属性 ，而 new 命令在执行时需要将构造函数的 prototype 赋值给新的对象的 `__proto__`

  ES6箭头函数语法定义函数，将原函数的“function”关键字和函数名都删掉，并使用“=>”连接参数列表和函数体。
  当函数参数只有一个，括号可以省略；但是没有参数时，括号不可以省略。 
```js
var a=arr.filter(item=>item>5)
var a=arr.filter(function(item){
return item>5;
})
let f=(n1,n2)=>({a:n1,b:n2})
var fn1 = (a, b) => {
    return a + b
}
(a, b) => {
    return a + b
}
 ```
 
 ### Set
ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。Set本身是一个构造函数，用来生成 Set 数据结构。
```js
const items = new Set([1, 2, 3, 4, 5, 5, 5, 5]);
items.size // 5
items.add(1).add(2).add(2) //链式添加
```
也提供了一种数组去重方法<br>
...扩展运算符 转为用逗号分隔的参数序列
```js
// 去除数组的重复成员
[...new Set(array)]
```
字符串去重
```js
[...new Set('ababbc')].join('')
// "abc"
```
### Map
ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。如果你需要“键值对”的数据结构，Map 比 Object 更合适。
```js
const m = new Map();
const o = {p: 'Hello World'};

m.set(o, 'content')
m.get(o) // "content"

m.has(o) // true
m.delete(o) // true
m.has(o) // false

ES6提供了for of遍历map
for(let [k,value] of m2)
{
}
```
 ### Promise
是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。

所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

`Promise` 翻译过来就是承诺的意思，这个承诺会在未来有一个确切的答复，并且该承诺有三种状态，这个承诺一旦从等待状态变成为其他状态就永远不能更改状态了。

- 进行中（pending）
- 完成了（resolved）
- 拒绝了（rejected）

当我们在构造 Promise 的时候，构造函数内部的代码是立即执行的。

```js
new Promise((resolve, reject) => {
  console.log('new Promise');
  resolve('success');
});
console.log('finifsh');

// 先打印new Promise， 再打印 finifsh
```
Promise实例生成以后，可以用then方法分别指定resolved状态和rejected状态的回调函数。第二个函数是可选的，不一定要提供
```js
 promise.then.((function(value){},function (error) {
    }));
```

Promise 实现了链式调用，也就是说每次调用 then 之后返回的都是一个 Promise，并且是一个全新的 Promise，原因也是因为状态不可变。如果你在 then 中 使用了 return，那么 return 的值会被 Promise.resolve() 包装。

```js
Promise.resolve(1)
  .then((res) => {
    console.log(res); // => 1
    return 2; // 包装成 Promise.resolve(2)
  })
  .then((res) => {
    console.log(res); // => 2
  });
```

当然了，Promise 也很好地解决了回调地狱的问题

```js
ajax(url)
  .then((res) => {
    console.log(res);
    return ajax(url1);
  })
  .then((res) => {
    console.log(res);
    return ajax(url2);
  })
  .then((res) => console.log(res));
```

其实它也是存在一些缺点的，比如无法取消 Promise，错误需要通过回调函数捕获。

  ### Proxy
  
Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。Proxy 这个词的原意是代理 代理器

Proxy 是 ES6 中新增的功能，它可以用来自定义对象中的操作，操作对象而提供的API。 Vue3.0 中将会通过 Proxy 来替换原本的 Object.defineProperty 来实现数据响应式。

```js
let p = new Proxy(target, handler);
```

`target` 代表需要添加代理的对象，`handler` 用来自定义对象中的操作，比如可以用来自定义 set 或者 get 函数。

```js
let onWatch = (obj, setBind, getLogger) => {
  let handler = {
    set(target, property, value, receiver) {
      setBind(value, property);
      return Reflect.set(target, property, value);
    },
    get(target, property, receiver) {
      getLogger(target, property);
      return Reflect.get(target, property, receiver);
    },
  };
  return new Proxy(obj, handler);
};

let obj = { a: 1 };
let p = onWatch(
  obj,
  (v, property) => {
    console.log(`监听到属性${property}改变为${v}`);
  },
  (target, property) => {
    console.log(`'${property}' = ${target[property]}`);
  }
);
p.a = 2; // 控制台输出：监听到属性a改变
p.a; // 'a' = 2
```
自定义 set 和 get 函数的方式，在原本的逻辑中插入了我们的函数逻辑，实现了在对对象任何属性进行读写时发出通知。

当然这是简单版的响应式实现，如果需要实现一个 Vue 中的响应式，需要我们在 get 中收集依赖，在 set 派发更新，之所以 Vue3.0 要使用 Proxy 替换原本的 API 原因在于 Proxy 无需一层层递归为每个属性添加代理，一次即可完成以上操作，性能上更好，并且原本的实现有一些数据更新不能监听到，但是 Proxy 可以完美监听到任何方式的数据改变，唯一缺陷可能就是浏览器的兼容性不好了。

Proxy 支持的拦截操作一览，一共 13 种。

- get(target, propKey, receiver)
  - 拦截对象属性的读取，比如 proxy.foo 和 proxy['foo']。
- set(target, propKey, value, receiver)
  - 拦截对象属性的设置，比如 proxy.foo = v 或 proxy['foo'] = v，返回一个布尔值。
- has(target, propKey)
  - 拦截 propKey in proxy 的操作，返回一个布尔值。
- deleteProperty(target, propKey)
  - 拦截 delete proxy[propKey]的操作，返回一个布尔值。
- ownKeys(target)
  - 拦截 Object.getOwnPropertyNames(proxy)、Object.getOwnPropertySymbols(proxy)、Object.keys(proxy)、for...in 循环，返回一个数组。该方法返回目标对象所有自身的属性的属性名，而 Object.keys()的返回结果仅包括目标对象自身的可遍历属性。
- getOwnPropertyDescriptor(target, propKey)
  - 拦截 Object.getOwnPropertyDescriptor(proxy, propKey)，返回属性的描述对象。
- defineProperty(target, propKey, propDesc)
  - 拦截 Object.defineProperty(proxy, propKey, propDesc）、Object.defineProperties(proxy, propDescs)，返回一个布尔值。
- preventExtensions(target)
  - 拦截 Object.preventExtensions(proxy)，返回一个布尔值。
- getPrototypeOf(target)
  - 拦截 Object.getPrototypeOf(proxy)，返回一个对象。
- isExtensible(target)
  - 拦截 Object.isExtensible(proxy)，返回一个布尔值。
- setPrototypeOf(target, proto)
  - 拦截 Object.setPrototypeOf(proxy, proto)，返回一个布尔值。如果目标对象是函数，那么还有两种额外操作可以拦截。
- apply(target, object, args)
  - 拦截 Proxy 实例作为函数调用的操作，比如 proxy(...args)、proxy.call(object, ...args)、proxy.apply(...)。
- construct(target, args)
  - 拦截 Proxy 实例作为构造函数调用的操作，比如 new proxy(...args)。


### Reflect
#### 什么是Reflect
ES6 为了操作对象而提供的新 API
#### 为什么要设计Reflect
1.将Object对象的属于语言内部的方法放到Reflect对象上，即从Reflect对象上拿Object对象内部方法。<br>
2. 修改某些Object方法的返回结果，让其变得更合理，将用老Object方法 报错的情况，改为返回false <br>
老写法
```js
try {
  Object.defineProperty(target, property, attributes);
  // success
} catch (e) {
  // failure
}
```
新写法
```js
if (Reflect.defineProperty(target, property, attributes)) {
  // success
} else {
  // failure
}
```
3.让Object操作变成函数行为
老写法（命令式写法）
```js
'assign' in Object // true
```
新写法
```js
Reflect.has(Object, 'assign') // true
```
4.Reflect对象的方法与Proxy对象的方法一一对应，只要是Proxy对象的方法，就能在Reflect对象上找到对应的方法。这就让Proxy对象可以方便地调用对应的Reflect方法，完成默认行为，作为修改行为的基础。也就是说，不管Proxy怎么修改默认行为，你总可以在Reflect上获取默认行为。
```js
Proxy(target, {
  set: function(target, name, value, receiver) {
    var success = Reflect.set(target, name, value, receiver);
    if (success) {
      console.log('property ' + name + ' on ' + target + ' set to ' + value);
    }
    return success;
  }
});
```
Proxy方法拦截target对象的属性赋值行为。它采用Reflect.set方法将值赋值给对象的属性，确保完成原有的行为，然后再部署额外的功能。
#### Reflect静态方法
和Proxy的API一致<br>
- Reflect.get(target, name, receiver)
Reflect.get方法查找并返回target对象的name属性，如果没有该属性，则返回undefined。如果name属性部署了读取函数（getter），则读取函数的this绑定receiver。如果第一个参数不是对象，Reflect.get方法会报错。
- Reflect.set(target, name, value, receiver) 
Reflect.set方法设置target对象的name属性等于value。
- Reflect.has(obj, name)
Reflect.has方法对应name in obj里面的in运算符。如果Reflect.has()方法的第一个参数不是对象，会报错。
- Reflect.defineProperty(target, propertyKey, attributes)
Reflect.defineProperty方法基本等同于Object.defineProperty，用来为对象定义属性。未来，后者会被逐渐废除，请从现在开始就使用Reflect.defineProperty代替它。<br>
这个方法可以与Proxy.defineProperty配合使用。<br>
```js
const p = new Proxy({}, {
  defineProperty(target, prop, descriptor) {
    console.log(descriptor);
    return Reflect.defineProperty(target, prop, descriptor);
  }
});
p.foo = 'bar';
// {value: "bar", writable: true, enumerable: true, configurable: true}
p.foo // "
```
Proxy.defineProperty对属性赋值设置了拦截，然后使用Reflect.defineProperty完成了赋值。

### Symbol
保证每个属性的名字都是独一无二的，这样就从根本上防止属性名的冲突。这就是 ES6 引入Symbol的原因。<br>
ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，前六种是：undefined、null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。<br>
Symbol 值通过Symbol函数生成。这就是说，对象的属性名现在可以有两种类型，一种是原来就有的字符串，另一种就是新增的 Symbol 类型。凡是属性名属于 Symbol 类型，就都是独一无二的，可以保证不会与其他属性名产生冲突。<br>
```js
let s = Symbol();
typeof s
// "symbol"
```


### map
https://www.jianshu.com/p/53032fc0909a
```js
定义在JavaScript的Array中，它返回一个新的数组，数组中的元素为原始数组调用函数处理后的值。
array.map(function(currentValue, index, arr), thisIndex)
function(currentValue, index, arr)：必须。为一个函数，数组中的每个元素都会执行这个函数。其中函数参数：
currentValue：必须。当前元素的的值。
index：可选。当前元素的索引。
arr：可选。当前元素属于的数组对象。
遍历对象数组
data.departments.map(v=>{
                  return {
                      key: v.id,
                      value: v.departmentName
                  }
          });
```

### filter

filter 的作用也是生成一个新数组，在遍历数组的时候将返回值为 true 的元素放入新数组，我们可以利用这个函数删除一些不需要的元素

filter 的回调函数接受三个参数，分别是当前索引元素，索引，原数组


  
 

### 变量的解构赋值
#### 数组的解构赋值
ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构
```js
let a = 1;
let b = 2;
let c = 3;
```
ES6
```js
 let [a,b,c,d]=[1,2,3,4];
 //本质上模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值
```
解构不成功，变量的值就等于undefined
 Set 结构，也可以使用数组的解构赋值。
```js 
 let [x, y, z] = new Set(['a', 'b', 'c']);
x // "a"
```
#### 对象的解构赋值
```js
let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
```
数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。
#### 对象的解构赋值
```js
const [a, b, c, d, e] = 'hello';
a // "h"
b // "e"
c // "l"
d // "l"
e // "o"
```
### async 和 await

一个函数如果加上 async ，那么该函数就会返回一个 Promise

```js
async function test() {
  return '1';
}
console.log(test());
// -> Promise {<resolved>: "1"}
```

async 就是将函数返回值使用 Promise.resolve() 包裹了下，和 then 中处理返回值一样，并且 await 只能配套 async 使用。

```js
async function test() {
  let value = await sleep();
}
```

async 和 await 可以说是异步终极解决方案了，相比直接使用 Promise 来说，优势在于处理 then 的调用链，能够更清晰准确的写出代码，毕竟写一大堆 then 也很恶心，并且也能优雅地解决回调地狱问题。

当然也存在一些缺点，因为 **await 将异步代码改造成了同步代码**，如果多个异步代码没有依赖性却使用了 await 会导致性能上的降低。

```js
async function test() {
  // 以下代码没有依赖性的话，完全可以使用 Promise.all 的方式
  // 如果有依赖性的话，其实就是解决回调地狱的例子了
  await fetch(url);
  await fetch(url1);
  await fetch(url2);
}
```

看一个使用 await 的例子：

```js
let a = 0;
let b = async () => {
  a = a + (await 10);
  console.log('2', a);
};
b();
a++;
console.log('1', a);

//先输出  ‘1’, 1
//在输出  ‘2’, 10
```

- 首先函数 b 先执行，在执行到 await 10 之前变量 a 还是 0，因为 await 内部实现了 generator ，generator 会保留堆栈中东西，所以这时候 a = 0 被保存了下来
- 因为 await 是异步操作，后来的表达式不返回 Promise 的话，就会包装成 Promise.reslove(返回值)，然后会去执行函数外的同步代码
- 同步代码 a++ 与打印 a 执行完毕后开始执行异步代码，将保存下来的值拿出来使用，这时候 a = 0 + 10

上述解释中提到了 await 内部实现了 generator，其实 **await 就是 generator 加上 Promise 的语法糖，且内部实现了自动执行 generator**。



