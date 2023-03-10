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

### 4. Vue 组件中的 watch 和 computed 有什么区别？

```js
1.用途不同: watch 是监听某个数据的变化，当数据发生变化时，执行相应的操作。computed 是计算属性，当某个数据发生变化时，会自动计算出新的值。
2.缓存不同: watch 是不缓存的，每次数据变化都会执行相应的操作。computed 是缓存的，只有当依赖的数据发生变化时，才会重新计算。
3.执行时机不同: watch 是数据发生变化时，执行相应的操作。computed 是在使用到计算属性的时候，才会计算。
```

```js
watch: {
  'user.name': function (newName, oldName) {
    console.log(`user.name 从 ${oldName} 变为 ${newName}`);
  }
}
```

```js
computed: {
  fullName: function () {
    return this.firstName + ' ' + this.lastName;
  }
}
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

### 6. Vue 的路由是如何实现的？

```js
Vue 的路由是通过 Vue Router 这个插件实现的。Vue Router 为 Vue.js 应用程序提供了路由功能，允许开发者在应用程序中定义不同的 URL 路径和组件之间的映射关系。

主要流程如下：
1.安装 Vue Router
2.在 main.js 中引入 Vue Router 并配置
3.定义路由规则，映射路径和组件
4.使用 router-link 和 router-view 标签实现导航
```

### 7. Vue 中如何实现组件间的通信？

```js
1.使用 props 和 events：父组件可以通过 props 向子组件传递数据，子组件可以通过 $emit 方法向父组件发送事件，
父组件可以通过 v-on 监听子组件发出的事件。
2.使用 Vuex：Vuex 是 Vue 官方提供的一个状态管理库，可以帮助我们统一管理组件之间的状态，从而实现组件间的通信。
3.使用 Event Bus：Vue 中可以通过创建一个 Event Bus 的方式，来实现组件间的通信。Event Bus 是一个 Vue 实例，
可以在任意组件中监听和发送事件。
4.使用 provide/inject：Vue 2.3.0+ 中新增的 provide 和 inject 方法，可以帮助我们实现组件间的通信，
它比 props 和 events 更加灵活。
5.使用 $attrs 和 $listeners：Vue 2.4.0+ 中新增的 $attrs 和 $listeners 属性，可以帮助我们实现组件间的通信。
$attrs 属性可以接收父组件传递给子组件的所有未被该组件定义的属性。这些属性将被添加到子组件的根元素上。
$listeners 属性可以接收父组件传递给子组件的所有事件监听器。这些监听器将被绑定到子组件的根元素上。
通常，在父组件中使用 v-bind 或者在子组件中使用 $attrs 和 $listeners 可以实现组件间的通信。
6.使用 $parent 和 $children：Vue 中的每个组件都有一个 $parent 属性，指向父组件，也有一个 $children 属性，指向子组件。
注意：$parent 和 $children 属性不应该被频繁使用，因为它们会依赖组件的层级结构，如果组件的层级结构发生变化，那么它们的结果也会发生变化。
```

### 8. Vue 中的 $emit 和 $on 有什么用？

```js
1.$emit 是 Vue 实例的一个方法，用于触发当前实例上的事件。参数是：事件名，以及传递给事件处理函数的参数。
2.$on 是 Vue 实例的一个方法，用于监听当前实例上的自定义事件。参数是：事件名，以及事件触发时的回调函数。

总结：
用 $emit 方法在子组件中触发事件，然后在父组件中用 $on 方法监听子组件发出的事件。
```

```js
// 子组件
this.$emit("customEvent", value);
```

```js
// 父组件
<child-component v-on:customEvent="handleEvent"></child-component>
// ...
methods: {
  handleEvent: function(value) {
      // do something with value
  }
}
```

### 9. Vue 中的 v-bind 和 v-model 有什么区别？

```js
1.v-bind 和 v-model 都是 Vue 提供的指令，用于绑定数据到 DOM 元素上。
2.v-bind 是 Vue 提供的用来动态绑定一个或多个属性到一个元素上的指令。
它的语法是 v-bind:<属性名>，例如：v-bind:src，用来绑定图片的 src 属性到一个元素上。

