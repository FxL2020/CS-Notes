
### Electron
npm init   ->package.json
npm install electron --save-dev
npx electron -v
./node_modules/.bin/electron

Electron
运行流程：
先找Package.json文件-->main.js  主进程文件--->mainWindow.loadFile()渲染进程 读取页面布局和演示---》IPC在主进程执行任务和获取信息    <br>

mainWindow = new BrowserWindow({})  //打开窗口     <br>
webpreferences:{nodeIntegration:true}  //启用node下的所有东西都可以渲染使用    <br>

render ->index.js //渲染    <br>

调试错误：view -->toggle Developer Tools    <br>
n
remote模块    <br>
实现复用    <br>
require('electron').remote.BrowserWindow //通过remote使用主进程BrowserWindow方法  渲染进程可以使用主进程的对象，方法    <br>

菜单：
```js
const {Menu}=require('electron')
var template =[{}]
Menu.buildFormTemplate(template)  //构建模板
```
绑定事件：
```js
{ label: ' 书'，
click:()=>{
var win =new BrowserWindow({
width:500,
height:500,
webpreferences:{nodeIntegration:true}
})
win.loadFile('er.html')  //新窗口载入页面
win.on('closed',()=>{win=null})  //监听关闭事件
}
}
```

嵌入网页和打开子窗口

子窗口向父窗口传递信息
window.opener.postMessage('传递的信息'，传递给那个父窗口)  //两个参数，一个参数默认传递所有的
```js
接受消息：window.addEventListener('message',(msg)=>{})
let mytext = document.querySelector(''#mytext')
mytext.innerHTML =JSON.stringify(msg.data)
```
electron-vue的原理    <br>
Electron桌面应用中有两个进程，分别是Main主进程和Renderer渲染进程。    <br>
主进程 Main Process 处理原生应用逻辑    <br>
渲染进程 Render Process 负责界面渲染    <br>
主进程和渲染进程之间通信    <br>
渲染进程默认创建主窗口，主窗口可以创建子窗口；渲染进程也可以创建主窗口的其他同级窗口    <br>
Electron运行流程：    <br>
先找Package.json文件-->main.js  主进程文件--->mainWindow.loadFile()渲染进程 读取页面布局和演示-->IPC在主进程执行任务和获取信息    <br>

#### 配置
Winodws开发环境配置    <br>
安装最新版本的Node.js 地址：https://nodejs.org/en/download/    <br>
安装完成后，需要来确认Node.js是否可以正常工作，    <br>
通过以下命令来确认 node 和 npm已经安装成功：    <br>
#下面这行的命令会打印出Node.js的版本信息    <br>
node -v
#下面这行的命令会打印出npm的版本信息    <br>
npm -v

进程通信    <br>
1，ipc模块    <br>
1.1、ipcMain    <br>
ipcMain.on(channel, listener)    <br>
监听 channel，当接收到新的消息时 listener 会以 listener(event, args...) 的形式被调用。    <br>
1.2、ipcRenderer    <br>
ipcRenderer.on(channel, listener)    <br>
监听 channel, 当新消息到达，将通过 listener(event, args...) 调用 listener    <br>
ipcRenderer.send(channel[, arg1][, arg2][, ...])    <br>
通过 channel 发送异步消息到主进程，可以携带任意参数。 在内部，参数会被序列化为 JSON，因此参数对象上的函数和原型链不会被发送。    <br>
主进程可以使用 ipcMain 监听channel来接收这些消息。    <br>
2、webContents.send方法（Main进程主动向Renderer进程发送消息）    <br>
webContents.send是BrowserWindow类的一个方法，BrowserWindow类用于创建一个程序窗口，实例化之后，设置窗口宽高，并设置其loadURL(加载的页面)，一个窗口就创建成功并开始显示。    <br>
主进程：mainWindow.webContents.send('list', res.data);    <br>
渲染进程中，依旧是使用ipcRenderer对消息进行接收：    <br>
ipcRenderer.on('list', (e, msg) => {
  console.log(msg);
  });
}
3、remote模块    <br>
emote模块支持RPC风格的通信，在渲染进程中获取主进程创建的一些全局对象和应用信息    <br>
