
### qs.parse()、qs.stringify()使用方法
qs是一个npm仓库所管理的包,可通过npm install qs命令进行安装.
- qs.parse()将URL解析成对象的形式
```html
const Qs = require('qs');
let url = 'method=query_sql_dataset_data&projectId=85&appToken=7d22e38e-5717-11e7-907b-a6006ad3dba0';
Qs.parse(url);
console.log(Qs.parse(url));
```
- qs.stringify()将对象 序列化成URL的形式，以&进行拼接
```html
const Qs = require('qs');
let obj= {
     method: "query_sql_dataset_data",
     projectId: "85",
     appToken: "7d22e38e-5717-11e7-907b-a6006ad3dba0",
     datasetId: " 12564701"
   };
Qs.stringify(obj);
console.log(Qs.stringify(obj));
```
https://blog.csdn.net/suwu150/article/details/78333452
