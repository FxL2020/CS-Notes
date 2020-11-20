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
标签选择器<br>
class选择器<br>
id选择器<br>
- 组合选择器<br>
E,F 多元素选择器，同时匹配所有E元素或F元素，E和F之间用逗号分隔<br>
E F 后代元素选择器，匹配所有属于E元素后代的F元素，E和F之间用空格分隔<br>
E>F 子元素选择器，匹配所有E元素的子元素F<br>
E~F 匹配任何在E元素之后的同级F元素<br>
- 属性选择器
[attr] 匹配所有具有attr属性的元素，不考虑它的值<br>
[attr=val] 匹配所有attr属性等于“val”的元素<br>
[attr~=val] 匹配所有attr属性具有多个空格分隔的值,其中一个值等于“val”的元素<br>
- 伪类选择器
:first-child 匹配元素的第一个子元素<br>
:link 匹配所有未被点击的链接<br>
:visited 匹配所有已被点击的链接<br>
:active 匹配鼠标已经其上按下、还没有释放的元素<br>
:hover 匹配鼠标悬停其上的元素<br>
:disabled 匹配表单中禁用的元素<br>
:checked 匹配表单中被选中的radio或checkbox元素<br>
- 伪元素选择器
::first-leter 匹配元素内容的第一个字母<br>
:before, ::before 为当前元素创建一个子元素作为伪元素。常通过 content 属性来为一个元素添加修饰性的内容。 此元素默认为行内元素<br>
#### CSS样式权重优先级与计算
important > 内嵌样式 > ID > 类 > 标签 | 伪类 | 属性选择 > 伪对象 > 继承 > 通配符
第一等：代表内联样式，如: style=””，权值为1000。
第二等：代表ID选择器，如：#content，权值为100。
第三等：代表类，伪类和属性选择器，如.content，权值为10。
第四等：代表类型选择器和伪元素选择器，如div p，权值为1。
参考 https://www.cnblogs.com/damingge/p/6498813.html
### 2.a标签全部作用
- 超链接
<a>标签的target属性大致有这几种：

 _self _blank _parent _top
<a href="https://www.baidu.com/" target="_blank">超链接</a>在一个新的窗口打开连接相应的网页。

- 锚点

  ```js
<div id="runtop"></div>
通过<a href="#runtop">返回顶部</a>能够实现一个常见的返回顶部的功能。<br>
- 打电话或者发邮件
<a href="tel:123456">打电话给号码为123456的人</a>
<a href="mailto:123456@789.com">发邮件给给号码为123456@789.com的人</a><br>
   ```
- 协议限定符
 <a href="javascript:alert("强制运行的javascript代码")">这样就能够在<a>标签被点击的时候强制运行href属性里面的代码</a>
 ### 3.用CSS画三角形
 
- 利用元素的border是由三角形组合而成
 ```js
   div {
       width: 0px;
       height: 0px;
       border: 40px solid;//高40px
       border-color: transparent transparent red transparent;
   }
  ```
 参考 https://www.jianshu.com/p/9a463d50e441
 
 ### 4.未知宽高元素水平垂直居中（方案及比较）
 - 思路：显示设置父元素为：table，子元素为：cell-table，这样就可以使用vertical-align: center，实现水平居中
优点：父元素（parent）可以动态的改变高度（table元素的特性）
缺点：IE8以下不支持
 ```html
<head>
    <meta charset="UTF-8">
    <title>未知宽高元素水平垂直居中</title>
    <style>
        .parent1{
        display: table;
        height:300px;
        width: 300px;
        background-color: #FD0C70;
    }
    .parent1 .child{
        display: table-cell;
        vertical-align: middle;
        text-align: center;
        color: #fff;
        font-size: 16px;
    }</style>
</head>
<body>
<div class="parent1">
    <div class="child">hello world-1</div>
</div>
</body>
 ```
 ...以后补充
 参考：https://www.cnblogs.com/jogen/p/5213566.html
 
 ### 5.元素种类的划分
 CSS中，html中的标签元素大体被分为三种不同的类型：
 - 常用的块状元素有：
  ```html
<div>、<p>、<h1>...<h6>、<ol>、<ul>、<dl>、<table>、<address>、<blockquote> 、<form>
  ```
 - 常用的内联元素(行内元素)有：
  ```html
<a>、<span>、<br>、<i>、<em>、<strong>、<label>、<q>、<var>、<cite>、<code>
  ```
 - 常用的内联块状元素有:
<img>、<input>
 <br>
 参考： https://blog.csdn.net/underoses/article/details/88770840
 
 ### 6.盒子模型及其理解
 html文档中的每个元素都被描绘成矩形盒子，这些矩形盒子通过一个模型来描述其占用空间，这个模型称为盒模型。盒模型通过四个边界来描述：margin（外边距），border（边框），padding（内边距），content（内容区域）<br>
 参考：https://www.cnblogs.com/sichaoyun/p/6761341.html
 
 ### 7.定位方式及其区别（文档流）
 - 文档流（普通流【normal flow】）
 符合HTML中标签本身含义，遵循自上而下，从左至右的布局。
 - 文本流
 文档对一系列字符的读取和输出的顺序，和文档流一样自上而下，从左至右排列。
 -定位方式
 1.文档流：又包含三种类型：①块级元素，②行内元素，③相对定位（position：relative）
 2.浮动（float）
  有一个元素A（图片中黑色背景元素），利用float脱离文档流的时候，其他的盒子元素会无视元素A所占空间，但是其他元素中的文字却不
会无视元素A，依然会为A让出位置，环绕在其周围。这时候就说元素A脱离了文档流，但是没有脱离文本流。
 3.绝对定位absolute,fixed
