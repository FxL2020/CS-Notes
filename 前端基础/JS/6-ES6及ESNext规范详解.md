## ES6及ESNext

### ECMAScript规范 

有的人以年份描述，比如ES2015,ES2016
有的人以版本号描述，比如ES6,ES7


总之: 严格来说, ES6是指2015年6月发布的ES2015标准, 但是很多人在谈及ES6的时候, 都会把ES2016 ES2017等标准的内容也带进去. 
所以严谨的说, 在谈论ECMAScript标准的时候, 用年份更好一些

#### ESNext

前面见到了各种ES6 7, ES2015, 怎么又冒出一个ESNext? ESNext是什么?

其实ESNext是一个泛指, 它永远指向下一个版本. 比如当前最新版本是ES2020, 那么ESNext指的就是2021年6月将要发布的标准.

### ES6及以后新增的常用API解析

#### let，const，var

```js
for(var i=0;i<=3;i++){ 
    setTimeout(function() {  
        console.log(i)  
    }, 100);
} 
//4 4 4 4
```
分别会输出什么? 为什么? 如何修改可以使其输出0,1,2,3?

```js
for(var i = 0; i <=3; i++) {
    (function (i) {
        setTimeout(function () {
            console.log(i);
        }, 100);
    })(i);
}
//0 1 2 3
for(let i=0;i<=3;i++){ 
    setTimeout(function() {  
        console.log(i)  
    }, 100);
} 
//0 1 2 3
```

原因: 
var定义的变量是全局的, 所以全局只有一个变量i.<br>
setTimeout是异步, 在下一轮事件循环, 等到执行的时候, 去找i变量的引用。所以函数找到了遍历完后的i, 此时它已经变成了4。

1. 而let引入了块级作用域的概念, 创建setTimeout函数时，变量i在作用域内。对于循环的每个迭代，引用的i是i的不同实例。

2. 还存在变量提升的问题

```js
console.log(i) //undefined
var i = 1;

console.log(letI) //报错
let letI；
let1=0;

const c1;//报错
c1=2
```
3. const
一旦声明必须赋值,不能使用 null 占位<br>
声明后不能再修改<br>
如果声明的是复合类型数据，可以修改其属性<br>

#### 箭头函数

1. 最大的区别：箭头函数里的this是定义的时候决定的, 普通函数里的this是使用的时候决定的。

箭头函数没有自己的this，arguments值，箭头函数中所使用的this都是来自函数作用域链， 箭头函数中引用this实际上是调用的是定义时的上一层作用域的this。

这里强调的是上一层作用域，是因为对象是不能形成独立的作用域的。

```js
const teacher = {
    name: 'er',
    getName: function() {
        return `${this.name}`
    }
}
console.log(teacher.getName());//er

const teacher = {
    name: 'er',
    getName: () => {
        return `${this.name}`
    }
}
console.log(teacher.getName());
//this指向window
```
2. 简写箭头函数

当函数参数只有一个，括号可以省略；但是没有参数时，括号不可以省略。没有return，默认直接return右边的

返回一个对象，需要用一个小括号包着，不然会返回undefined

```js
const arrowFn = (value) => Number(value);

 const fn=()=>{a:1}
 console.log(fn()) //undefined

const f= () => ({}) //返回一个对象

console.log(arrowFn('aaa'))
```

3. 注意, 箭头函数不能被用作构造函数

构造函数会干嘛? 改变this指向到新实例出来的对象. 
箭头函数会干嘛？this指向是定义的时候决定的. 


#### class

```js
class Test {
    _name = '';
    constructor() {
        this.name = 'lubai';
    }

    static getFormatName() {
        return `${this.name} - xixi`;
    }

    get name() {
        return this._name;
    }

    set name(val) {
        console.log('name setter');
        this._name = val;
    }
}

console.log(new Test().name)
console.log(Test.getFormatName())
```

### 模板字符串
反引号
1 传变量拼接字符串
2 换行

```js
const b = 'lubai'

const a  = `${b} - xxxx`;
const c = `我是换行
我换行了！
我又换行了！
`;
```
编写render函数, 实现template render功能.
```js
const year = '2021'; 
const month = '10'; 
const day = '01'; 

let template = '${year}-${month}-${day}';
let context = { year, month, day };

const str = render(template)({year,month,day}); 

console.log(str) // 2021-10-01

function render(template) {
    return function(context) {
        return template.replace(/\$\{(.*?)\}/g, (match, key) => context[key]);
    }
}
```

