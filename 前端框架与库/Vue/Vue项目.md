<img src="./img/logo.jpg" style='float: right; width:200px;height:70px'>

# 05.16 【讲义】Vue 项目实战

# vue-cli4 介绍
## 安装
```sh
npm install -g @vue/cli
# OR
yarn global add @vue/cli
```
## 查看版本 `vue --version`

## 更新
```sh
npm update -g @vue/cli

# OR
yarn global upgrade @vue/cli@4
```

## 常用命令
* vue --help
* vue --version
* vue inspect  输出webpack配置内容
  * vue inspect > output.js
  * vue inspect --mode production > output.prod.js
* vue create 创建项目
2.x
* vue ui

npm install reset-css
yarn add reset-css
去掉浏览器默认样式

更详细的vue.config.js配置
https://www.jianshu.com/p/b358a91bdf2d

## vue.config.js 配置介绍
* 不自持import语法，要用require，因为是在Node端使用
* 如何去掉source-map: productionSourceMap
* 如何设置静态资源: publicPath，旧版本是baseUrl
* 如何更改打包目录: assetDir
* 如何使用带complier版本的vue: runtimeComplier
* devServer
  * 本地开发如何做代理
    ```
      devServer: {
        proxy: {
          '/api': {
            target: 'http://localhost:3000',
            changeOrigin: true
          } 
        }
      },
    ```

## vue.config.js 更改webpack配置
* chainWebpack
  * 可以获取webpack已有的配置，增加自己的逻辑，进行增删改查
* configWebpack
  * 类似于webpackMerge

# 服务端渲染 server-side-render
## 客户端渲染
## 服务端渲染
### 优点
* SEO 优化
* 减少白屏时间
### 缺点
* 占用服务器资源
* 支持的api有限，支持beforeCreate created生命周期

![avatar](./vue_ssr.jpeg) 

### 用法
* npm install -s vue-server-renderer
* 服务端的包 koa koa-router koa-static koa-mount

### 问题
* 如何区分客户端打包还是服务端打包
  * cross-env 传入环境变量，区分server client
  ```
   "build:server": "cross-env VUE_ENV=server vue-cli-service build  --no-clean",

  // nodemon.json 设置环境变量, pm2也可以设置
  "env": {
      "VUE_ENV": "server",
  },

  process.env.VUE_ENV === 'server'
  ```
* 添加两个webpack入口, server-entry client-entry
  * webpack添加entry配置
  * server-entry
    * 输出一个函数，返回promise

* 服务端代码启动
  * 监听端口
    ```
    const app = new Koa()
    app.listen(port, () => {
      console.log(`server started at port: ${port}`)
    })
    ```
  * 启动服务端路由
    ```
    const router = new KoaRouter()
    router.get('/(.*)', async ctx => {})
    app.use(router.routes())
    ```
  * 添加静态资源处理
    ```
    app.use(KoaMount('/assets', KoaStatic(path.resolve(__dirname, '../dist/assets'))))

    ```


* 服务端渲染基本流程
  * 添加server-entry，webpack入口，返回一个函数
    ```
    export default (context) => {
        return new Promise((resolve, reject) => {
            const {app} = createVueApp()

            resolve(app)
        })
    }
    ```
  * 将vue组件产出dom字符串，并插入到html中
    * 服务端打包添加`vue-server-renderer/server-plugin`插件

    * 服务端代码读取上述插件的产物，传入到`createBundleRenderer`生成`render`实例

    ```
    const serverBundle = require('../dist/vue-ssr-server-bundle.json')
    const template = fs.readFileSync(path.resolve(__dirname, '../public/server.html'), 'utf-8')
    
    const render = VueServerRenderer.createBundleRenderer(serverBundle, {
        runInNewContext: false,
        template, //会将html字符串替换 <!--vue-ssr-outlet--> 这个注释
    })
    ```

    * 在路由里面调用`render.renderToString()`，执行定义的`server-entry`后，得到html字符串，返回给客户端

    ```
      render.renderToString({}, (err, html) => {
          if(err) {
              reject(err)
          }
          resolve(html)
      })

    ```
