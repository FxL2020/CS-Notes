
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

### Es6 中箭头函数与普通函数的区别？

- 普通 function 的声明在变量提升中是最高的，箭头函数没有函数提升
- 箭头函数没有属于自己的`this`，`arguments`
- 箭头函数不能作为构造函数，不能被 new，没有 property
- 不可以使用 yield 命令，因此箭头函数不能用作 Generator 函数
- 不可以使用 new 命令，因为：
  - 没有自己的 this，无法调用 call，apply
  - 没有 prototype 属性 ，而 new 命令在执行时需要将构造函数的 prototype 赋值给新的对象的 `__proto__`