#### 解构


1. 数组的解构

```js
// 基础类型解构
let [a, b, c] = [1, 2, 3]
console.log(a, b, c) // 1, 2, 3

// 对象数组解构
let [a, b, c] = [{name: '1'}, {name: '2'}, {name: '3'}]
console.log(a, b, c) // {name: '1'}, {name: '2'}, {name: '3'}

// ...解构
let [head, ...tail] = [1, 2, 3, 4]
console.log(head, tail) // 1, [2, 3, 4]

// 嵌套解构
let [a, [b], d] = [1, [2, 3], 4]
console.log(a, b, d) // 1, 2, 4

// 解构不成功为undefined
let [a, b, c] = [1]
console.log(a, b, c) // 1, undefined, undefined

// 解构默认赋值
let [a = 1, b = 2] = [3]
console.log(a, b) // 3, 2
```

2. 对象的结构

```js
// 对象属性解构
let { f1, f2 } = { f1: 'test1', f2: 'test2' }
console.log(f1, f2) // test1, test2

// 可以不按照顺序，这是数组解构和对象解构的区别之一
let { f2, f1 } = { f1: 'test1', f2: 'test2' }
console.log(f1, f2) // test1, test2

// 解构对象重命名
let { f1: rename, f2 } = { f1: 'test1', f2: 'test2' }
console.log(rename, f2) // test1, test2

// 嵌套解构
let { f1: {f11}} = { f1: { f11: 'test11', f12: 'test12' } }
console.log(f11) // test11

// 默认值
let { f1 = 'test1', f2: rename = 'test2' } = { f1: 'current1', f2: 'current2'}
console.log(f1, rename) // current1, current2
```

3. 解构的原理是什么?

针对可迭代对象的Iterator接口，通过遍历器按顺序获取对应的值进行赋值.

对list、tuple、dict、set、str等类型的数据使用for...in...的循环语法从其中依次拿到数据进行使用，我们把这样的过程称为遍历，也叫迭代。
把可以通过for...in...这类语句迭代读取一条数据供我们使用的对象称之为可迭代对象（Iterable）。

3.1 那么 Iterator 是什么?

Iterator是一种接口，为各种不一样的数据解构提供统一的访问机制。任何数据解构只要有Iterator接口，就能通过遍历操作
，依次按顺序处理数据结构内所有成员。

ES6中的for of的语法相当于遍历器，会在遍历数据结构时，自动寻找Iterator接口。

3.2 Iterator有什么用?

* 为各种数据解构提供统一的访问接口
* 使得数据解构能按次序排列处理
* 可以使用ES6最新命令 for of进行遍历

生成一个iterator对象
```js
function generateIterator(array) {
    let nextIndex = 0
    return {
        next: () => nextIndex < array.length ? {
            value: array[nextIndex++],
            done: false
        } : {
            value: undefined,
            done: true
        }
    };
}

const iterator = generateIterator([0, 1, 2])

console.log(iterator.next())
console.log(iterator.next())
console.log(iterator.next()) //done: false value: 2
console.log(iterator.next()) // done: true value: undefined
```

3.3 可迭代对象是什么?

可迭代对象是Iterator接口的实现。这是ECMAScript 2015的补充，它不是内置或语法，而仅仅是协议。任何遵循该协议点对象都能成为可迭代对象。可迭代对象得有两个协议：可迭代协议和迭代器协议。

* 可迭代协议：对象必须实现iterator方法。即对象或其原型链上必须有一个名叫Symbol.iterator的属性。该属性的值为无参函数，函数返回迭代器协议。

* 迭代器协议：定义了标准的方式来产生一个有限或无限序列值。其要求必须实现一个next()方法，该方法返回对象有done(boolean)和value属性。

3.4 我们自己来实现一个可以for of遍历的对象?

通过以上可知，自定义数据结构，只要拥有Iterator接口，并将其部署到自己的Symbol.iterator属性上，就可以成为可迭代对象，能被for of循环遍历。