v-model 是 Vue 提供的用来实现双向数据绑定的指令。
它的语法是 v-model，例如：v-model="message"，用来绑定输入框的 value 和 message 变量。
当使用 v-bind 时，需要手动更新数据到 DOM 元素上，而 v-model 可以自动实现双向绑定。

总结：
v-bind 是用来绑定属性和值，只能用于单向绑定
v-model 是用来实现双向数据绑定，它内部实际上是通过 v-bind 和 v-on 来实现的。
```

### 10. Vue 中的 v-if 和 v-show 有什么区别？

```js
1.v-if 是条件渲染指令，它会根据表达式的值来渲染或不渲染一个元素。
当表达式的值为 true 时，元素会被渲染；当表达式的值为 false 时，元素会被销毁。
2.v-show 也是条件渲染指令，它会根据表达式的值来在 DOM 中添加或删除 CSS 属性 display: none 来控制元素的显示与隐藏
当表达式的值为 true 时，元素会显示；当表达式的值为 false 时，元素会隐藏。

总结：
v-if 是条件渲染，会根据表达式的值来渲染或销毁元素
v-show 是条件显示，会根据表达式的值来显示或隐藏元素，不会对元素进行销毁或重建
当需要频繁切换显示/隐藏时建议使用 v-show，因为它不需要销毁重建元素，更加高效。
```

### 11. Vue 中的 v-for 和 v-if 有什么区别？

```js
1.v-for 是循环渲染指令，它会根据一个数组或对象来渲染多个相同的元素或组件，它常用于渲染列表或表格中的数据。
2.v-if 是条件渲染指令，它会根据表达式的值来渲染或不渲染一个元素。

在 Vue 2 中，v-for 指令的优先级高于 v-if 指令。
当 v-for 和 v-if 同时出现在同一元素上时，Vue 会先处理 v-for 指令。这意味着，当 v-for 和 v-if 一起使用时，v-if 将会在 v-for 生成的每一个元素上进行判断。
如果你希望 v-if 先于 v-for 来判断是否渲染元素，你可以将 v-if 指令放在一个单独的元素上，并在这个元素上使用 v-for 指令。
如果你希望在v-if 条件不成立时不渲染 v-for 渲染出来的元素，你可以使用 template 标签来包裹 v-for 元素。

在 Vue 3 中，v-for 指令的优先级低于 v-if 指令。可以在同一元素上同时使用 v-for 和 v-if 指令。
```

### 12. Vue 中的 v-bind:class 和 v-bind:style 有什么区别？

```js
v-bind:class 和 v-bind:style 是 Vue 中的指令，用于动态绑定元素的 class 和 style。
v-bind:class 用于动态绑定元素的 class，它可以接受一个对象、字符串或表达式作为参数。当表达式的值为 true 时，对应的 class 就会被加上，否则就会被移除。
v-bind:style 用于动态绑定元素的 style，它可以接受一个对象、字符串或表达式作为参数。对象的 key 是样式的名称，value 是对应的值。
```

```js
<div v-bind:class="{ active: isActive }"></div>
<div v-bind:style="{ color: color, fontSize: fontSize + 'px' }"></div>
当 isActive 为 true 时，元素会被添加 active 类，否则不会。
而 v-bind:style 会根据 color和fontSize的值来对对应的样式进行赋值。

总结：
v-bind:class 用于绑定 class，v-bind:style 用于绑定 style。
```

### 13. Vue 中如何实现动态组件？

```js
Vue 中可以使用 v-bind 指令和 component 属性来实现动态组件。
通过设置 v-bind:is 或者 :is 属性来改变当前组件，这样就可以在不同条件下渲染不同的组件。
```

```js
<component v-bind:is="currentComponent"></component>

