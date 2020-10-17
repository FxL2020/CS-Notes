
# ES6

### var、let 及 const 区别？
变量提升：
JavaScript 中，函数及变量的声明都将被提升到函数的最顶部。
JavaScript 中，变量可以在使用后声明，也就是变量可以先使用再声明。
- 全局申明的 var 变量会挂载在 window 上，而 let 和 const 不会
- var 声明变量存在变量提升，let 和 const 不会
- let、const 的作用范围是块级作用域，而 var 的作用范围是函数作用域
- 同一作用域下 let 和 const 不能声明同名变量，而 var 可以
- 同一作用域下在 let 和 const 声明前使用会存在暂时性死区
- const
  - 一旦声明必须赋值,不能使用 null 占位
  - 声明后不能再修改
  - 如果声明的是复合类型数据，可以修改其属性
  
  ### Proxy

Proxy 是 ES6 中新增的功能，它可以用来自定义对象中的操作。 Vue3.0 中将会通过 Proxy 来替换原本的 Object.defineProperty 来实现数据响应式。

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

### Es6 新增箭头函数与普通函数的区别？

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
var fn1 = (a, b) => {
    return a + b
}
(a, b) => {
    return a + b
}
 ```
  
  ### Promise

`Promise` 翻译过来就是承诺的意思，这个承诺会在未来有一个确切的答复，并且该承诺有三种状态，这个承诺一旦从等待状态变成为其他状态就永远不能更改状态了。

- 等待中（pending）
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
### Set
ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。Set本身是一个构造函数，用来生成 Set 数据结构。
```js
const items = new Set([1, 2, 3, 4, 5, 5, 5, 5]);
items.size // 5
```
也提供了一种数组去重方法
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
```