```js
const obj = {
    count: 0,
    [Symbol.iterator]: () => {
        return {
            next: () => {
                obj.count++;
                if (obj.count <= 10) {
                    return {
                        value: obj.count,
                        done: false
                    }
                } else {
                    return {
                        value: undefined,
                        done: true
                    }
                }
            }
        }
    }
}

for (const item of obj) {
    console.log(item)
}
 
```

#### 遍历

1. for in

遍历数组时，key为数组下标字符串；遍历对象，key为对象字段名。

```js
let obj = {a: 'test1', b: 'test2'}
for (let key in obj) {
    console.log(key, obj[key])
}
```
缺点：
* for in 不仅会遍历当前对象，还包括原型链上的可枚举属性  <br>
* for in 不适合遍历数组（拿到的是索引），主要应用为对象  <br>

2. for of 

可迭代对象（包括 Array，Map，Set，String，TypedArray，arguments对象，
NodeList对象）上创建一个迭代循环,调用自定义迭代钩子，并为每个不同属性的值执行语句。

```js
let arr = [{age: 1}, {age: 5}, {age: 100}, {age: 34}]
for(let {age} of arr) {
    if (age > 10) {
        break // for of 允许中断
    }
    console.log(age)
}
```

优点：
* for of 仅遍历当前对象

#### Object

1. Object.keys

该方法返回一个给定对象的自身可枚举属性组成的数组。

```js
const obj = { a: 1, b: 2 };
const keys = Object.keys(obj); // [a, b]
```

手写实现一个函数模拟Object.keys?

```js
  function getObjectKeys(obj) {
       let array=[];
       for (let key in obj){
           if (obj.hasOwnProperty(key)){
               array.push(key)
           }
       }
       return array
   }

   console.log(getObjectKeys({name:'23',age:23,sex:'nan'}))
```

2. Object.values

该方法返回一个给定对象自身的所有可枚举属性值的数组。

```js
const obj = { a: 1, b: 2 };
const keys = Object.keys(obj); // [1, 2]
```

手写实现一个函数模拟Object.values?

```js
function getObjectValues(obj) {
    const result = [];
    for (const prop in obj) {
        if (obj.hasOwnProperty(prop)) {
            result.push(obj[prop]);
        }
    }

    return result;
}

console.log(getObjectValues({
    a: 1,
    b: 2
}))
```

3. Object.entries

该方法返回一个给定对象自身可枚举属性的键值对数组。

```js
const obj = { a: 1, b: 2 };
const keys = Object.entries(obj); // [ [ 'a', 1 ], [ 'b', 2 ] ]
```

手写实现一个函数模拟Object.entries?

```js
function getObjectEntries(obj) {
    const result = [];
    for (const prop in obj) {
        if (obj.hasOwnProperty(prop)) {
            result.push([prop, obj[prop]]);
        }
    }

    return result;
}

console.log(getObjectEntries({
    a: 1,
    b: 2
}))
```

4. Object.getOwnPropertyNames

该方法返回一个数组，该数组对元素是 obj自身拥有的枚举或不可枚举属性名称字符串。

看一下这段代码会输出什么？

```js
Object.prototype.aa = '1111';

const testData = {
    a: 1,
    b: 2
}

for (const key in testData) {
    console.log(key);
}

console.log(Object.getOwnPropertyNames(testData))
```

5. Object.getOwnPropertyDescriptor

什么是descriptor? 对象对应的属性描述符, 是一个对象. 包含以下属性:
* configurable。 如果为false，则任何尝试删除目标属性或修改属性特性（writable, configurable, enumerable）的行为将被无效化。所以通常属性都有特性时，可以把configurable设置为true即可。
* writable 是否可写。设置成 false，则任何对该属性改写的操作都无效（但不会报错，严格模式下会报错），默认false。
* enumerable。是否能在for-in循环中遍历出来或在Object.keys中列举出来。

```js
const object1 = {};
Object.defineProperty(object1, 'p1', {
  value: 'lubai',
  writable: false
});

object1.p1 = 'not lubai';

console.log(object1.p1);
```

讲到了defineProperty, 那么肯定离不开Proxy.


#### Proxy

Proxy 是 ES6 中新增的功能，它可以用来自定义对象中的操作。 Vue3.0 中将会通过 Proxy 来替换原本的 Object.defineProperty 来实现数据响应式。