可以动态地改变 currentComponent 的值来改变当前渲染的组件。
this.currentComponent = 'ComponentA'
```

### 14. Vue 中的 slot 是什么？

```js
Vue 中的 slot 是用来在组件中插入其它内容的一种方式。通过使用 slot 指令，可以在父组件中定义一个插槽，在子组件中使用 slot 指令来插入内容。
共分为三类：
1.默认插槽：父组件在使用子组件时，可以在子组件标签内部放置内容，这些内容会放入默认插槽中。
2.具名插槽：子组件可以在 template 中定义多个插槽，并为每个插槽指定名称。父组件在使用子组件时，
可以通过 v-slot 指令指定内容放入哪个具名插槽中。
3.作用域插槽：在 Vue2 中需要使用 scoped-slots 这个插件来实现，在 Vue3 中可以直接使用。
作用域插槽是一种特殊类型的具名插槽，它可以把子组件中的数据传递给父组件。
```

```js
// 默认插槽
<template>
  <div>
    <h1>这是父组件</h1>
    <slot>默认插槽内容</slot>
  </div>
</template>

<template>
  <parent-component>
    <p>这是子组件，将会被放入默认插槽中</p>
  </parent-component>
</template>

```

```js
// 具名插槽
<template>
  <div>
    <h1>这是父组件</h1>
    <slot name="header"></slot>
    <slot name="body"></slot>
    <slot name="footer"></slot>
  </div>
</template>

<template>
  <parent-component>
    <template v-slot:header>
      <h1>这是头部</h1>
    </template>
    {/* <h1 slot="header">这是头部</h1> 这种写法也可以 */}
    <template v-slot:body>
      <p>这是主体</p>
    </template>
    <template v-slot:footer>
      <p>这是尾部</p>
    </template>
  </parent-component>
</template>
```

```js
// 作用域插槽
<template>
  <div>
    <h1>这是父组件</h1>
    <slot :item="item" v-for="item in items"></slot>
  </div>
</template>

<template>
  <parent-component :items="items">
    <template v-slot="{item}">
      <p>{{item.name}}</p>
    </template>
  </parent-component>
</template>
```

```js
总结：
默认插槽和具名插槽的用法都很相似，而作用域插槽可以让子组件获取父组件传递过来的数据。
```

### 15. Vue 中如何实现组件的异步加载？

```js
Vue 中可以使用 dynamic imports 来实现组件的异步加载。dynamic imports 是 ECMAScript 的一个新特性，可以在运行时加载模块。
在 Vue 中，可以使用 Vue Router 的 lazy-loading 或者 vue-cli 的 code splitting 等技术来实现组件的异步加载。
```

```js
const AsyncComponent = () => ({
  component: import("./AsyncComponent.vue"),
  loading: Loading,
  error: Error,
  delay: 200,
  timeout: 3000,
});

AsyncComponent 是一个函数，返回一个对象，对象中包含了一个异步加载的组件。当这个组件被加载时，会显示 Loading 组件。
如果加载失败，会显示 Error 组件。
```

### 16. Vue 中如何使用自定义指令？

```js
在 Vue 中使用自定义指令，需要在 Vue 实例的 directives 配置项中注册一个指令。

// 首先，在 Vue 实例的 directives 配置项中注册自定义指令。
Vue.directive("my-directive", {
  bind(el, binding, vnode) {
    //在指令第一次绑定到元素上时调用
  },
  inserted(el, binding, vnode) {
    //在元素插入到父节点时调用
  },
  update(el, binding, vnode) {
    //在元素更新时调用
  },
  unbind(el, binding, vnode) {
    //在元素解绑时调用
  }
});

// 然后，在 template 中使用指令
<div v-my-directive="someValue"></div>

someValue 将会传递给指令的 bind 函数作为第二个参数（binding）。
```

### 17. Vue 中如何使用自定义插件？

```js
定义一个 JavaScript 对象，该对象包含插件的选项和需要执行的函数。
在 Vue 实例中使用 Vue.use() 方法来安装插件。

