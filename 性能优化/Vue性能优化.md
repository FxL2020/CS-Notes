### Vue性能优化

#### Vue 代码层面的优化

##### 1.1、v-if 和 v-show 区分使用场景
v-if与v-show都可以动态控制dom元素显示隐藏，v-if显示隐藏是将dom元素整个添加或删除，而v-show隐藏则是为该元素添加css--display:none，dom元素还在。<br>

应用场景： v-if 适用于在运行时很少改变条件，不需要频繁切换条件的场景；v-show 则适用于需要非常频繁切换条件的场景。<br>

##### 1.2、computed 和 watch  区分使用场景
computed： 是计算属性，依赖其它属性值，并且 computed 的值有缓存，只有它依赖的属性值发生改变，下一次获取 computed 的值时才会重新计算 computed  的值；
watch： 更多的是「观察」的作用，类似于某些数据的监听回调 ，每当监听的数据变化时都会执行回调进行后续操作；

应用场景：
- 依赖其它数据，进行数值计算时，computed具有缓存特性，避免每次获取值时就要重新计算；<br>
- 当数据变化时执行异步操作或开销较大的操作上，使用watch选型允许执行异步操作，限制执行该操作的频率，并且在得到最终结果前，设置中间状态

##### 1.3、v-for 遍历必须为 item 添加 key，且避免同时使用 v-if

- v-for 遍历必须为 item 绑定 key  <br>
在列表数据进行遍历渲染时，需要为每一项 item 设置（数据唯一标识比如id） key 值，方便 Vue.js 内部机制精准找到该条列表数据。当 state 更新时，新的状态值和旧的状态值对比，较快地定位到 diff 

- v-for 遍历避免同时使用 v-if  <br>
v-for 比 v-if 优先级高，如果每一次都需要遍历整个数组，将会影响速度，尤其是当之需要渲染很小一部分的时候，必要情况下应该替换成 computed 属性。

#### 1.4 长列表性能优化

Vue 会通过 Object.defineProperty 对数据进行劫持，来实现视图响应数据的变化，然而有些时候我们的组件就是纯粹的数据展示，不会有任何改变，我们就不需要 Vue 来劫持我们的数据  <br>
在大量数据展示的情况下，这能够很明显的减少组件初始化的时间，那如何禁止 Vue 劫持我们的数据呢？可以通过 Object.freeze 方法来冻结一个对象，一旦被冻结的对象就再也不能被修改了。

```js
export default {
  data: () => ({
    users: {}
  }),
  async created() {
    const users = await axios.get("/api/users");
    this.users = Object.freeze(users);
  }
};
```
