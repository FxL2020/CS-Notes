### TypeScript


#### 一、你觉得使⽤ts的好处是什么?

1.1 TypeScript是JavaScript的加强版，它给JavaScript添加了可选的静态类型和基于类的⾯向  <br>
对象编程，它拓展了JavaScript的语法。所以ts的功能⽐js只多不少.  <br>
1.2 Typescript 是纯⾯向对象的编程语⾔，包含类和接⼝的概念.  <br>
1.3 TS 在开发时就能给出编译错误， ⽽ JS 错误则需要在运⾏时才能暴露。  <br>
1.4 作为强类型语⾔，你可以明确知道数据的类型。代码可读性极强，⼏乎每个⼈都能理解。  <br>
1.5 ts中有很多很⽅便的特性, ⽐如可选链  <br>

#### 二、如何基于⼀个已有类型, 扩展出⼀个⼤部分内容相似, 但是有部分区别的类型?
1.通过Pick和Omit
```ts
interface User {
    name:string
    age:number
    height:string
}

type name=Pick<User,'name'>
const u1:name={
    name: 'we'
}
type withoutName=Omit<User, 'name'>
const u2:withoutName={
    age:10,
    height:'we'
}
```
2.泛型
```ts
interface User<T> {
    name:T
}
type u1=User<string>
type u2=User<number>
const v1:u1={
    name:'12'
}
const v2:u2={
    name:12
}
```
3.Partical，Required

#### 三、写⼀个计算时间的装饰器
index.ts
```ts
export function measure(target: any, name: any, descriptor: any) {
    const oldValue = descriptor.value;
    descriptor.value = async function() {
        const start = Date.now();
        const ret = await oldValue.apply(this, arguments);
        console.log(`${name}执行耗时 ${Date.now() - start}ms`);
        return ret;
    };
    return descriptor;
}
```
home.vue
```ts
import {measure} from '../decorator/index'

 @measure
  public async created(){
    await this.longTimeFn();
  }
  private longTimeFn(){
    return new Promise((resolve => {
      setTimeout(resolve,3000)
    }))
  }
```

#### 四、写⼀个缓存的装饰器
```ts
const cacheMap = new Map();

export function EnableCache(target: any, name: string, descriptor: PropertyDescriptor) {
    const val = descriptor.value;
descriptor.value = async function(...args: any) {
    const cacheKey = name + JSON.stringify(args);
    if (!cacheMap.get(cacheKey)) {
        const cacheValue = Promise.resolve(val.apply(this, args)).catch((_) => cacheMap.set(cacheKey, null));
        cacheMap.set(cacheKey, cacheValue);
    }
    return cacheMap.get(cacheKey);
};
return descriptor;
}
```