// 定义插件
var MyPlugin = {
  install: function (Vue, options) {
    // 为 Vue 添加一个自定义方法
    Vue.prototype.$myMethod = function () {
      console.log('Hello from my plugin!')
    }
  }
}
// 使用插件
Vue.use(MyPlugin)
// 在组件中使用插件
new Vue({
  methods: {
    myMethod: function () {
      this.$myMethod()
    }
  }
})
```

### 18. Vue 中如何使用自定义混入？

```js
Vue 中使用自定义混入可以通过全局方法 Vue.mixin() 或者局部方法 mixins 选项来实现。

// 全局混入
Vue.mixin({
  created: function () {
    console.log('Global Mixin - Created Hook')
  }
})

// 局部混入
var myMixin = {
  created: function () {
    console.log('Local Mixin - Created Hook')
  }
}

new Vue({
  mixins: [myMixin],
  created: function () {
    console.log('Vue Instance - Created Hook')
  }
})
局部混入会在 Vue 实例的 created 钩子之前调用。如果混入对象和 Vue 实例对象中定义了同样的钩子函数，混入对象中的函数会先执行。

总结：
自定义混入可以用来将一些公共逻辑和行为混合到多个组件中，这样可以避免重复代码和维护问题。
```

### 19. Vue 中 mixin 与 hooks 的异同点

```js
Mixin 和 Hooks 都是 Vue 中用来在组件之间共享代码的一种方式。

1.Mixin 是全局混入，可以在多个组件中使用同一个 mixin。它可以添加组件的 data、methods、created、mounted 等钩子函数。Mixin 中的代码会在组件实例化之前合并到组件中，如果有相同的选项，则组件中的选项会覆盖 mixin 中的选项。

2.Hooks 是局部混入，只能在当前组件中使用，并且不能添加组件的选项，只能扩展组件的行为。Hooks 可以在组件的生命周期钩子函数中使用，用来在不改变组件选项的情况下，扩展组件的行为。

总结来说 Mixin 是全局混入，可以在多个组件中使用, Hooks 是局部混入，只能在当前组件中使用。
```

### 20. Vue 中的 v-pre, v-once 和 v-cloak 有什么用？

```js
1.v-pre 指令会跳过这个元素和它的子元素的编译过程。这可以用来显示原始 Mustache 标签，或者在您有自定义指令的场景下，跳过自定义指令的编译。
2.v-once 指令只渲染元素和组件一次。随后的重新渲染，元素/组件及其所有的子节点将被视为静态内容并跳过。
3.v-cloak 指令会在元素被编译和渲染后被移除，可以用来隐藏未编译完成时出现的闪烁。常用于样式，如 v-cloak="{display: none}"。
```

### 21. Vue 中的 $nextTick 方法是干什么用的？

```js
Vue 中的 $nextTick 方法可以在下次 DOM 更新循环结束之后执行回调函数。
这意味着所有数据绑定和事件监听器在回调函数执行之前已经完成更新。这对于在数据变化之后立即使用更新后的 DOM 状态很有用。
这个方法通常用于在数据变化之后立即执行某些操作，例如计算高度、定位、或者在组件中进行其他操作。
```

### 22. Vue 中的 $set 和 $delete 方法是干什么用的？

```js
1.$set 方法是 Vue.set 方法的别名，用来向响应式对象中添加新的属性或者修改现有属性的值。它能触发视图的更新。
2.$delete 方法是 Vue.delete 方法的别名，用来从响应式对象中删除一个属性。它能触发视图的更新。

使用这些方法可以在不使用 Vue.set 和 Vue.delete 的情况下改变响应式数据。
```

### 23. Vue 中的 $refs 属性是什么？

```js
Vue 中的 $refs 属性是一个存储组件实例或 DOM 元素的对象。它可以在组件的模板中通过 "ref" 特性来绑定，然后通过 $refs 属性来访问这些绑定。$refs 属性在渲染后才能访问到，因此不能在模板中直接使用。$refs 属性通常用于访问子组件或 DOM 元素。
```

### 24. Vue 中的 $options 属性是什么？

```js
Vue 中的 $options 属性表示当前 Vue 实例的配置选项。它包含了所有在 Vue 实例创建时传入的选项，包括 data、computed、watch、methods、props、components 等。通常不常用，但有时可能会在插件或者组件内部使用。
```

### 25. Vue 中的 $root 属性是什么？

```js
Vue 中的 $root 属性表示当前 Vue 实例的根实例。如果当前实例没有父级实例，则 $root 属性指向自身。通过 $root 属性，可以访问整个 Vue 实例树中任意位置的实例。

