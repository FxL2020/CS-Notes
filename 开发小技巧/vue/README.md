### vue使用@方式引入，配置vue.config.js文件
项目中使用引入文件有时候路径比较深，需要使用"../../../xx.js"比较繁琐，可以使用webpack的别名alias来解决
- vue.config.js
```html
const path = require("path");
function resolve(dir) {
  return path.join(__dirname, dir);
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
然后配置webpack.config.js路径
```html
settings-->Languages&Frameworks-->JavaScript-->项目名-->node_modules-->@vue-->@cli-service-->webpack.config.js
```
或者
先确定项目中是否有path模块，
```html
node_modules-->path
```
如果没有path模块需要先安装path
```html
npm install path --save
```
