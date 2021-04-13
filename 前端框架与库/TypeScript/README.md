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
interface和type的异同   <br>
重点：用interface描述数据结构，用type描述类型   <br>
1.都可以描述一个对象或者一个函数   <br>
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
interface和type都可以扩展，并且两者并不是相互独立的，interface可以extends type,type也可以extends interface
```ts
//interface extends interface
interface Name1 {
    name: string;
}
interface User1 extends Name1{
    age:number;
}
//type extends type
type Name2 = {
    name: string;
}
type User2=Name2 & {
    age: number;
}
//interface extends type
type Name3 = {
    name: string;
}
interface User3 extends Name3{
    age: number;
}
//type extends interface
interface Name4{
    name:string;
}
type User4=Name4 &{
    age:number;
}
```
3.只有type可以做的
type 可以声明基本类型别名，联合类型，元组等类型
```ts
//基本类型别名
type str=string
//联合类型
interface Dog {
    wang()
}
interface Cat {
    miao()
}
type Pet=Dog | Cat
//具体定义数组每个位置的类型
type PetList=[Dog,Cat]
```
#### 联合类型 |
取值可以是多种类型中的一种
```ts
let m: string | number
m=12;
m='we'
```

#### 泛型
泛型是指在定义函数，接口或类的时候，不预先指定具体的类型，使用时再去指定类型的一种特性（返回值，参数，属性的类型）<br>
可以把泛型理解为代表类型的参数<br>
定义泛型函数
```ts
function test<T>(arg: T) {
    return arg
}
```
###### 使用泛型
######方式一 直接使用
```ts
test(10)
```
使用时可以直接传递参数使用，类型会由TS自动推断出来，但有时编译器无法自动推断时还需要使用下面的方式<br>
######方式二 指定类型
```ts
test<number>(10)
```
#### typeof
typeof操作符可以用来获取一个变量声明或对象的类型
```ts
function toArray(x:number):Array<number> {
    return [x]
}
type f=typeof toArray
```

#### keyof
Keyof 操作符可以⽤来⼀个对象中的所有 key 值：
```ts
interface u {
    name:string;
    age:number
}
type k1=keyof u
const k2:k1 ="name"
```

#### extends
有时候我们定义的泛型不想过于灵活或者说想继承某些类等，可以通过 extends 关键字添加泛
型约束
```ts
interface LengthWise {
    length: number;
}

function identify<T extends LengthWise>(arg: T): T {
    console.log(arg.length);
    return arg;
}

identify({length:10,value:3})
identify({length:4})
```

#### Paritial
Partial<T> 的作用就是将某个类型里的属性全部变为可选项 ?
```ts
interface u {
    name:string;
    age:number
}
type p=Partial<u>
const u1:p={
    name:'we'
}
```
#### Reuqired
Required<T> 的作用就是将某个类型里的属性全部变为必选项。
```ts
interface u {
    name?:string;
    age?:number
}
type r=Required<u>
const u1:r={
    name:'we',
    age:23
}
```
#### Readonly 
Readonly<T> 的作用是将某个类型所有属性变为只读属性，也就意味着这些属性不能被重新赋值。

#### Record 
Record<K extends keyof any, T> 的作用是将 K 中所有的属性的值转化为 T 类型。
```ts
interface PageInfo {
  title: string;
}
type Page = "home" | "about" | "contact";

const x: Record<Page, PageInfo> = {
  about: { title: "about" },
  contact: { title: "contact" },
  home: { title: "home" }
};
```

#### Exclude
Exclude<T, U> 的作用是将某个类型中属于另一个的类型移除掉。

```ts
type T0 = Exclude<"a" | "b" | "c", "a">; // "b" | "c"
type T1 = Exclude<"a" | "b" | "c", "a" | "b">; // "c"
```

#### Extract
Extract<T, U> 的作用是从 T 中提取出 U。
```ts
type T0 = Extract<"a" | "b" | "c", "a" | "f">; // "a"
type T1 = Extract<string | number | (() => void), Function>; // () => void
```
