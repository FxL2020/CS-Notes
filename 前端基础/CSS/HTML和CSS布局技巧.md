### 十种选择器



### 常用的CSS单位
- px:绝对单位，1px代表一个像素点，通常修改段落中文字大小时，除了修改font-size，还要修改line-height

- em:相对大小；1em=多少px，是基于目前这个容器中的font-size大小设定的，取决于使用em单位的标签的父标签（直系），的font-size

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
优势为，更容易计算，只需要更改html标签中的font-size即可统一修改所有rem单位。可以避免元素被多层嵌套后难以预测它的实际大小。

- css3自适应布局单位vw,vh
视口单位(Viewport units)

vh and vw：相对于视口的高度和宽度，而不是父元素的（CSS百分比是相对于包含它的最近的父元素的高度和宽度）。1vh 等于1/100的视口高度，1vw 等于1/100的视口宽度。

当width：100vw；height：100vh时，该元素会占满整个屏幕，当将父元素这样设置后，就能够很好地将子元素进行居中处理；

vmin与vmax
vmin代表屏幕较短的一边，vmax代表屏幕较长的一边，取值也是1~100；在移动端实现屏幕旋转显示。比如：一张正方形的图片：
当宽设为100vmin时，就会以屏幕较短的一边的总长度作为图片的边长，即使旋转屏幕后，边长也不会改变；

当宽设为100vmax时，就会以屏幕较长的一边的总长度作为图片的边长，旋转屏幕后，边长也不会改变，不能显示的区域将会出现滚动轴；

```js
<img src="demo.jpg">

img{
    width:100vmin;
    //width:100vmax;
}
```

