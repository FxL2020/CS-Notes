
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

### Vue在跨域请求时携带cookie的配置withCredentials: true
Vue在发起跨域请求时，后端已经开启CORS，前端需要也携带cookie，此时需要在前端请求头加上withCredentials: true，表示请求可以携带cookie，
```html
 axiosInstance = axios.create({
        withCredentials: true,//携带cookie
        //转换数据的方法
        transformRequest: [
            (data) => {
                return qs.stringify(data, {arrayFormat: 'indices', allowDots: true});
            }
        ],
        //设置请求头
        headers: {
            'Content-Type': 'application/x-www-form-urlencoded'
        }
```
```html
axios.post(this.host + '/users/', {
                        username: this.username,
                        password: this.password,
                        password2: this.password2,
                        mobile: this.mobile,
                        sms_code: this.sms_code,
                        allow: this.allow.toString()
                    }, {
                        responseType: 'json',
                        withCredentials: true
                    })
                    .then(response => {
                         // 记录用户的登录状态
                        sessionStorage.clear();
                        localStorage.clear();

                        localStorage.token = response.data.token;
                        localStorage.username = response.data.username;
                        localStorage.user_id = response.data.id;

                        location.href = '/index.html';
                    })
                    .catch(error=> {
                        if (error.response.status == 400) {
                            if ('non_field_errors' in error.response.data) {
                                this.error_sms_code_message = error.response.data.non_field_errors[0];
                            } else {
                                this.error_sms_code_message = '数据有误';
                            }
                            this.error_sms_code = true;
                        } else {
                            console.log(error.response.data);
                        }
                    })
```