```js
// const obj = {};
// let val = undefined;
// Object.defineProperty(obj, 'a', {
//     set: function (value) {
//         console.log(`${value} - xxxx`);
//         val = value;
//     },
//     get: function () {
//         return val;
//     },
//     configurable: true,
// })

// obj.a = 111;

// console.log(obj.a)

const obj = new Proxy({}, {
    get: function (target, propKey, receiver) {
        console.log(`getting ${propKey}`);
        return target[propKey];
    },
    set: function (target, propKey, value, receiver) {
        console.log(`setting ${propKey}`);
        return Reflect.set(target, propKey, value, receiver);
    }
});

obj.something = 1;
console.log(obj.something);
```

自定义 set 和 get 函数的方式，在原本的逻辑中插入了我们的函数逻辑，实现了在对对象任何属性进行读写时发出通知。

当然这是简单版的响应式实现，如果需要实现一个 Vue 中的响应式，需要我们在 get 中收集依赖，在 set 派发更新，
之所以 Vue3.0 要使用 Proxy 替换原本的 API 原因在于 Proxy 无需一层层递归为每个属性添加代理，一次即可完成以上操作，性能上更好，并且原本的实现有一些数据更新不能监听到，
但是 Proxy 可以完美监听到任何方式的数据改变，唯一缺陷可能就是浏览器的兼容性不好了。

#### Reflect又是个什么东西?

* 将Object对象的一些明显属于语言内部的方法（比如Object.defineProperty），放到Reflect对象上。现阶段，某些方法同时在Object和Reflect对象上部署，未来的新方法将只部署在Reflect对象上。也就是说，从Reflect对象上可以拿到语言内部的方法
* 让Object操作都变成函数行为。某些Object操作是命令式，比如name in obj和delete obj[name]（将命令式转为函数行为），
而Reflect.has(obj, name)和Reflect.deleteProperty(obj, name)让它们变成了函数行为。
* Reflect对象的方法与Proxy对象的方法一一对应，只要是Proxy对象的方法，就能在Reflect对象上找到对应的方法。这就让Proxy对象可以方便地调用对应的Reflect方法，完成默认行为，作为修改行为的基础。也就是说，不管Proxy怎么修改默认行为，你总可以在Reflect上获取默认行为。

但是要注意, 通过defineProperty设置writable为false的对象, 就不能用Proxy了

```js
const target = Object.defineProperties({}, {
    foo: {
        value: 123,
        writable: false,
        configurable: false
    },
});


const proxy = new Proxy(target, {
    get(target, propKey) {
        return 'abc';
    }
});

proxy.foo
```

6. Object.create()

Object.create()方法创建一个新的对象，并以方法的第一个参数作为新对象的__proto__属性的值(根据已有的对象作为原型，创建新的对象。)
Object.create()方法还有第二个可选参数，是一个对象，对象的每个属性都会作为新对象的自身属性，对象的属性值以descriptor（Object.getOwnPropertyDescriptor(obj, 'key')）的形式出现，且enumerable默认为false

```js
const person = {
    isHuman: false,
    printIntroduction: function () {
        console.log(`My name is ${this.name}. Am I human? ${this.isHuman}`);
    }
};
const me = Object.create(person);

me.name = "lubai";
me.isHuman = true;
me.printIntroduction();

console.log(person);

const myObject = Object.create(null)
```

传入第二个参数是怎么操作的呢？

```js
function Person(name, sex) {
    this.name = name;
    this.sex = sex;
}

const b = Object.create(Person.prototype, {
    name: {
        value: 'coco',
        writable: true,
        configurable: true,
        enumerable: true,
    },
    sex: {
        enumerable: true,
        get: function () {
            return 'hello sex'
        },
        set: function (val) {
            console.log('set value:' + val)
        }
    }
})

console.log(b.name)
console.log(b.sex)
```

那么Object.create(null)的意义是什么呢? 平时创建一个对象Object.create({}) 或者 直接声明一个{} 不就够了?

Object.create(null)创建一个对象，但这个对象的原型链为null，即Fn.prototype = null

```js
const b = Object.create(null) // 返回纯{}对象，无prototype

b // {}
b.__proto__ // undefined
b.toString() // throw error
```

所以当你要创建一个非常干净的对象, 没有任何原型链上的属性, 那么就使用Object.create(null). for in 遍历的时候也不需要考虑原型链属性了.

