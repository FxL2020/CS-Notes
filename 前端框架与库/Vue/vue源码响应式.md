
```js
export class Vue {
  //传一个配置
  constructor(options = {}) {
    this.$options = options
    this.$el = typeof options.el === 'string' ? document.querySelector(options.el) : options.el
    this.$data = options.data
    this.$methods = options.methods

    this.proxy(this.$data)

    // observer 拦截 this.$data
    new Observer(this.$data)

    new Compiler(this)
  }

  // 代理一下，this.$data.xxx -> this.xxx
  proxy(data) {
    Object.keys(data).forEach(key => {
      // this
      Object.defineProperty(this, key, {
        enumerable: true,
        configurable: true,
        get() {
          return data[key]
        },
        set(newValue) {
          // NaN !== NaN
          if (data[key] === newValue || __isNaN(data[key], newValue)) return
          data[key] = newValue
        }
      })
    })
  }
}

function __isNaN(a, b) {
  return Number.isNaN(a) && Number.isNaN(b)
}

//发布订阅模式

//dep方法 一个收集器
class Dep {
  constructor() {
    this.deps = new Set()
  }
  add(dep) { //收集依赖 使用或者页面渲染得地方
    if (dep && dep.update) this.deps.add(dep)
  }
  notify() { //通知依赖 只发生变化
    this.deps.forEach(dep => dep.update())
  } 
}

// html -> <h1>{{ count }}</h1> -> compiler 发现有 {{ count }}
// -> new Watcher(vm, 'count', () => renderToView(count)) -> count getter 被触发
// -> dep.add(watcher实例) -> this.count++ -> count setter -> dep.notify
// -> () => renderToView(count) -> 页面就变了

//监视值是否发生变化，渲染到页面
class Watcher {
  // vm - Vue 实例
  constructor(vm, key, cb) {
    this.vm = vm
    this.key = key  //当前观察的值
    this.cb = cb // 在我们今天的列子里面，就是绘制数据到页面 回调方法

    //new Watcher实例观察双大括号中变量的时候
    // window.watcher = this
    Dep.target = this
    this.__old = vm[key] // 存下了初始值，触发 getter
    Dep.target = null
  }
  update() {  //notify()方法会触发watcher中的update方法更新渲染页面
    let newValue = this.vm[this.key]
    if (this.__old === newValue || __isNaN(newValue, this.__old)) return
    this.cb(newValue)
  }
}


class Observer {
  constructor(data) {
    this.walk(data)
  }
  walk(data) {
    if (!data || typeof data !== 'object') return
    Object.keys(data).forEach(key => this.defineReactive(data, key, data[key]))  //遍历对象，拿到key value
  }
  defineReactive(obj, key, value) {
    let that = this
    this.walk(value)   //递归data中也可能包含对象
    let dep = new Dep()  //对每个key进行收集依赖
    Object.defineProperty(obj, key, {  //递归的使用defineProperty对属性做一个劫持
      configurable: true,
      enumerable: true,
      get() {
        // Watcher 实例
        //get()的时候会new 一个watcher实例
        Dep.target && dep.add(Dep.target) //在get方法中进行收集依赖
        return value
      },
      set(newValue) {
        if (value === newValue || __isNaN(value, newValue)) return
        value = newValue
        that.walk(newValue)
        dep.notify()  //值发生变化 在set方法中通知依赖
      }
    })
  }
}

class Compiler {
  constructor(vm) {
    this.el = vm.$el
    this.vm = vm
    this.methods = vm.$methods

    this.compile(vm.$el)
  }
  compile(el) {
    let childNodes = el.childNodes
    // 类数组
    Array.from(childNodes).forEach(node => {
      if (this.isTextNode(node)) { //如果是文本节点
        this.compileText(node)
      }
      else if (this.isElementNode(node)) {  //如果是元素节点
        this.compileElement(node)
      }

      if (node.childNodes && node.childNodes.length) this.compile(node)
      // ...
    })
  }
  // <input v-model="msg"/>
  compileElement(node) {
    if (node.attributes.length) {
      Array.from(node.attributes).forEach(attr => {
        let attrName = attr.name
        if (this.isDirective(attrName)) {
          // v-on:click  v-model
          attrName = attrName.indexOf(':') > -1 ? attrName.substr(5) : attrName.substr(2)
          let key = attr.value
          this.update(node, key, attrName, this.vm[key])
        }
        // ...
      })
    }
  }
  update(node, key, attrName, value) {
    if (attrName === 'text') {
      node.textContent = value
      new Watcher(this.vm, key, val => node.textContent = val)
    }
    else if (attrName === 'model') { //双向绑定
      node.value = value
      new Watcher(this.vm, key, val => node.value = val)
      node.addEventListener('input', () => {
        this.vm[key] = node.value
      })
    }
    else if (attrName === 'click') {
      node.addEventListener(attrName, this.methods[key].bind(this.vm))
    }
    // ....
  }
  // 'this is {{ count }}'
  compileText(node) {
    let reg = /\{\{(.+?)\}\}/   //匹配{{}}
    let value = node.textContent
    if (reg.test(value)) {
      let key = RegExp.$1.trim()
      node.textContent = value.replace(reg, this.vm[key]) //取count

      new Watcher(this.vm, key, val => {
        node.textContent = val
      })
    }
  }
  isDirective(str) {
    return str.startsWith('v-')
  }
  isElementNode(node) {
    return node.nodeType === 1 //元素节点
  }
  isTextNode(node) {
    return node.nodeType === 3 //文本节点
  }
}

```
