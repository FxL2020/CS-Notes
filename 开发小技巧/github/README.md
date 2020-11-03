
#### 一，如何在github上新键文件夹
```html
github-->create new file-->code/新文件夹名/README.md-->commit new file
```
- github上不允许新键一个空的文件夹所以下面建了一个README.md文件

#### 二，如何加速国内Github访问
- 修改hosts文件
1 获取GitHub官方CDN地址<br>
打开https://www.ipaddress.com/
2 查询以下三个链接的DNS解析地址<br>
github.com<br>
assets-cdn.github.com<br>
github.global.ssl.fastly.net<br>
2 修改系统Hosts文件<br>
打开系统hosts文件(需管理员权限)。<br>
路径：C:\Windows\System32\drivers\etc<br>
3 刷新系统DNS缓存<br>
Windows+X 打开系统命令行（管理员身份）或powershell<br>
运行 ipconfig /flushdns 手动刷新系统DNS缓存。<br>
- win10下以管理员身份打开hosts文件
1 文件-> 2 打开windows PowerShel(R) 3 以管理员身份打开windows PowerShel(A) 4先后执行两个命令cmd        notepad hosts 在记事本中修改hosts文件<br>
