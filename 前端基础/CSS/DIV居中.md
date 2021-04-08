### div居中

### 一、使用flex
```js
<head>
    <style>
        .content{
            display: flex;
            justify-content: center;
            align-items: center;
            width: 300px;
            height: 300px;
            background-color: #aaaaaa;
        }
        .cen{
            width: 100px;
            height: 100px;
            background-color: #0099ff;
        }
    </style>
</head>
<body>
<div class="content">
    <div class="cen">100px</div>
</div>
```
效果:

<img src="https://user-images.githubusercontent.com/45973908/113986404-ca770b80-987f-11eb-91e6-b73fc67a25d8.png" width="200"  alt="center"/>

### 二、position(已知宽度)
距上50%，据左50%，然后减去元素自身宽度的一半距离就可以实现
```js
<head>
    <style>
        .content{
            position: relative;
            width: 300px;
            height: 300px;
            background-color: #aaaaaa;
        }
        .cen{
            position: absolute;
            top: 50%;
            left: 50%;
            width: 100px;
            height: 100px;
            background-color: #0099ff;
            margin: -50px 0 0 -50px;
        }

    </style>
</head>
<body>
<div class="content">
    <div class="cen"></div>
</div>
</body>
```

### 三、position transform （元素未知宽度）
```js
<head>
    <style>
        .content{
            position: relative;
            width: 300px;
            height: 300px;
            background-color: #aaaaaa;
        }
        .cen{
            position: absolute;
            top: 50%;
            left: 50%;
            background-color: #0099ff;
            transform: translate(-50%,-50%);
        }
    </style>
</head>
<body>
<div class="content">
    <div class="cen">center</div>
</div>

```
效果:

<img src="https://user-images.githubusercontent.com/45973908/113993692-4cb6fe00-9887-11eb-8c87-1153a0cd5ec0.png" width="200"  alt="center"/>

### 四、position（元素已知宽度）（left，right，top，bottom为0，maigin：auto ）
```js
<head>
    <style>
        .content{
            position: relative;
            width: 300px;
            height: 300px;
            background-color: #aaaaaa;
        }
        .cen{
            position: absolute;
            width: 100px;
            height: 100px;
            background-color: #0099ff;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            margin: auto;
        }
    </style>
</head>
<body>
<div class="content">
    <div class="cen">center</div>
</div>
</body>
```

### 五、table-cell 布局实现

```js
<head>
    <style>
        .content{
            width: 300px;
            height: 300px;
            background-color: #aaaaaa;
            display: table-cell;
            vertical-align: middle;
        }
        .cen{
            margin-left: 100px;
            width: 100px;
            height: 100px;
            background-color: #0099ff;
        }
    </style>
</head>
<body>
<div class="content">
    <div class="cen">center</div>
</div>
</body>

```

isplay：table-cell 会使元素表现的类似一个表格中的单元格td, table-cell 时不要与 float 以及 position: absolute 一起使用，设置了 table-cell 的元素对高度和宽度高度敏感，对margin值无反应，可以响 padding 的设置，表现几乎类似一个 td 元素。

