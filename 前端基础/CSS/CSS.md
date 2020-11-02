### 1.CSS权重及其引入方式
- 行内样式(内联样式)
为元素添加一个style属性在，style 属性里面直接书写
<h3 style="font-size: 18px; color: #cccccc;">一朵菊花，一个小鬼</h3>
- 内部样式表(内嵌样式)
在head标签下添加一个style元素标签，并在标签内编写css样式。
 <style>
            *{
                margin: 0;
                padding: 0;
            }
            body{
                font-size: 12px;
            }
        </style>
- 外部样式表(外联样式)
将页面需要的CSS写在一个单独的扩展名为.css的文件中，并用link元素引用
 <head>
        <title>外部样式表</title>
        <link rel="stylesheet" type="text/css" href="..."/>
    </head>
- 导入样式表
采用import方式导入CSS样式表
<style type="text/css">
            <!--
            @import url("style.css");
            -->
        </style>

