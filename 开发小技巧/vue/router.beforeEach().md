
beforeEach的钩子函数，它是一个全局的before 钩子函数， （before each）意思是在 每次每一个路由改变的时候都得执行一遍。

三个参数：

- 1.to: (Route路由对象)  即将要进入的目标 路由对象       to对象下面的属性： path   params  query   hash   fullPath    matched   name    meta（在matched下，但是本例可以直接用）

- 2.from: (Route路由对象)  当前导航正要离开的路由

- 3.next: (Function函数)   一定要调用该方法来 resolve 这个钩子。  调用方法：next(参数或者空)   ***必须调用

 
