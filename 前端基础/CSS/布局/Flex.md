### Flex
移动端使用广泛，pc端浏览器端支持较差<br>
flexible弹性布局：用来为盒状模型提供最大的灵活性，任何一个容器都能指定为flex布局<br>
为父盒子模型设置为flex布局后，子元素的float,clear和vertical-align属性都将失效<br>
<br>
#### flex布局原理：通过给父盒子添加flex属性，来控制子盒子的位置和排列方式
#### 父项常见属性
flex-direction: 设置主轴的方向<br>
justify-content: 设置主轴上的子元素排列方式<br>
flex-wrap: 设置子元素是否换行<br>
align-content: 设置侧轴上的子元素的排列方式(多行)<br>
align-items: 设置侧轴上的子元素的排列方式(单行)<br>
flex-flow: 复合属性，相当于同时设置了flex-direction和flex-wrap<br>
<br>
主轴和侧轴<br>
默认主轴x方向，水平向右<br>
侧轴y方向，垂直向下<br>
元素跟着主轴来排列
<br>
flex-direction: 设置主轴的方向<br>
属性<br>
row: 默认从左到右<br>
roe-reverse: 从右到左<br>
column: 从上到下<br>
column-reverse: 从下到上<br>
<br>
justify-content: 设置主轴上的子元素排列方式<br>
属性<br>
flex-start：默认从左到右排序，左对齐<br>
flex-end：右对齐<br>
center：居中对齐<br>
space-around：平分剩余空间<br>
space-between：先两边贴边，然后平分剩余空间<br>
<br>
flex-wrap: 设置子元素是否换行<br>
属性<br>
flex布局中默认是不换行的，如果放不开会缩小子元素的宽度<br>
默认:nowrap 不换行<br>
wrap 换行<br>
<br>
align-items: 设置侧轴上的子元素的排列方式(单行)<br>
属性<br>
flex-start：默认，上对齐<br>
flex-end：下对齐<br>
center：居中对齐<br>
srtetch: 拉伸但是子盒子不要给高度<br>
<br>
align-content: 设置侧轴上的子元素的排列方式(多行)<br>
子项目出现换行
flex-start：<br>
flex-end：<br>
center：居中对齐<br>
space-around：平分剩余空间<br>
space-between：先两边贴边，然后平分剩余空间<br>
<br>
flex-flow: 复合属性，相当于同时设置了flex-direction和flex-wrap<br>
flex-flow: column wrap;//设置y为主轴，换行
#### 子项常见属性
属性<br>

