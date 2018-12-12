## class
v-bind:class:   如果在组件里使用，会和之前的class 叠加在一起
* 可以绑定一个计算属性
* 可以绑定一个对象 v-bind:class="{ active: isActive, 'text-danger': hasError }">
* 数组语法  v-bind:class="[activeClass, errorClass]"    
三元表达式 v-bind:class="[isActive ? activeClass : '', errorClass]"   

##  绑定内联样式
* 属性名这个和React内联一样，用驼峰再加上短横线
* 可以直接绑定一个对象
* 绑定数组语法  v-bind:style="[baseStyles, overridingStyles]"
* 自动添加前缀
