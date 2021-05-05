### this指向

#### 默认绑定（函数直接调用）
#### 隐式绑定（属性访问调用）
#### 显式绑定（`call`、 `bind`、 `apply`）

#### 箭头函数

非严格模式下：

```js
function fn() {
  console.log(this) // window
}

fn()
```

严格模式下：

```js
function fn() {
  'use strict'
  console.log(this) // undefined
}

fn()
```
 非严格模式下，默认绑定指向全局window（`node` 中式 `global`）
