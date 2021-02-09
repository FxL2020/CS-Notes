### Vue性能优化

#### Vue 代码层面的优化

1.1、v-if 和 v-show 区分使用场景
v-if与v-show都可以动态控制dom元素显示隐藏，v-if显示隐藏是将dom元素整个添加或删除，而v-show隐藏则是为该元素添加css--display:none，dom元素还在。<br>

应用场景： v-if 适用于在运行时很少改变条件，不需要频繁切换条件的场景；v-show 则适用于需要非常频繁切换条件的场景。<br>