1. Object.assign

浅拷贝, 类似于 { ...a, ...b };

```js
function shallowClone(source) {
    const target = {};
    for (const i in source) {
        if (source.hasOwnProperty(i)) {
            target[i] = source[i];
        }
    }

    return target;
}

const a = {
    b: 1,
    c: {
        d: 111
    }
}

const b = shallowClone(a);


b.b = 2222;

b.c.d = 333;

console.log(b)
console.log(a)
```

8. Object.is

```js
const a = {
    name: 1
};
const b = a;
console.log(Object.is(a, b))

console.log(Object.is({}, {}))
```

#### Promise

大部分promise都讲过了, 大概再来复习一下promise.all吧

```js
function PromiseAll(promiseArray) {
    return new Promise(function (resolve, reject) {
        //判断参数类型
        if (!Array.isArray(promiseArray)) {
            return reject(new TypeError('arguments muse be an array'))
        }
        let counter = 0;
        let promiseNum = promiseArray.length;
        let resolvedArray = [];
        for (let i = 0; i < promiseNum; i++) {
            // 3. 这里为什么要用Promise.resolve?
            Promise.resolve(promiseArray[i]).then((value) => {
                counter++;
                resolvedArray[i] = value; // 2. 这里直接Push, 而不是用索引赋值, 有问题吗
                if (counter == promiseNum) { // 1. 这里如果不计算counter++, 直接判断resolvedArr.length === promiseNum， 会有问题吗?
                    // 4. 如果不在.then里面, 而在外层判断, 可以吗?
                    resolve(resolvedArray)
                }
            }).catch(e => reject(e));
        }
    })
}

// 测试
const pro1 = new Promise((res, rej) => {
    setTimeout(() => {
        res('1')
    }, 1000)
})
const pro2 = new Promise((res, rej) => {
    setTimeout(() => {
        res('2')
    }, 2000)
})
const pro3 = new Promise((res, rej) => {
    setTimeout(() => {
        res('3')
    }, 3000)
})

const proAll = PromiseAll([pro1, pro2, pro3])
    .then(res =>
        console.log(res) // 3秒之后打印 ["1", "2", "3"]
    )
    .catch((e) => {
        console.log(e)
    })
```

再来写一个Promise.allSeettled, 需要返回所有promise的状态和结果

```js
function PromiseAllSettled(promiseArray) {
    return new Promise(function (resolve, reject) {
        //判断参数类型
        if (!Array.isArray(promiseArray)) {
            return reject(new TypeError('arguments muse be an array'))
        }
        let counter = 0;
        const promiseNum = promiseArray.length;
        const resolvedArray = [];
        for (let i = 0; i < promiseNum; i++) {
            Promise.resolve(promiseArray[i])
                .then((value) => {
                    resolvedArray[i] = {
                        status: 'fulfilled',
                        value
                    };

                })
                .catch(reason => {
                    resolvedArray[i] = {
                        status: 'rejected',
                        reason
                    };
                })
                .finally(() => {
                    counter++;
                    if (counter == promiseNum) {
                        resolve(resolvedArray)
                    }
                })
        }
    })
}

```

1、Promise.allSettled() 方法接受一组 Promise 实例作为参数，返回一个新的 Promise 实例   <br>
2、只有等到所有这些参数实例都返回结果，不管是 fulfilled 状态 还是 rejected 状态，包装实例才会结束   <br>
3、返回的新 Promise 实例，一旦结束，状态总是 fulfilled，不会变成 rejected   <br>
4、新的 Promise 实例给监听函数传递一个数组 results 。该数组的每个成员都是一个对象，对应传入 Promise.allSettled 的 Promise 实例。   <br>
每个对象都有 status 属性，对应着 fulfilled 和 rejected 。fulfilled 时，对象有 value 属性，rejected 时，有 reason 属性，对应着两种状态的返回值。   <br>
5、有时候我们不关心异步操作的结果，只关心这些操作有没有结束时，这个方法会比较有用。   <br>


#### 数组

1. Array.flat

flat() 方法会按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组中的元素合并为一个新数组返回