new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  },
  methods: {
    showRootMessage: function() {
      alert(this.$root.message);
    }
  }
  // ...
})

通过 $root 属性，可以在 methods中访问根实例的 message 数据。
```

### 26. Vue 中的 $isServer 属性是什么？

```js
$isServer 属性是 Vue 提供的一个只读属性，表示当前 Vue 实例是否运行在服务器端。这个属性可以用来判断当前环境是服务器端渲染还是客户端渲染。如果运行在服务器端，则 $isServer 的值为 true，否则为 false。
```

### 27. Vue 中如何实现动态组件的加载和卸载？

```js
在 Vue 中实现动态组件的加载和卸载可以使用 v-bind 和 v-if 指令。
使用 v-bind 指令可以动态绑定组件的类型，使用 v-if 指令可以控制组件的显示和隐藏。

例如，如果有一个组件类型是由一个变量 currentComponent 控制的，那么可以使用如下代码实现动态加载和卸载：
1. 使用 v-bind 指令动态绑定组件的类型
<component v-bind:is="currentComponent"></component>
2. 使用 v-if 指令控制组件的显示和隐藏
<component v-if="currentComponent" v-bind:is="currentComponent"></component>

其中，v-bind:is 将组件类型绑定到 currentComponent 变量上，v-if 指令用来控制组件的显示和隐藏。
可以通过改变 currentComponent 变量的值来加载和卸载组件。
```

### 28. Vue 中如何使用 $forceUpdate 方法？

```js
$forceUpdate 方法可以强制 Vue 实例重新渲染。使用这个方法前需要清楚的是，通常不需要手动调用这个方法，因为 Vue 通过数据的响应机制自动维护视图的更新。在极少数情况下，由于 Vue 实例内部状态被破坏而导致数据不能正确响应时，需要手动调用 $forceUpdate 方法来修复。

this.$forceUpdate();

注意，$forceUpdate 方法用于强制 Vue 实例重新渲染。它会跳过虚拟 DOM 的生成和 diff 算法，并且不会执行任何钩子函数,直接将实例的 DOM 元素替换为新的 DOM 元素。这个方法通常不会使用，但是在某些情况下，它可以用来强制更新组件。
```

### 29. Vue 中如何使用 $destroy 方法？

```js
在 Vue 中, $destroy 方法用于销毁一个 Vue 实例。这会触发 beforeDestroy 和 destroyed 生命周期钩子，并在销毁实例时解除事件监听器和子组件。使用方法就是在组件实例中调用 $destroy 方法即可。

this.$destroy()

注意：在销毁实例后，该实例的所有绑定和事件监听都会被解除。你不能再访问实例的任何属性和方法。
```

### 30. Vue 中如何使用 $mount 方法？

```js
$mount 方法可以用来手动挂载一个未挂载的 Vue 实例。该方法接受一个可选的 DOM 元素作为参数，如果不传入参数，则会在内存中创建一个新元素并进行挂载。这个方法会在实例上设置 $el 属性，并调用 $mount 方法挂载组件。
1.
// 创建一个 Vue 实例
const vm = new Vue({
  // ...
});

// 手动挂载到 DOM 元素上
vm.$mount('#app');

2.
// 创建一个 Vue 实例
const vm = new Vue({
  // ...
});

// 手动挂载到某个 DOM 元素上
const element = document.getElementById('app');
vm.$mount(element);


如果传入的参数是一个字符串，那么会在 DOM 中查找匹配的元素并进行挂载，如果未找到匹配元素会抛出错误。

