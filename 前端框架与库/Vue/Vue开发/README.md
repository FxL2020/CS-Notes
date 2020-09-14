
### 1,vue开发使用@路径引入，vue.config.js配置
项目中有的时候引用文件路径比较深，使用“../../../config.js”就比较麻烦，这时候就可以使用webpack的别名alias来解决
vue.config.js配置文件
```html
const path=require('path')
function resolve (dir) {
  return path.join(__dirname, dir)
}
module.exports = {
  chainWebpack: config => {
    config.resolve.alias
      .set("@", resolve("src"))
      .set("assets", resolve("src/assets"))
      .set("components", resolve("src/components"))
      .set("base", resolve("baseConfig"))
      .set("public", resolve("public"));
  },
}
```
### 2,关于Vue中main.js，App.vue，index.html之间关系进行总结
https://www.cnblogs.com/chenleideblog/p/10484554.html
