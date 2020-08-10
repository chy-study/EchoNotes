---
title: Vue 笔记
date: 2020-07-28 22:03:31
categories:
- 笔记
tags:
- vue
---
Vue是近年很流行的前端开发框架...
<!--more-->

#### 指令:
- 指令带有前缀v-,职责是当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM
- v-bind: 绑定数据和元素的属性,例如 ` v-bind:title="" `, `v-bind:class=""（class和style的绑定）`，缩写为 `:title=""`, `:class=""`
- 条件与循环： v-if 和 v-for
- 事件监听： v-on，例如 v-on:click=""，缩写为 @click=""
- 双向绑定： v-model，例如 v-model=""
- 条件渲染： v-if, v-else-if, v-else, v-show
- v-else-if 和 v-else 必须紧跟在 v-if 或者 v-else-if 后面。否则它将不会被识别
- 不推荐同时使用 v-if 和 v-for,当 v-if 与 v-for 一起使用时，v-for 具有比 v-if 更高的优先级.
- v-if 和 v-show 的比较：
   - v-show 不支持 \<template> 元素，也不支持 v-else。
   	- v-if 是“真正”的条件渲染，它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。如果在初始渲染时条件为假，则什么也不做,——直到条件第一次变为真时，才会开始渲染条件块
   	- v-show不管初始条件是什么，元素总是会被渲染，并且只是基于 CSS 进行切换,切换元素的 CSS property display，元素始终会被渲染并保留在 DOM 中
   	- 一般来说，v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好.
- 用key管理可复用的元素： Vue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染。如果不需要复用，只需要在元素上添加一个具有唯一值的 key attribute 即可。请用字符串或数值类型的值作为key
- 列表渲染： v-for，语法格式 item in items，也可以用 of 代替 in 作为分隔符，items是源数据，item是被迭代的元素的别名。建议尽可能在使用 v-for 时提供 key attribute
   - 遍历数组: v-for="(item, index) in items"， item: property， index: 当前项的索引
   - 遍历对象: v-for="(value,name,index) in object", value: property, name: property名称(键名), index: 索引
- 事件修饰符： Vue.js 为 v-on 提供了事件修饰符，修饰符是由点开头的指令后缀来表示的。修饰符可以串联，使用时顺序很重要
   - .stop
   - .prevent
   - .capture
   - .self
   - .once
   - .passive
- 按键修饰符： 监听键盘事件，v-on:keyup.page-down=" "， @keyup.enter=" " （可能需要加上 .native）
- .exact修饰符： 控制精确的系统修饰符组合触发的事件。
- 鼠标按钮修饰符： @click.left=""， @click.right=""， @click.middle=""
- 表单输入绑定修饰符：
   - v-model.lazy=""，在默认情况下，v-model在每次input事件触发后将输入框的值与数据进行同步，这时可以添加lazy修饰符，从而转为在change事件之后进行同步
   - v-model.number=""，自动将用户的输入值转为数值类型
   - v-model.trim=""，自动过滤用户输入的首尾空白字符
- Vue暴露出了一些有用的实例property和方法，它们都有前缀$，以便与用户定义的property区分开。 例如： vm.$data, vm.$watch()
- 计算属性：computed，计算属性是基于它们的响应式依赖进行缓存的，只在相关响应式依赖发生改变时它们才会重新求值,大多数情况下更合适
- 侦听属性：watch，当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的
- **在 JavaScript中，truthy（真值）指的是在布尔值上下文中，转换后的值为真的值。所有值都是真值，除非它们被定义为 假值（即除 false、0、""、null、undefined 和 NaN 以外皆为真值）。JavaScript 在布尔值上下文中使用强制类型转换（coercion）。**
- ref：
   - 用来给DOM元素或子组件注册引用信息。引用信息会根据父组件的 $refs 对象进行注册。如果在普通的DOM元素上使用，引用信息就是元素; 如果用在子组件上，引用信息就是组件实例
   - 只要想要在Vue中直接操作DOM元素，就必须用ref属性进行注册
   - 例如要在create的时候引用DOM元素，先在DOM中使用ref标签进行注册，然后便可以通过’this.$refs’再跟注册时的名称来引用DOM元素了

***

#### 组件基础：
- 组件是可复用的Vue实例，并且带有一个名字
- 组件的data选项必须是一个函数，不能直接提供一个对象
- 自定义的组件必须先注册，Vue才能够识别并在模板中使用，组件的注册方式有**全局注册**和**局部注册**
- 通过prop向子组件传递数据
- 监听子组件事件
   - 父级组件可以像处理 native DOM 事件一样通过 v-on 监听子组件实例的任意事件
   - 子组件可以通过调用 $emit 方法并传入事件名称来触发一个事件
- 子组件使用事件抛出一个值
   - 子组件使用 $emit 方法的第二个参数来提供这个值
   - 在父级组件监听这个事件的时候，可以：
      - 通过 $event 直接访问到被抛出的这个值
      - 或者，如果父级组件对这个事件的处理函数是一个方法，那么这个值将会作为第一个参数传入这个方法
- 通过插槽分发内容：\<slot>