### 1.CSS权重及其引入方式
#### 常见的css样式引入方式
- 行内样式(内联样式)
为元素添加一个style属性在，style 属性里面直接书写
```html
<h3 style="font-size: 18px; color: #cccccc;">一朵菊花，一个小鬼</h3>
```
- 内部样式表(内嵌样式)
在head标签下添加一个style元素标签，并在标签内编写css样式。
```html
 <style>
            *{
                margin: 0;
                padding: 0;
            }
            body{
                font-size: 12px;
            }
        </style>
```
- 外部样式表(外联样式)
将页面需要的CSS写在一个单独的扩展名为.css的文件中，并用link元素引用
```html
 <head>
        <title>外部样式表</title>
        <link rel="stylesheet" type="text/css" href="..."/>
    </head>
```
- 导入样式表
采用import方式导入CSS样式表
```
<style type="text/css">
            <!--
            @import url("style.css");
            -->
        </style>
```
#### 不同类型的样式编写方式权重顺序
就近原则
内嵌样式 > 内部样式表 > 外联样式表 > 导入样式表
#### CSS选择器分类
- 基础选择器
* 通用
标签选择器
class选择器
id选择器
- 组合选择器
E,F 多元素选择器，同时匹配所有E元素或F元素，E和F之间用逗号分隔
E F 后代元素选择器，匹配所有属于E元素后代的F元素，E和F之间用空格分隔
E>F 子元素选择器，匹配所有E元素的子元素F
E~F 匹配任何在E元素之后的同级F元素
- 属性选择器
[attr] 匹配所有具有attr属性的元素，不考虑它的值
[attr=val] 匹配所有attr属性等于“val”的元素
[attr~=val] 匹配所有attr属性具有多个空格分隔的值,其中一个值等于“val”的元素
- 伪类选择器
:first-child 匹配元素的第一个子元素
:link 匹配所有未被点击的链接
:visited 匹配所有已被点击的链接
:active 匹配鼠标已经其上按下、还没有释放的元素
:hover 匹配鼠标悬停其上的元素
:disabled 匹配表单中禁用的元素
:checked 匹配表单中被选中的radio或checkbox元素
- 伪元素选择器
::first-leter 匹配元素内容的第一个字母
:before, ::before 为当前元素创建一个子元素作为伪元素。常通过 content 属性来为一个元素添加修饰性的内容。 此元素默认为行内元素
#### CSS样式权重优先级与计算
important > 内嵌样式 > ID > 类 > 标签 | 伪类 | 属性选择 > 伪对象 > 继承 > 通配符
第一等：代表内联样式，如: style=””，权值为1000。
第二等：代表ID选择器，如：#content，权值为100。
第三等：代表类，伪类和属性选择器，如.content，权值为10。
第四等：代表类型选择器和伪元素选择器，如div p，权值为1。
参考 https://www.cnblogs.com/damingge/p/6498813.html
