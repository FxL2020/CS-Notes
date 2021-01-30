### 十种选择器



### 常用的CSS单位
px:绝对单位，1px代表一个像素点，通常修改段落中文字大小时，除了修改font-size，还要修改line-height

em:相对大小；1em=多少px，是基于目前这个容器中的font-size大小设定的，取决于使用em单位的标签的父标签（直系），的font-size

在用em单位设置文字段落的字体大小时，只需要修改父元素的font-size，那么使用em单位的font-size和line-height就不需要更改了，会自动等比例缩放；

```js
    <style>
        body{
            font-size: 10px;
        }
        div{
            font-size: 2em;
        }
    </style>
</head>
<body>
<div>
    wo  //20px
    <div>   //40px
        <div>
            wo  //80px
        </div>
    </div>
</div>
</body>

```
- rem
也就是root em。它与em相似，唯一的不同是它是基于html元素的font-size大小来计算的，不受上一级的父标签影响

```js
    <style>
        html{
            font-size: 10px;
        }
        div{
            font-size: 2rem;
        }
    </style>
</head>
<body>
<div>
    wo
    <div>  wo
        <div>
            wo
        </div>
    </div>
</div>
</body>

```
