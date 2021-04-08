
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