```js
const arr1 = [1, 2, [3, 4]];
arr1.flat();
// [1, 2, 3, 4]

const arr2 = [1, 2, [3, 4, [5, 6]]];
arr2.flat();
// [1, 2, 3, 4, [5, 6]]

const arr3 = [1, 2, [3, 4, [5, 6]]];
arr3.flat(2);
// [1, 2, 3, 4, 5, 6]

//使用 Infinity，可展开任意深度的嵌套数组
const arr4 = [1, 2, [3, 4, [5, 6, [7, 8, [9, 10]]]]];
arr4.flat(Infinity);
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

如何模拟实现Array.flat? 

```js
// 使用 reduce、concat 和递归展开无限多层嵌套的数组
const arr1 = [1, 2, 3, [1, 2, 3, 4, [2, 3, 4]]];

function flatDeep(arr, d = 1) {
    if (d > 0) {
        return arr.reduce((res, val) => {
            if (Array.isArray(val)) {
                res = res.concat(flatDeep(val, d - 1))
            } else {
                res = res.concat(val);
            }
            return res;
        }, [])
    } else {
        return arr.slice()
    }
};

console.log(flatDeep(arr1, Infinity))
// [1, 2, 3, 1, 2, 3, 4, 2, 3, 4]
```

如果不考虑深度, 咱们直接给他无限打平

```js
function flatten(arr) {
    let res = [];
    let length = arr.length;
    for (let i = 0; i < length; i++) {
        if (Object.prototype.toString.call(arr[i]) === '[object Array]') {
            res = res.concat(flatten(arr[i]))
        } else {
            res.push(arr[i])
        }
    }
    return res
}

// 如果数组元素都是Number类型
function flatten(arr) {
	return arr.toString().split(',').map(item => +item)
}

function flatten(arr){
    while(arr.some(item=>Array.isArray(item))){
        arr = [].concat(...arr);
    }
    return arr;
}
```

2. Array.includes

includes() 方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回false。

```js
const array1 = [1, 2, 3];

console.log(array1.includes(2));

const pets = ['cat', 'dog', 'bat'];

console.log(pets.includes('cat'));
```

3. Array.from

3.1 Array.from() 方法从一个类似数组或可迭代对象转换成一个浅拷贝的数组实例。

* arrayLike
想要转换成数组的伪数组对象或可迭代对象。
* mapFn 可选
如果指定了该参数，新数组中的每个元素会执行该回调函数。

3.2 Array.from() 可以通过以下方式来创建数组对象：

* 伪数组对象（拥有一个 length 属性和若干索引属性的任意对象）
* 可迭代对象（可以获取对象中的元素,如 Map和 Set 等）

```js
console.log(Array.from('foo'));

console.log(Array.from([1, 2, 3], x => x + x));

const set = new Set(['foo', 'bar', 'baz', 'foo']);
Array.from(set);
// [ "foo", "bar", "baz" ]

const map = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(map);
// [[1, 2], [2, 4], [4, 8]]

const mapper = new Map([['1', 'a'], ['2', 'b']]);
Array.from(mapper.values());
// ['a', 'b'];

Array.from(mapper.keys());
// ['1', '2'];
```

所以数组去重我们可以怎么做?

```js
function unique (arr) {
  return Array.from(new Set(arr))
  // return [...new Set(arr)]
}
const test = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a'];
console.log(unique(test));


function unique(arr) {
    const map = new Map();
    const array = []; // 数组用于返回结果
    for (let i = 0; i < arr.length; i++) {
        if (!map.has(arr[i])) { // 如果有该key值
            array.push(arr[i]);
            map.set(arr[i], true);
        }
    }
    return array;
}

function unique(arr) {
    if (!Array.isArray(arr)) {
        console.log('type error!')
        return
    }
    const array = [];
    for (let i = 0; i < arr.length; i++) {
        if (!array.includes(arr[i])) { //includes 检测数组是否有某个值
            array.push(arr[i]);
        }
    }
    return array
}
```

如何把arguments转换成真数组

1. [...arguments]  <br>
2. Array.from(arguments)  <br>
3. Array.prototype.slice.call()  <br>



5. Array.of

Array.of() 方法创建一个具有可变数量参数的新数组实例，而不考虑参数的数量或类型。

```js
Array.of(7);       // [7]
Array.of(1, 2, 3); // [1, 2, 3]
```

那怎么去模拟实现它呢?

```js
Array.of = function() {
    return Array.prototype.slice.call(arguments);
};
```

### async await yeild

