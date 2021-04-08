### BFC
Formatting context(格式化上下文) <br>

具有 BFC 特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且 BFC 具有普通容器所没有的一些特性。

#### 触发BFC

只要元素满足下面任一条件即可触发 BFC 特性：

- body 根元素
- 浮动元素：float 除 none 以外的值
- 绝对定位元素：position (absolute、fixed)
- display 为 inline-block、table-cells、flex
- overflow 除了 visible 以外的值 (hidden、auto、scroll)

#### BFC特性
##### 一、同一个BFC下外边距会发生重叠

```js
<head>
    <style>
        div{
            width: 100px;
            height: 100px;
            margin: 100px;
            background-color: #0099ff;
        }

    </style>
</head>
<body>
<div></div>
<div></div>
</body>
```
效果

<img src="https://user-images.githubusercontent.com/45973908/113958569-e5cc2180-9853-11eb-9b76-cf73f34f30ca.png" width="200"  alt="BFC"/>

想要避免外边距的重叠，可以将其放在不同的BFC下


```js
<head>
    <style>
        p{
            width: 100px;
            height: 100px;
            margin: 100px;
            background-color: #0099ff;
        }
        .bfc{
            overflow: hidden;
        }

    </style>
</head>
<body>
<div class="bfc">
    <p></p>
</div>
<div class="bfc">
    <p></p>
</div>
</body>
```

效果

<img src="https://user-images.githubusercontent.com/45973908/113960657-5e80ad00-9857-11eb-8ef9-907054570b15.png" width="200"  alt="bfc"/>

##### 二、BFC 可以包含浮动的元素（清除浮动）

浮动的元素会脱离普通文档流

```js
<head>
    <style>
        .content{
            overflow: hidden;  //设置overflow: hidden;前后的效果
            border: solid 1px #0099ff;
        }
        .fl{
            float: left;
            width: 100px;
            height: 100px;
            background-color: #42b983;
        }
    </style>
</head>
<body>
<div class="content">
   <div class="fl"></div>
</div>
</body>
```


