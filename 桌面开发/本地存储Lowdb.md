
### Lowdb
electron应用是桌面级应用，lowdb是用JSON为基本存储结构基于lodash开发的，有lodash的加持，使用方便。优势在于它在持续的维护，有不少好用的插件。同步操作，采用链式调用的写法，。再者，用JSON存储的数据，不管是调用还是备份都很方便。

#### 使用Lowdb
运行
```js
npm install lowdb
```

datastore.js
```js
const low = require('lowdb');
const FileSync = require('lowdb/adapters/FileSync'); // 同步模块
const Memory = require('lowdb/adapters/Memory'); // 存入内存
const path = require('path');
const fs = require('fs-extra');
const os = require('os');
const { remote, app } = require('electron');

// 渲染进程和主进程兼容
const APP = process.type === 'renderer' ? remote.app : app;

// 本地路径一项目目录
// const adapter = new FileSync('datastore.json')
// const STORE_PATH = APP.getAppPath('userData') // 获取electron应用的用户目录
// if (process.type !== 'renderer') {
// if (!fs.pathExistsSync(STORE_PATH)) {
// fs.mkdirpSync(STORE_PATH);
// }
// }

// 本地路径二项目目录
// const adapter = new FileSync(path.join(__dirname, '/datastore.json')) // 初始化lowdb读写的json文件名以及存储路径

// 本地路径三，系统目录
const adapter = new FileSync(path.join(os.homedir(), 'datastore.json')); // 存储在本地目录

let db = low(adapter)

db.defaults({ info: {}, isActivated: false }).write();
db.set('info', {name: 'guo', desc: '前端工程师'}).write();
db.set('info2', {name: 'guo2', desc: '后端工程师'}).write();
let appInfo = db.get('info').value();
let appInfo2 = db.get('info2').value();
console.log('db', appInfo);
console.log('db', appInfo2);

module.exports = db; //模块导出，可在其它js文件中引用
```
