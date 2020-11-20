
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
#### 操作
创建：主要通过set()或者defaults()方法。其中defaults()专门针对空JSON文件进行初始化。
```js
db.defaults({ posts: [], user: {}, count: 0 })
  .write() // 一定要显式调用write方法将数据存入JSON
```
读取：
```js
db.get('posts').value() // []
```
在main进程拿到的内存里的db，和renderer拿到的内存里的db不是同一个db，也就是所谓的不是一个db的两份引用，而是一个db的两份拷贝。main进程对其进行的操作，renderer进程是不知道的。换句话说，main进程对db进行了任何读写操作，renderer拿到的db依然是当初应用打开时所读取的db。所以就会遇到main进程更新了数据，而renderer进程依然无法拿到新的数据。
```js

```

#### 更详细的资料
https://molunerfinn.com/electron-vue-3/
