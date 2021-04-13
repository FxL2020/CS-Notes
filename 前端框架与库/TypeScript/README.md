### TypeScript
TypeScript 是 JavaScript 的一个超集，主要提供了类型系统和对 ES6 的支持。<br>
TypeScript 只会进行静态检查，编译为 js 之后，并没有什么检查的代码被插入进来。如果编译时发现有错误，就会报错，但还是会生成编译结果。


### 基本类型
- number
```ts
//声明一个变量同时指定它的类型
let m:number;
m=10;
//变量的声明和赋值同时进行，Ts可以自动对变量进行类型检测
let n=false;
```
- string
- boolean
- array
```ts
let arr:number[] =[1,2,3]
let arr:Array<number> =[1,2,3]
```
- object
- any
任意类型，会关闭ts类型检测    <br>
声明变量如果不指定类型，则Ts解析器会自动判断变量类型为any(隐式)    <br>
any类型的变量可以赋值给任意类型变量    <br>
```ts
let d: any=4
d='hello'
```
- unknown
类型安全的any    <br>
unknown 表示未知类型的值,不能直接赋值给别人，需要先判断或断言
```ts
let c;
c=12;
let d: unknown=4
d='hello'
let e:unknown
    e='string'
let f:string
//解决一，判断类型
if (typeof e==="string"){
    f=e
}

//解决二，断言 告诉解析器变量实际类型
f=e as string
f=<string>e
```
- void 
void 类型表示没有任何类型。 一般用于一个方法没有返回值的情况，方法没有返回值将得到 undefined   <br>
声明void的变量，只能赋值null,undefined
```ts
//对函数参数，返回值进行类型限制
function sum1(a:number,b:number)：number {
    console.log(a+b)
}
```
- never
never 类型表示的是那些永不存在的值的类型，包括 null 和 undefined
```ts
function error(message: string) {
    throw new Error(message)
}
```
- tuple 元组 固定长度数组 ts新增类型
```ts
let n:[string,number]
n=['12',3]
```
- enum枚举 ts新增类型
```ts
enum Gender {
    Male ,
    Female = 1
}
let i:{name:string,gender:Gender}
i={
    name:'12',
    gender:Gender.Female
}
```
- 字面量
```ts
let n: 1|2|3|4
```
#### 定义类型
interface和type的异同 <br>
重点：用interface描述数据结构，用type描述类型 <br>
1.都可以描述一个对象或者一个函数 <br>
```ts
interface User1 {
    name:string
    age:number
}
interface setUser1 {
    (name:string,age:number): void
}
type User2={
    name:string
    age:number
}
type setUser2 ={
    (name:string,age:number):void
}
```
2.都允许扩展(extends)
interface和type都可以扩展，并且两者并不是相互独立的


#### 联合类型 |
取值可以是多种类型中的一种
```ts
let m: string | number
m=12;
m='we'
```
