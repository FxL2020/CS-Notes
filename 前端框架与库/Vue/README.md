
### 什么是MVVM
MVVM是Model-view-ViewModel的缩写，Model代表数据模型，View代表UI组件，ViewModel是Model和View之间的桥梁，数据会绑定到ViewModel层并自动将数据渲染到页面中，视图变化的时候会通知ViewModel层更新数据
- 与MVC都是一种设计思想，主要是MVC中的controller演变成了ViewModel，mvvm 主要解决了 mvc 中大量的 DOM 操作使页面渲染性能降低，加载速度变慢，影响用户体验。
### 简单说一下Vue2.x响应式数据原理
Vue在初始化数据时，会使用Object.defineProperty重新定义data中的所有属性，当页面使用对应属性时，首先会进行依赖收集（收集当前组件的watcher),如果属性发生变化会通知相关依赖进行更新操作（发布订阅）。
### Vue3.x响应式数据原理
Vue3.x改用Proxy替代Object.defineProperty。因为Proxy可以直接监听对象和数组的变化，并且有多达13种拦截方法。并且作为新标准将受到浏览器厂商重点持续的性能优化。
### vue双向绑定原理
- 数据劫持（vue.js）