浮动（float）布局会使元素脱离文档流，不脱离文本流。元素无视它的存在，而元素其中的文本会围绕在它周围，但是它不会脱离DOM树，用浏览器的审查元素可以看到脱离文档流的它。
绝对定位position: absolute;和position: fixed;布局会使元素既脱离文档流，又脱离文本流。（元素和文本都定位不到它的存在）。<br>
参考: https://blog.csdn.net/thisequalthis/article/details/96020597

### 8.margin塌陷及合并问题
margin塌陷问题<br>
在文档流中，父元素的高度默认是被子元素撑开的
也就是说 子元素有多高，父元素就有多高
但是当子元素设置浮动之后，子元素会完全脱离文档流
此时将会导致子元素无法撑开父元素的高度，导致父元素高度塌陷
- 触发（开启）BFC属性(Block Formatting Content块级格式化上下文简称BFC)
满足下面任一条件即可<br>
 ```html
浮动元素   float属性值为除了none以外的值<br>
绝对定位元素 position 为 absolute、fixed<br>
display 为inline-blocks,table-cells,table-captions<br>
overflow 为 hidden,auto,scroll<br>
 ```
bfc的三个特性：<br>
a.阻止外边距折叠<br>
b.可以包含浮动的元素<br>
c.可以阻止元素被浮动元素覆盖 <br>
- 给父级元素添加一个边框，就可以解决；如果不希望看到边框，可以将边框的颜色设成背景色即可。
margin合并问题<br>
处于上下位置关系的两个div容器，在通过margin-top、margin-bottom改变间距时，如果两个属性的值相同时，则两容器间的距离就是这个值；如果两个属性的值不同，则取较大值作为两容器间的距离；<br>
也存在着解决方法，那就是在两容器外都套上相同容器（class/id相同的），并在容器中设定overflow：hidden
 
 ### 9.浮动模型及清除浮动的方法
 浮动可以使元素向左或向右偏移，会给每个元素产生一个块级元素框，直到这个块级框遇到边界框或者另一个元素的边框。且浮动使得元素脱离文档流，后面的元素会直接在其原来的位置上进行定位<br>
 使元素脱离文档流<br>
 清除浮动：<br>
 - clear
 clear: both 清除两侧浮动带来的影响
 
 参考： http://www.360doc.com/content/19/0924/17/66228184_862966414.shtml
 
 
 ### 10.display定位属性
 这个属性用于定义建立布局时元素生成的显示框类型<br>
 display: none 隐藏不占网页空间<br>
 display: block 将目的元素转为块级元素，span原本是行内元素，设置宽高是没有效果的，只有转化为块才有效果<br>
 display: inline 将目的元素转为行内元素，设置宽高是没有效果的，<br>
 display: inline-block 设置成行内块元素,既有行元素特性又有块元素特性<br>
 
 ### 11.CSS定位属性
 参考：https://www.cnblogs.com/qianguyihao/p/8296748.html
 
 ### 12.IFC与BFC
- BFC属性(Block Formatting Content块级格式化上下文简称BFC)

参考： https://blog.csdn.net/mevicky/article/details/47008939

 ### 13.圣杯布局和双飞翼布局的实现
 
 ### 14.Flex布局
 ### 15.px、em、rem的区别
 用于设置字体的大小以及盒子的宽高，但是px不会因为浏览器尺寸的改变而改变，而em和rem会因为浏览器尺寸的变化而变化<br>
 - px pixel的缩写 像素 像素是相对于显示器屏幕分辨率而言的
 - em是一个相对长度的的单位，是相对于当前对象内文本的字体尺寸。如过我们未设置当前文本的字体尺寸，那么em就会相对于浏览器的默认字体尺寸
 在浏览器中默认字体尺寸为16px，换句话说1em=16px,一般我们在写自适应布局时经常会用到em为单位。通过在CSS中的body选择器中设置font-size值来简化代码，使得页面中所有的em都相对于body值。
 参考： https://zhidao.baidu.com/question/553998626685304812.html
 
 ### 16.Less预处理语言
 Less 是一门 CSS 预处理语言，它扩充了 CSS 语言，增加了诸如变量、混合（mixin）、函数等功能，让 CSS 更易维护、方便制作主题、扩充。Less 可以运行在 Node 或浏览器端。
 
 ### 17.媒体查询
 
 ### 18.css3自适应布局单位vw,vh
 
 ### 19.H5的语义化作用及语义化标签
 #### 语义化
 标签有了自己的含义，通过标签就能判断内容语义
 #### 好处
 - html结构清晰，代码可读性好，易于团队维护和开发
 - 更有利于搜索引擎或辅助设备理解html页面内容
 #### H5常用的语义化标签
 ```html
 - <section>用于对网站和页面内容分块，划分单独的模块区域
 - <article>独立的文章展示
 - <aside>页面中的附属侧边信息
 - <header>：定义页面或内容的头部区域
 - <footer>：定义页面或内容的底部区域
 - <nav>：定义页面导航
 - <figure>表示一个独立的内容
 - <figcaption>表示<figure>的标题（必须写在<figure>的内部，一般放在<figure>的第一位或者最后一位，最多只有一个）
 - <main>表示页面的主体内容（一个页面只能使用一次） 
 - <hgroup>表示对网页或区段的标题进行组合，通常对h1~h6进行分组 
 - <time>：定义日期和时间
 - <mark>用来突出显示文本,默认情况下背景为黄色 
 - <dialog>类似于微信对化框（默认display：none 加open才显示 ，有默认定位和默认边框）
 - <embed>标记定义外部的可交互的内容和插件
 - <progress></progress>代表一个任务完成的进度
  ```
 参考：https://www.cnblogs.com/dzh-123/p/12388430.html
 