* 如何激活(Hydrate)
  * 在`createBundleRenderer`中传入由`vue-server-renderer/client-plugin`插件生成的文件，会将客户端打包的JS注入

  ```
  const clientManifest = require('../dist/vue-ssr-client-manifest.json')

    const render = VueServerRenderer.createBundleRenderer(serverBundle, {
        runInNewContext: false,
        template,
        clientManifest, // 注入客户端JS，script标签
    })

  ```

* 路由如何处理
  * 服务端将`url`通过`context`传入到`server-entry`中，执行`router.onReady`确保异步路由解析完毕

  ```
  // server-router
  const context = {url: ctx.path}
  render.renderToString(context,(err, html) => {})

  // server-entry.js
  // 根据服务端传入的url，设置当前客户端的url
  router.push(context.url)
  ```

* 异步路由如何处理
  ```
  // server-entry.js
  router.onReady(() => {
    resolve(app) 
  }, reject)

  ```

* ssr添加vue-loader配置
  ```
  config.module
    .rule('vue')
    .use('vue-loader')
    .tap((options) => {
      if (isServer) {
        options.cacheIdentifier += '-server'
        options.cacheDirectory += '-server'
      }
      options.optimizeSSR = isServer
      return options
    })

    // node端不需要打包node_modules里面的模块
    externals = nodeExternals({
        // 允许打包css文件
        allowlist: /\.css$/
    })

  ```
* 静态资源路径问题
  * 添加koa-static中间件
  * app.use(KoaMount('/assets', KoaStatic(path.resolve(__dirname, '../dist/assets'))))


* 如何等待异步请求的数据返回后，再渲染页面；客户端中的store如何同步服务端的数据；
  * 组件中添加`serverPrefetch`选项，返回promise
  * 服务端入口添加`context.rendered`回调，渲染完成后执行
  * 设置`context.state = store.state`
  * 客户端入口获取`window.__INITIAL_STATE__`，设置`store`初始状态
   ```
   // server-entry
    context.rendered = () => {
        context.state = store.state
    }

    // client-entry
    if(window.__INITIAL_STATE__) {
      store.replaceState(window.__INITIAL_STATE__)
    }
   ``` 