注意：在 Vue 实例创建之后立即调用 $mount 方法并不会触发 beforeMount 钩子函数。
```

### 31. Vue2 中如何使用 $watch, $watchGroup 和 $unwatch 方法？

Vue3 已经被弃用了，Vue3 中使用的是 watchEffect 和 watch。

```js
1.$watch 方法可以监听 Vue 实例中某个属性的变化，并在变化时执行一个回调函数。该方法接受两个参数，第一个参数为要监听的属性名称，第二个参数为回调函数。使用方式如下：
vm.$watch('message', function (newValue, oldValue) {
  // 回调函数
})
```

```js
2.$watchGroup 方法可以同时监听多个属性的变化，并在有任意一个属性变化时执行回调函数。该方法接受一个数组参数，数组中的元素为要监听的属性名称，第二个参数为回调函数。使用方式如下：
vm.$watchGroup(['a', 'b'], function (newValues, oldValues) {
  // 回调函数
})
```

```js
3.$unwatch 方法用于取消之前使用 $watch 方法设置的监听器。该方法接受一个参数，为要取消监听的属性名称。使用方式如下：
vm.$unwatch('message')
```

### 32. Vue3 中如何使用 watchEffect 和 watch 方法？

```js
1.watchEffect 方法是用来监听数据变化并执行副作用的函数。它的使用方式与 Vue2 中的 computed 属性类似，可以在函数中进行数据操作或访问其他数据。
watchEffect(() => {
  // logic here
});
```

```js
2.watch 方法是用来监听单个数据属性变化并执行回调函数。它可以接受三个参数，分别是要监听的数据属性、回调函数和选项对象。。
watch('property', (newVal, oldVal) => {
  // logic here
});
```

### 33. Vue 中如何使用 vuex 进行状态管理？

```js
Vuex 是一个专门用于 Vue.js 应用程序的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。
为了使用 vuex 进行状态管理，需要遵循以下步骤：
1.安装 vuex 模块：通过 npm 安装 vuex 模块，命令为 npm install vuex
2.创建 store 文件：在项目中新建一个 store 文件夹，在其中创建 index.js 文件
3.定义 state：在 index.js 文件中定义一个 state 对象，用来存储应用程序的全局状态
4.定义 mutations：在 index.js 文件中定义一个 mutations 对象，用来存储用于更改 state 的函数
5.定义 actions：在 index.js 文件中定义一个 actions 对象，用来存储用于触发 mutations 的函数
6.定义 getters：在 index.js 文件中定义一个 getters 对象，用来存储计算属性
7.创建 store 实例：在 main.js 文件中创建一个 store 实例，并将其挂载到 Vue 实例上
8.使用 vuex 的组件：在需要使用 vuex 的组件中调用 state、mutations、actions 和 getters。
```

### 34. Vue 中的事件修饰符有哪些？

```js
Vue事件修饰符是在事件处理程序中使用的特殊附加功能，用于表示事件的修饰符。
事件修饰符有以下几种：
1.stop：阻止冒泡
2.prevent：阻止默认事件
3.capture：添加事件侦听器时使用事件捕获模式
4.self：只当事件是从侦听器绑定的元素本身触发时调用处理程序
5.once：事件只触发一次

事件修饰符可以在模板中与事件处理程序一起使用，例如：
<button v-on:click.stop="doThis"></button>

事件修饰符可以链式调用,执行顺序是从右到左，例如：
<button @click.stop.prevent="doThis"></button>
```

### 35. Vue 中的按键修饰符有哪些？

```js
Vue 按键修饰符是在事件处理程序中使用的特殊附加功能，用于表示按键的修饰符。
按键修饰符有以下几种：
1.enter：回车键
2.tab：tab 键
3.delete：delete 键
4.esc：esc 键
5.space：space 键
6.up：向上键
7.down：向下键
8.left：向左键
9.right：向右键
10.exact：精确匹配按键修饰符（仅在按下的是指定的按键时触发）

