
### Axios 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中
Axios是ajax的一种库，简化和健壮了ajax数据请求操作，目前主流浏览器都支持它。请求部分只管请求数据，请求完成后，再承诺对数据处理，这相当于承诺了请求完成后一定会执行结果处理函数，JavaScript中，将这种承诺将来会执行的对象称为promise对象。
### 特性
- 从浏览器中创建 XMLHttpRequests
- 从 node.js 创建 http 请求
- 支持 Promise API
- 拦截请求和响应
- 转换请求数据和响应数据
- 取消请求
- 自动转换 JSON 数据
- 客户端支持防御 XSRF
### 安装
使用npm安装
```html
$ npm install axios
```