* 热更新
  * 改用代码获取webpack配置及启动webpack服务
   ```
      // 1. 获取webpack配置文件
      const webpackConfig = require('@vue/cli-service/webpack.config')

      // 2. 编译webpack配置文件
      const serverComplier = webpack(webpackConfig) 

   ```
  * 将webpack打包的结果输出到内存中

    ```
      // 3. 设置webpack打包到内存中
      const mfs = new MemoryFS()
      serverComplier.outputFileSystem = mfs
    ```

  * 监听webpack打包的结果，更新bundle

    ```
      // 4.监听文件的修改，获取最新的vue-ssr-server-bundle.json
      let bundle
      serverComplier.watch({}, (err, stats) => {
          if(err) {
              throw(err)
          }
          stats = stats.toJson()
          stats.errors.forEach(error => console.error(error))
          stats.warnings.forEach(warning => console.warn(warning))

          const bundlePath = path.join(webpackConfig.output.path, 'vue-ssr-server-bundle.json')
          bundle = JSON.parse(mfs.readFileSync(bundlePath, 'utf-8'))
          console.log('new bundle created')
      })

    ```


  * 设置路由，获取客户端的manifest.json
    ```
      router.get('/(.*)', async ctx => {
          if(!bundle) {
              ctx.body = '正在构建中，请稍后刷新重试'
              return;
          }

          const clientManifestResp = await axios.get(`http://localhost:${process.env.CLIENT_PORT || '8080'}/vue-ssr-client-manifest.json`)

          const render = VueServerRenderer.createBundleRenderer(bundle, {
              runInNewContext: false,
              template,
              clientManifest: clientManifestResp.data,
          })

          

          ctx.body = await new Promise((resolve, reject) => {
              const context = {url: ctx.path}
              render.renderToString(context, (err, html) => {
                  if(err) {
                      reject(err)
                  }
                  resolve(html)
              })
          })
      })
    ```

  * 设置publicPath，以便可以访问静态资源

    ```
    publicPath = `http://localhost:${process.env.CLIENT_PORT || 8080}`

    ```

  * 热更新设置可跨域访问

    ```
    headers: { 'Access-Control-Allow-Origin': '*' },
    ```
  * 服务端入口webpack配置去掉热更新插件
    ```
    if (isServer) {
      config.plugins.delete('hmr')
    }
    ```


* meta、title等标签如何注入
  ```
  // 注册插件
  // App组件中定义默认的metaInfo
  metaInfo: {
    // if no subcomponents specify a metaInfo.title, this title will be used
    title: 'Default Title',
  }

  // 子组件中覆盖默认的metaInfo
  metaInfo() {
    return {
      title: this.newsInfo.title,
      meta: [
        {name: 'description', content: this.newsInfo.title.substr(0, 10)},
        {name: 'keywords', content: this.newsInfo.title.substr(10, 20)}
        // { charset: 'utf-8' },
        // { name: 'viewport', content: 'width=device-width, initial-scale=1' }
      ]
    }
  },

  // server-entry中拿到meta，并将其传入到context中
  const meta = app.$meta()
  // ...
  context.meta = meta

  // html模板中添加此标签
    {{{ meta.inject().title.text() }}} 
    {{{ meta.inject().meta.text() }}}
  ```
* 服务端渲染会执行的生命周期，及要注意的问题
  * 只执行beforeCreate created；不要在这两个生命周期里面添加定时器或者使用window等

* 本地开发时CSS注入到style中
  ```
  if(isServer) {
    config.module
      .rule('vue')
      .use('cache-loader')
      .tap((options) => {
        // Change cache directory for server-side
        options.cacheIdentifier += '-server'
        options.cacheDirectory += '-server'
        return options
      })
  }
  ```
* 生产环境css配置
  ```

    if(isServer) {
      // fix ssr bug: document not found -- https://github.com/Akryum/vue-cli-plugin-ssr/blob/master/lib/webpack.js
      const isExtracting = config.plugins.has('extract-css')
      console.log('isExtracting', isExtracting)
      if (isExtracting) {
        // Remove extract
        for (const lang of langs) {
          for (const type of types) {
            const rule = config.module.rule(lang).oneOf(type)
            rule.uses.delete('extract-css-loader')
            // Critical CSS
            rule
              .use('vue-style')
              .loader('vue-style-loader')
              .before('css-loader')
          }
        }
        config.plugins.delete('extract-css')
      }

    }


    // ... or 都设置false
    css: {
      extract: true,
      sourceMap: true
    },
  ```

# 项目需求
## 1. 明确需求
### 首页
* 左侧边栏是新闻频道导航
* 内容区是新闻列表
* 右侧是更多和友情链接
### 新闻详情页
* 左侧是分享及评论数量
* 内容区包含新闻详情 + 推荐新闻列表
* 右侧是作者简介
## 2. 确定Layout
* 头部 + 主体（左中右，左侧固定）
* 头部（左侧和下侧支持自定义）
* 左侧
* 内容
* 右侧
## 3. 划分组件
### Layout组件
### button组件
### 新闻列表组件
## 4. 编写代码

# 其他问题
## 如何透传属性
```
inheritAttrs: false

// 模板中
v-bind="$attrs"
```

## less-loader版本的问题
* TypeError: this.getOptions is not a function，改用@7.3.0版本

## vue 无限滚动组件
https://peachscript.github.io/vue-infinite-loading/zh/guide/


## 自动注入css公共文件
```
const types = ['vue-modules', 'vue', 'normal-modules', 'normal']

chainWebpack: (config) => {
types.forEach(type => addStyleResource(config.module.rule('less').oneOf(type)))
}

function addStyleResource (rule) {
  rule.use('style-resource')
    .loader('style-resources-loader')
    .options({
      patterns: [
        path.resolve(__dirname, './src/styles/global.less'),
      ],
    })
}

```

## 服务端ajax请求必须是是绝对路径
```
// webpack config
new webpack.DefinePlugin({
  'process.env.API_BASE': '"http://localhost:3000"'
})

// axios
axios.create({
    baseURL: (process.env.API_BASE || '') + '/api',
})
```

## XSS问题(使用v-html时要注意)

## 请求错乱demo

## a链接
* rel="noopener noreferrer nofollow"
## vscode eslint自动修复
安装eslint插件，并添加如下配置
```
"editor.codeActionsOnSave": {
    "source.fixAll": true
}

```