你可以直接使用 KeyboardEvent.key 暴露的按键名称作为修饰符，但需要转为 kebab-case 形式。
例如：
<input @keyup.enter="onEnter" />
// 等价于使用 keyCode 修饰符：
<input @keyup.13="onEnter" />

系统按键修饰符有以下几种：
1.ctrl：ctrl 键
2.alt：alt 键
3.shift：shift 键
4.meta：meta 键

系统按键修饰符写法：
<input @keyup.ctrl="onCtrl" />

鼠标按键修饰符有以下几种：
1.left：鼠标左键
2.right：鼠标右键
3.middle：鼠标中键
鼠标按键修饰符写法：
<button @click.middle="doThis"></button>
```

### 36. Vue 中的自定义指令有哪些？

```js
Vue 自定义指令是一个函数，接收三个参数：
1.el：指令所绑定的元素，可以用来直接操作 DOM
2.binding：一个对象，包含以下属性：
  name：指令名，不包括 v- 前缀
  value：指令的绑定值，例如：v-my-directive="1 + 1" 中，绑定值为 2
  oldValue：指令绑定的前一个值，仅在 update 和 componentUpdated 钩子中可用。无论值是否改变都可用
  expression：字符串形式的指令表达式。例如 v-my-directive="1 + 1" 中，表达式为 "1 + 1"
  arg：传给指令的参数，可选。例如 v-my-directive:foo 中，参数为 "foo"
  modifiers：一个包含修饰符的对象。例如：v-my-directive.foo.bar 中，修饰符对象为 { foo: true, bar: true }
3.vnode：Vue 编译生成的虚拟节点
4.oldVnode：上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用
```

<!-- ### 37. Vue2 和 Vue3 的区别有哪些？
```js
1.模板语法
  Vue2 中的模板语法是基于 HTML 的模板引擎，Vue3 中的模板语法是基于 JavaScript 的模板引擎。
2.响应式系统
  Vue2 中的响应式系统是基于 Object.defineProperty 的，Vue3 中的响应式系统是基于 Proxy 的。
3.编译器
  Vue2 中的编译器是基于正则表达式的，Vue3 中的编译器是基于 AST 的。
4.性能
  Vue2 中的性能是基于优化的，Vue3 中的性能是基于重写的。
5.生命周期
  Vue2 中的生命周期有 11 个，常用的有 8 个，不常用的有 3 个，分别是：
  beforeCreate：实例初始化之后，数据观测(data observer)和 event/watcher 事件配置之前被调用
  created：实例创建完成后被立即调用，此时完成了数据观测，属性和方法的运算，watch/event 事件回调
  beforeMount：在挂载开始之前被调用：相关的 render 函数首次被调用
  mounted：el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子
  beforeUpdate：数据更新时调用，发生在虚拟 DOM 打补丁之前
  updated：由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子
  activated：keep-alive 组件激活时调用
  deactivated：keep-alive 组件停用时调用
  beforeDestroy：实例销毁之前调用。在这一步，实例仍然完全可用
  destroyed：Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁
  errorCaptured：当捕获一个来自子孙组件的错误时被调用

  Vue3 中的生命周期有 12 个，常用的有 8 个，不常用的有 4 个，分别是：
  onBeforeMount：在挂载开始之前被调用：相关的 render 函数首次被调用
  onMounted：组件挂载完成后执行
  onBeforeUpdate：在组件即将因为响应式状态变更而更新其 DOM 树之前调用。
  onUpdated：在组件因为响应式状态变更而更新其 DOM 树之后调用。
  onBeforeUnmount：实例销毁之前调用。在这一步，实例仍然完全可用
  onUnmounted：Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁
  onActivated：keep-alive 组件激活时调用
  onDeactivated：keep-alive 组件停用时调用
  onErrorCaptured：当捕获一个来自子孙组件的错误时被调用
  onRenderTracked：跟踪一个响应式引用的 getter 调用时调用
  onRenderTriggered：当触发一个响应式引用的 setter 时调用
  onServerPrefetch：在组件渲染之前调用。只会在服务器端渲染期间被调用
6.其他
``` -->
