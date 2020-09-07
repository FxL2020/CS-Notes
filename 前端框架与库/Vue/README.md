
### 什么是MVVM
MVVM是Model-view-ViewModel的缩写，Model代表数据模型，View代表UI组件，ViewModel是Model和View之间的桥梁，数据会绑定到ViewModel层并自动将数据渲染到页面中，视图变化的时候会通知ViewModel层更新数据
- 与MVC都是一种设计思想，主要是MVC中的controller演变成了ViewModel，mvvm 主要解决了 mvc 中大量的 DOM 操作使页面渲染性能降低，加载速度变慢，影响用户体验。
### 简单说一下Vue2.x响应式数据原理
Vue在初始化数据时，会使用Object.defineProperty重新定义data中的所有属性，当页面使用对应属性时，首先会进行依赖收集（收集当前组件的watcher),如果属性发生变化会通知相关依赖进行更新操作（发布订阅）。
### Vue3.x响应式数据原理
Vue3.x改用Proxy替代Object.defineProperty。因为Proxy可以直接监听对象和数组的变化，并且有多达13种拦截方法。并且作为新标准将受到浏览器厂商重点持续的性能优化。
### vue双向绑定原理
- 数据劫持（vue.js）
vue.js采用数据劫持结合发布者-订阅者模式，通过Object.defineProperty()来劫持各个属性的setter,getter,在数据变动时发布消息给订阅者，触发相应的监听回调。vue是通过数据劫持的方式来做绑定数据的，最核心的就是通过Object.defineProperty()来实现对属性的劫持
1、实现一个数据监听器Observer,能够对数据对象的所有属性进行监听，如有变动可拿到最新值并通知订阅者
通过obeject . defineProperty(来监听属性变动那么将需要observe的数据对象进行递归遍历，包括子属性对象的属性，都加上setter和getter这样的话，给这个对象的某个值赋值，就会触发setter, 那么就能监听到了数据变化，然后通过维护一个数组收集订阅者，数据变动触发notify，在调用订阅者的update方法
2、实现个指令解析器Compile,对每个元素节点的指令进行扫描和解析，根据指令模板替换数据，以及绑定相应的更新函数
3、实现一个Watcher,作为连接Observer和Compile的桥梁， 能够订阅并收到每个属性变动的通知，执行指令绑定的相应回调函数，从而更新视图

https://segmentfault.com/a/1190000006599500
