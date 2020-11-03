
beforeEach的钩子函数，它是一个全局的before 钩子函数， （before each）意思是在 每次每一个路由改变的时候都得执行一遍。

三个参数：

- 1.to: (Route路由对象)  即将要进入的目标 路由对象       to对象下面的属性： path   params  query   hash   fullPath    matched   name    meta（在matched下，但是本例可以直接用）

- 2.from: (Route路由对象)  当前导航正要离开的路由

- 3.next: (Function函数)   一定要调用该方法来 resolve 这个钩子。  调用方法：next(参数或者空)   ***必须调用

```html
router.beforeEach((to, from, next) => {
  /*路由发生改变修改页面的title */
  if(to.meta.title) {
    document.title = to.meta.title
  }
  /*localStorage清空配置*/
  for(let name in routerToClear){
    if(routerToClear.hasOwnProperty(name) && routerToClear[name] === to.name){//到达这些页面
      for(let key in StorageConst.LOCAL_PAGE_LIST){
        localStorage.setItem(StorageConst.LOCAL_PAGE_LIST[key], "");//清除列表里面所有页面缓存
      }
      break;
    }
  }
  next();
})

/**
 * value: to.name
 */
const routerToClear = {
  "home": "home",
  "allotManage": "allot-manage",
}
export default routerToClear
```
