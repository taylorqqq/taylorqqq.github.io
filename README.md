## Vue 相关面试题

文档地址
https://xieerduos.github.io
11
https://ffffee.com (国内访问)

需要加微信群技术交流群的
艾特群管理发二维码
微信群回复更快更及时

- Vue 和 React 有什么区别？
- Vue 是如何实现数据双向绑定的？
- Vue 组件中的 props 和 data 有什么区别？
- Vue 的路由是如何实现的？
- Vue 中如何使用过滤器？
- Vue 的生命周期是什么？
- Vue 中的 computed 属性是什么？
- Vue 中的 watch 和 computed 有什么区别？
- Vue 中如何实现组件间的通信？
- Vue 中的 $emit 和 $on 有什么用？
- Vue 中的 v-bind 和 v-model 有什么区别？
- Vue 中的 v-if 和 v-show 有什么区别？
- Vue 中的 v-for 和 v-if 有什么区别？
- Vue 中的 v-bind:class 和 v-bind:style 有什么区别？
- Vue 中如何实现动态组件？
- Vue 中的 slot 是什么？
- Vue 中如何实现组件的异步加载？
- Vue 中如何使用自定义指令？
- Vue 中如何使用自定义过滤器？
- Vue 中如何使用自定义插件？
- Vue 中如何使用自定义混入？
- Vue 中如何使用自定义指令和过滤器？
- Vue 中的 v-pre, v-once 和 v-cloak 有什么用？
- Vue 中的 $nextTick 方法是干什么用的？
- Vue 中的 $set 和 $delete 方法是干什么用的？
- Vue 中的 $refs 属性是什么？
- Vue 中的 $attrs 和 $listeners 有什么用？
- Vue 中的 $parent 和 $children 有什么用？
- Vue 中的 $options 属性是什么？
- Vue 中的 $root 属性是什么？
- Vue 中的 $isServer 属性是什么？
- Vue 中如何实现动态组件的加载和卸载？
- Vue 中如何使用 $forceUpdate 方法？
- Vue 中如何使用 $destroy 方法？
- Vue 中如何使用 $mount 方法？
- Vue 中如何使用 $nextTick 方法？
- Vue 中如何使用 $watch, $watchGroup 和 $unwatch 方法？

### 1. Vue 和 React 有什么区别？

```js
主要区别有：
1.设计理念：Vue.js 更注重简单易用，提供了较为完整的解决方案，而 React 更注重灵活性和可扩展性。
2.数据绑定：Vue.js 使用双向数据绑定，而 React 使用单向数据流。
3.组件化：Vue.js 和 React 都支持组件化开发，但 Vue.js 的组件通信方式更简单易用。
4.性能：React 使用 Virtual DOM 可以提高性能，而 Vue.js 也有相应的优化手段。

总的来说，Vue.js 和 React 都是优秀的 JavaScript 框架，适用于不同场景。要根据项目特点和个人喜好来选择使用哪一种框架。

```

### 2. Vue 是如何实现数据双向绑定的？

```js
1.Vue 通过 Object.defineProperty 函数在 JavaScript 原型链上劫持了对象属性的 getter 和 setter 函数来实现数据双向绑定。
2.在 Vue 初始化的时候，会遍历 data 对象上的所有属性，对每一个属性都使用 Object.defineProperty 函数重新定义 getter 和 setter 函数。
3.在 getter 函数中，会触发依赖收集，把当前组件中用到该属性的 Watcher 加入到该属性的依赖列表中。在 setter 函数中，会触发更新，把该属性的依赖列表中的 Watcher 更新。
4.这样当数据变化时，会触发 setter 函数，而 setter 函数中又会触发相应的更新，实现了数据双向绑定。同时当页面上的某些元素发生变化时，会触发 getter 函数，实现了页面元素和数据的双向绑定。

具体来说，Vue 利用了观察者模式来实现数据的双向绑定，在 Vue 的实例中会有一个 observer 对象来观察数据的变化，并且在每个 Vue 的组件实例中会有一个 watcher 对象来监听 observer 数据的变化，实现了双向绑定。
```

### 3. Vue 组件中的 props 和 data 有什么区别？

```js
1.用途不同: props 是从父组件传递给子组件的数据，它只能在组件的 template 中使用，不能在组件内部进行修改。data 是组件内部私有数据，组件内部可以随意修改。
2.赋值方式不同:props 是在父组件中通过特定语法进行赋值的,而 data 是在组件内部通过定义一个 data 函数返回一个对象来定义的.
3.类型限制不同: props 可以接受任意类型的值，并且可以对 props 设置验证规则，检测传入的值是否符合预期。而 data 只能是对象或函数返回对象。

总的来说，Vue, props 是从父组件传入的数据，是只读的，不能在组件内部进行修改。而 data 是组件内部的私有数据，可以随意修改。

```

### 4. Vue 的路由是如何实现的？

```js
Vue 的路由是通过 Vue Router 这个插件实现的。Vue Router 为 Vue.js 应用程序提供了路由功能，允许开发者在应用程序中定义不同的 URL 路径和组件之间的映射关系。

主要流程如下：
1.安装 Vue Router
2.在 main.js 中引入 Vue Router 并配置
3.定义路由规则，映射路径和组件
4.使用 router-link 和 router-view 标签实现导航

```

### 5. Vue 中如何使用过滤器？

```js
Vue 中可以使用过滤器（filters）来对渲染出来的数据进行过滤和格式化。
过滤器可以在模板中使用，也可以在 Vue 实例中全局注册。
过滤器是有性能损耗的，所以应该尽量避免使用过多的过滤器，或者使用计算属性来替代。
```

```js
在模板中使用过滤器：
<div>{{ message | capitalize }}</div>
过滤器可以链式调用，使用方法如下：
<div>{{ message | filterA | filterB }}</div>
注意：过滤器的参数可以通过冒号来传递，如
<div>{{ message | filterA(arg1, arg2) }}</div>
```

```js
在 Vue 实例中全局注册过滤器：
Vue.filter('capitalize', function (value) {
  if (!value) return ''
  value = value.toString()
  return value.charAt(0).toUpperCase() + value.slice(1)
})
```

```js
在 Vue 实例中局部注册过滤器：
new Vue({
  filters: {
    capitalize: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  }
})

```
