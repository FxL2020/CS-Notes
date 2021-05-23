## 模块化 & webpack

### 模块化

AMD CMD ESM

模块化的本质利用了闭包

### webpack

1.webpack.config.js 配置文件
1-1 入口

input: '.src/index.js',
找到入口->分析依赖(import require 等等) ->找到依赖的位置 ->分析依赖的依赖 ->repeat -> 构建依赖图

1-2 出口

output: 'dist',
build 之后的产物

2.webpack 打包的基本流程

根据配置的入口-> travel()遍历所以路径（依赖） ->构建一个依赖图->( babel)编译（转ES5）->打包 -> 输出
 ->页面请求->(切片: chunk) ->产出bundle->挂 bundle(html) ->渲染页面-代码变更->
通知-> reload ->渲染

HMR热更新：

client ->websocket ->webpack

启动一个服务，监听文件是否发送变化

webpack? 

- 配置复杂 .dev.js .st.js prod.js, happypack... (作用？) -> 提速 <- webpack 配置工程师
- 慢 开发体验

webpack5 <- 进程级缓存 redis 空间换时间

巨型应用优化
- 微前端 百度云
- ESM （今天的内容），vite、snowpack 等...


ESM 核心的优点？

- 快 （为什么快？）

入口 -> 转换 -> 输出 -> 页面请求 -> 吐对应的 chunk 过去 -> 渲染 -> 代码变更 -> 通知 -> reload -> 渲染

编译原理

file ->'import React from ''react' \n export default ...->
状态机  ->   tokens（字节流） -> parse(解析字节流，while循环）-> ast ->操作对象 ->code generate ->new code



webpack

loader
less -> css -> js node

webpack是基于node，他只能识别js, json，less文件不能识别；
本质上：就是文件资源转换，转成node认识的

loader执行顺序：
倒叙执行loader

 rules: [{
      test: /\.less$/,
      use: [
        { loader: 'style-loader' },
        { loader: 'less-loader' }
      ]
    }]

  //修改查找路径
  resolveLoader: {
    modules: [path.resolve(__dirname, '../loader'), 'node_modules']
  },

less-loader

const less = require('less');

// instance -> bind(webpackResource)
// 处理异步的方式 callback

module.exports = function loader(source) {
  const callback = this.async();

  less.render(source, {sourceMap: {}}, function (err, res) {
    let { css, map } = res;
    callback(null, css, map);
  })
}


插件

compiler 对象代表了完整的 webpack 环境配置。

compilation 对象代表了一次资源版本构建。当前版本编译的资源

生命周期 钩子 -> 函数回调

钩子 -> 函数回调

compiler.hooks.emit.tapAsync

写 plugin 的时候
 // 1. 插件希望执行的时间点
 // 2. 同步的还是异步的，还是返回 promise 
// 3. 用 api 去拼凑功能

compiler.hooks -> 一个对象，上边挂载了一堆钩子

.emit -> 代表的是一堆钩子中的某一个，具体的说，是一个生命周期（时间点）执行，执行的时间点：输出到 output之前执行。

发散想想？有哪些 case? .afterEmit -> 输出到 output 之后 ...

.tap 同步执行
.tapAsync  异步执行
.tapPromise Promise方式执行

 plugins: [
    new UnusedWebpackPlugin({
      // Source directories
      directories: [
        path.join(__dirname, 'awesome-module'),
        path.join(__dirname, 'simple-module'),
      ],
      // Exclude patterns
      exclude: ['**/*.test.js'],
      // Root directory (optional)
      root: __dirname,
      failOnUnused: false,
    }),
    new GzipPlugin()
  ]

压缩的插件

const zlib = require('zlib');

// webpack 执行
// opts -> let i = new YourPlugin(opts) -> i.apply(compiler)

module.exports = class GzipPlugin {

  // 插件配置的参数
  constructor(option = {}) {
    this.option = option;
  }

  // 固定的
  apply(compiler) {
    compiler.hooks.emit.tap('myPlugin', compilation => {
      const assets = compilation.getAssets();
      for (const file of assets) {
        if (/\.js$/.test(file.name)) {  //如果是js文件压缩
          const gzipFile = zlib.gzipSync(file.source._value, {
            level: this.option.level || 7
          });

          compilation.assets[file.name + '.gz'] = {
            source: function () {
              return gzipFile;
            },
            size: function () {
              return gzipFile.length
            }
          }
        }
      }
    })
  }
}

Tree shaking
sideEffects


module , package , bundle, chunk 

module
common.js / amd规范包

package
整个项目

bundle
webpack打包结果

chunk

require.ensure(['./modile'],function(require){
     const result = require('./module');
     console.log(resule);
})

import('/module') impore函数 懒加载

异步加载会被分割打包，由主bundle获取的分包叫chunk

分割公用的
optimization: {
    splitChunks: {
       chunks: 'asyc'/'all'
       minSize: 0
}
}







