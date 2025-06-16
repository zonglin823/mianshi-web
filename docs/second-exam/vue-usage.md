# Vue 使用

[Vue](https://cn.vuejs.org/) 是国内最普及的前端框架，面试考察概率最高。

::: tip
如有疑问，可免费 [加群](/docs/services/group.md) 讨论咨询，也可参与 [1v1 面试咨询服务](/docs/services/1v1.md)， 专业、系统、高效、全流程 准备前端面试
:::

## 🔥Vue3 和 Vue2 的区别有哪些？说几个主要的

Vue 3 提供了更现代化、更高性能的架构，通过 `Composition API` 和 `Proxy` 响应式系统等改进提升了开发体验 :tada::tada::tada:。相比于 Vue 2，它的优势如下:

::: details 参考答案

**性能优化**

- **虚拟 DOM 重构**：Vue3的虚拟DOM采用了更高效的 `Diff算法`，减少了渲染和更新的开销。

- **Tree-shaking 支持**：Vue3的代码结构模块化，支持按需引入，减小了打包体积。

**Composition API**

- Vue3引入了Composition API，使代码更模块化、复用性更强。

- 使用 `setup()` 方法代替了部分选项式 API，通过函数的方式组织逻辑，代码更加清晰简洁。

**响应式系统改进**

- Vue3使用 `Proxy` 实现响应式，解决了 Vue2使用Object.defineProperty实现响应式的一些局限性，如无法监听新增属性和数组索引变化。

**新特性和改进**

- **Teleport**：可以将组件的DOM渲染到指定的DOM节点之外，例如模态框、通知等。

- **Fragment 支持**：Vue3支持组件返回多个根节点，不再需要单一根节点。

- Vue3原生支持 `TypeScript`，提供更完善的类型推导和开发体验。

- Vue3支持为一个组件绑定多个 `v-model`，并且可以自定义 `prop` 和 `event` 名称。

:::

## 🔥Vue 组件的通讯方式有哪些？

组件之间的通讯通常分为父子组件通讯和跨组件通讯。要注意，vue3 组件的通讯方式和 vue2 有一定的区别。

::: details 参考答案

**父子组件通信**

- Props：父组件通过 `props` 向子组件传递数据。
- $emit：子组件通过 `$emit` 向父组件发送事件，并可以传递数据。
- 获取组件实例对象，调用属性或方法：
  💡 Vue 2：通过 `this.$parent` 获取父组件实例，或通过 `this.$children` 获取子组件实例。
  💡 Vue 3：通过 `ref` 引用子组件，直接访问其属性和方法。
- Vue 3 组件支持多个 `v-model` 绑定和自定义属性名，父子之间的双向绑定更加灵活。

**跨组件通信**

- Provide / Inject：父组件通过 `provide` 向后代组件传递数据，后代组件使用 `inject` 接收数据，适用于深层嵌套组件间的通信。
- vuex：通过全局状态管理库 Vuex 共享状态，实现跨组件通信（vue2）。
- pinia：Pinia 是 Vue 3 推荐的全局状态管理库，替代了 Vuex。
- 事件总线（Vue 2）：Vue 2 中可以通过`Event Bus`实现组件间的通信，但在 Vue 3 中不推荐使用。
- 全局事件处理器：通过在根组件$root或全局对象上监听事件，进行跨组件通信（Vue 3 推荐使用外部库，如 `mitt`）。
  :::

## 🔥Vue 组件的生命周期

Vue 组件的生命周期是指组件从创建到销毁的整个过程，包括组件的初始化、渲染、更新和销毁等阶段。在Vue2和Vue3中，组件的生命周期有一些区别。

::: details Vue2

- **创建阶段**

1️⃣ **beforeCreate**：组件实例刚被创建，数据观测和事件/监听器设置之前。此时无法访问 `data` 、 `computed` 和 `methods` 等。
2️⃣ **created**：组件实例已创建，数据观测、事件/监听器设置完成，此时可以访问 `data` 、 `computed` 和 `methods` 等，通常用于数据初始化。

- **挂载阶段**

3️⃣ **beforeMount**：在挂载开始之前，模板已编译， `el` 和 `template` 已经确定，但尚未渲染。
4️⃣ **mounted**：组件实例挂载到 DOM 上之后，此时可以访问和操作 DOM。

- **更新阶段**

5️⃣ **beforeUpdate**：数据发生变化，DOM 尚未更新。可以在这里做一些数据处理，避免不必要的渲染。
6️⃣ **updated**：数据变化，DOM 更新后调用。此时组件的 DOM 已经更新，可以访问和操作新的 DOM。

- **销毁阶段**

7️⃣ **beforeDestroy**：组件实例销毁之前。可以在此阶段进行清理工作，例如移除事件监听器、定时器等。
8️⃣ **destroyed**：组件实例销毁之后。此时，所有的事件监听器和子组件已被销毁。

:::

::: details Vue3

- **创建阶段**

1️⃣ **onBeforeMount**：等效于 Vue 2 中的 `beforeMount` ，在组件挂载之前调用。
2️⃣ **onMounted**：等效于 Vue 2 中的 `mounted` ，在组件挂载之后调用。

- **更新阶段**

3️⃣ **onBeforeUpdate**：等效于 Vue 2 中的 `beforeUpdate` ，在数据更新之前调用。
4️⃣ **onUpdated**：等效于 Vue 2 中的 `updated` ，在数据更新并渲染之后调用。

- **销毁阶段**

5️⃣ **onBeforeUnmount**：等效于 Vue 2 中的 `beforeDestroy` ，在组件卸载前调用。
6️⃣ **onUnmounted**：等效于 Vue 2 中的 `destroyed` ，在组件卸载后调用。

:::

::: tip setup与生命周期

setup 作为 Vue3 的 Composition API 的一部分, 其内部函数的执行时机早于Mounted钩子。

```vue{7}
<script setup>
  import { ref, onMounted } from 'vue';
  console.log("setup");
  onMounted(() => {
  console.log('onMounted');
  });
  // 执行结果:setup onMounted
</script>

```

:::

## Vue 组件在哪个生命周期发送 ajax 请求？

在 Vue中，接口请求一般放在 `created` 或 `mounted` 生命周期钩子中。

::: details 参考答案

**created 钩子**

- 优点：
  ✅ **更快获取数据**：能尽早获取服务端数据，减少页面加载时间。
  ✅ **SSR 支持**：支持服务器端渲染（SSR），在 SSR 环境中不会受到限制。

- 缺点
  ❌ UI 未渲染时发起请求：如果需要操作 DOM 或渲染数据，可能导致闪屏问题

**mounted 钩子**

- 优点：
  ✅ **DOM 可用**：适合需要操作 DOM 或渲染数据后再发起请求的情况，避免闪屏。

- 缺点
  ❌ **请求延迟**：数据请求会稍微延迟，增加页面加载时间。
  ❌ **SSR 不支持**：`mounted` 只在客户端执行，不适用于 SSR 环境。

:::

## Vue 父子组件生命周期调用顺序

::: details 参考答案

1️⃣ 创建阶段

- 父组件：`beforeCreate` ➡️ `created`
- 子组件：`beforeCreate` ➡️ `created`
- 顺序：
  父组件的 `beforeCreate` 和 `created` 先执行 ，子组件的 `beforeCreate` 和 `created` 后执行。
  > 原因：父组件需要先完成自身的初始化（如 data、computed 等），才能解析模板中的子组件并触发子组件的初始化。

2️⃣ 挂载阶段

- 父组件：`beforeMount`
- 子组件：`beforeMount` ➡️ `mounted`
- 父组件：`mounted`
- 顺序：
  父 `beforeMount` → 子 `beforeCreate`→ 子 `created`→ 子 `beforeMount`→ 子 `mounted` → 父 `mounted`
  > 原因：父组件在挂载前（beforeMount）需要先完成子组件的渲染和挂载，因为子组件是父组件模板的一部分。只有当所有子组件挂载完成后，父组件才会触发自身的 mounted。

3️⃣ 更新阶段

- 父组件：`beforeUpdate`
- 子组件：`beforeUpdate` ➡️ `updated`
- 父组件：`updated`
- 顺序：
  父 `beforeUpdate` → 子 `beforeUpdate` → 子 `updated` → 父 `updated`
  > 原因：父组件的数据变化会触发自身更新流程，但子组件的更新必须在父组件更新前完成（因为子组件可能依赖父组件的数据），最终父组件的视图更新完成。

4️⃣ 销毁阶段

- 父组件：`beforeDestroy`
- 子组件：`beforeDestroy` ➡️ `destroyed`
- 父组件：`destroyed`
- 顺序：
  父 `beforeDestroy` → 子 `beforeDestroy` → 子 `destroyed` → 父 `destroyed`
  > 原因：父组件销毁前需要先销毁所有子组件，确保子组件的资源释放和事件解绑，避免内存泄漏。

::: tip
注：vue3中，`setup()` 替代了 `beforeCreate` 和 `created`，但父子组件的生命周期顺序不变。

:::

## 🔥v-show 和 v-if 的区别

::: details 参考答案

- **渲染方式：**
  💡v-if：条件为 true 时才会渲染元素，条件为 false 时销毁元素。
  💡v-show：始终渲染元素，只是通过 CSS 控制 `display 属性`来显示或隐藏。
- **适用场景：**
  💡v-if：适用于条件变化不频繁的场景。
  💡v-show：适用于条件变化频繁的场景。

:::

## 为何v-if和v-for不能一起使用？

`v-if` 和 `v-for` 不能直接一起使用的原因，主要是因为它们在 **解析优先级** 和 **逻辑处理** 上存在冲突。

::: details 参考答案

由于`v-for` 的解析优先级高于 `v-if`，同时使用 v-if 和 v-for，Vue 首先会循环创建所有dom元素，然后根据条件来判断是否渲染每个元素，这种方式可能导致 Vue 进行大量的 DOM 操作，性能较差。其次，`v-for` 会为每个循环项创建一个新的作用域，而 `v-if` 的条件如果依赖于这个作用域内的数据，可能导致判断逻辑异常。

为避免上述问题，vue官方推荐我们将 `v-if` 放到 `v-for` 外层，或者将 `v-if` 放置到 `v-for` 内部的单个节点上。

```js
<div v-if="show">
  <div v-for="item in list" :key="item.id">{{ item.name }}</div>
</div>
```

:::

## computed 和 watch 有什么区别

::: details 参考答案

**computed**用于计算基于响应式数据的值，并缓存结果:

```vue
<template>
  <div>
    <p>原始值：{{ count }}</p>
    <p>计算后的数值：{{ doubledCount }}</p>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const count = ref(2)

// 计算属性
const doubledCount = computed(() => count.value * 2)
</script>
```

**watch**用于监听数据变化并执行副作用操作

```vue
<template>
  <div>
    <p>原始数值：{{ count }}</p>
    <button @click="count++">增加数值</button>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

const count = ref(0)

// 监听器
watch(count, (newVal, oldVal) => {
  console.log(`数值从 ${oldVal} 变为 ${newVal}`)
})
</script>
```

| 特性         | `computed`                                                   | `watch`                                                  |
| ------------ | ------------------------------------------------------------ | -------------------------------------------------------- |
| **用途**     | 用于计算基于响应式数据的值，并缓存结果                       | 用于监听数据变化并执行副作用操作                         |
| **返回值**   | 返回计算结果                                                 | 不返回值，执行副作用                                     |
| **缓存机制** | 只有在访问时才会计算，会缓存计算结果，仅当依赖变化时重新计算 | 数据变化时立即执行回调，不缓存，每次数据变化都会触发回调 |
| **适用场景** | 计算派生数据，避免不必要的重复计算                           | 执行异步操作、处理副作用操作，如 API 请求                |
| **性能**     | 性能较好，避免重复计算                                       | 每次数据变化时都会执行回调函数                           |

:::

## 🔥watch 和 watchEffect 的区别

`watch` 和 `watchEffect` 都是 Vue 3 中用于响应式数据变化时执行副作用的 API，它们的使用场景和工作机制存在区别：

::: details 参考答案

- **依赖追踪方式**

`watch` ：需要显式声明依赖，监听指定的数据源；可以监听多个数据源或进行深度监听。

```js
import { watch, reactive } from 'vue'
const state = reactive({
  count: 0,
})
watch(
  () => state.count, // 显式声明监听的依赖
  (newCount, oldCount) => {
    console.log(`新值 ${newCount} 老值 ${oldCount}`)
  }
)
```

`watchEffect` ：会自动追踪 **作用域内所有的响应式依赖**，不需要显式声明依赖。

```js
import { watchEffect, reactive } from 'vue'
const state = reactive({
  count: 0,
})
watchEffect(() => {
  console.log(`Count 变化了: ${state.count}`) // 自动追踪 `state.count`
})
```

- **执行时机**

`watch` ：在监听的响应式数据变化后立即执行。

`watchEffect` ：在 **组件挂载时** 执行一次副作用，并在 **依赖发生变化时** 再次执行。

- **适用场景**

`watch` ：适用于 **监听特定数据** 变化并执行副作用的场景，如 API 请求、保存操作等。适合需要 **访问新值和旧值** 进行比较的场景。

`watchEffect` ：不需要访问旧值，适用于 **自动追踪多个响应式依赖** 的副作用，如渲染、自动保存等。

:::

> Vue官方API： [watchEffect](https://cn.vuejs.org/api/reactivity-core.html#watcheffect)

## 🔥Vue3 ref 和 reactive 如何选择？

`ref` 和 `reactive` 都是 Vue 3 中用来创建响应式数据的 API，他们的区别及使用场景如下。

::: details 参考答案

- **reactive的实现：**
  `reactive` 通过 `Proxy` 对对象或数组的每个属性进行深度代理，实现响应式。这种设计使得 `reactive` 能自动追踪所有嵌套属性的变化，但由于 `Proxy` 无法直接处理基本数据类型（如 `number` 、 `string` 、 `boolean` ），因此， `reactive` 不适用于基本数据类型。

- **ref的实现：**
  为了实现基本数据类型的响应式，Vue 设计了 `ref` 。 `ref` 会将基本数据类型封装为一个包含 `value` 属性的对象，通过 `getter` 和 `setter` 实现响应式依赖追踪和更新。当访问或修改 `ref.value` 时，Vue 内部会触发依赖更新。此外，对于复杂数据类型（如对象或数组）， `ref` 的内部实现会直接调用 `reactive` ，将复杂数据类型变为响应式。

::: tip 如何选择

**Vue官方建议**使用 `ref()` 作为声明响应式状态的主要，因为 `reactive` 存在以下局限性：

💡有限的值类型：它只能用于对象类型 (对象、数组和如 Map、Set 这样的集合类型)。它不能持有如 string、number 或 boolean 这样的原始类型。
💡不能替换整个对象：由于 Vue 的响应式跟踪是通过属性访问实现的，因此我们必须始终保持对响应式对象的相同引用。这意味着我们不能轻易地“替换”响应式对象，因为这样的话与第一个引用的响应性连接将丢失：

```js
let state = reactive({
  count: 0,
})

// 上面的 ({ count: 0 }) 引用将不再被追踪
// (响应性连接已丢失！)
state = reactive({
  count: 1,
})
```

💡对解构操作不友好：当我们将响应式对象的原始类型属性解构为本地变量时，或者将该属性传递给函数时，我们将丢失响应性连接

```js
const state = reactive({
  count: 0,
})
// 当解构时，count 已经与 state.count 断开连接
let { count } = state
// 不会影响原始的 state
count++

// 该函数接收到的是一个普通的数字
// 并且无法追踪 state.count 的变化
// 我们必须传入整个对象以保持响应性
callSomeFunction(state.count)
```

:::

## 什么是动态组件？如何使用它？

::: details 参考答案

动态组件是 Vue 提供的一种机制，允许我们根据条件动态切换渲染的组件，而不需要手动修改模板。
在Vue中，我们可以通过 ` <component>` 标签的 `:is` 属性指定需要渲染的组件：

```vue
<template>
  <div>
    <!-- 动态渲染组件 -->
    <component :is="currentComponent"></component>

    <!-- 控制组件切换 -->
    <button @click="currentComponent = 'ComponentA'">显示组件A</button>
    <button @click="currentComponent = 'ComponentB'">显示组件B</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import ComponentA from './ComponentA.vue'
import ComponentB from './ComponentB.vue'

// 当前显示的组件
const currentComponent = ref('ComponentA')
</script>
```

`<component>` 标签的 `:is` 属性值可以是：

- 被注册的组件名
- 导入的组件对象
- 一般的 HTML 元素

当使用 `<component :is="...">` 来在多个组件间作切换时，被切换掉的组件会被卸载。如果需要保留动态组件状态，使用 `<KeepAlive>` 组件即可。

:::

## 什么是 slot ，有什么应用场景？

slot 是 Vue 中的一种用于 组件内容分发 的机制。它允许父组件向子组件插入内容，从而使组件更加灵活和可复用。

::: details 参考答案

在Vue中，插槽的使用方式可以分为四种：**默认插槽**、**具名插槽**、**条件插槽**和**作用域插槽**。

- **默认插槽**

默认插槽是最简单的插槽形式，它允许我们将组件的内容传递到组件内部的一个占位符中。

子组件 `MyComponent.vue`

```vue
<template>
  <div>
    <p>我是子组件的标题</p>
    <slot></slot>
  </div>
</template>
```

父组件

```vue
<template>
  <MyComponent>
    <p>这是插槽内容，由父组件传入</p>
  </MyComponent>
</template>
```

输出结果：

```html
<div>
  <p>我是子组件的标题</p>
  <p>这是插槽内容，由父组件传入</p>
</div>
```

- **具名插槽**

当子组件需要多个插槽时，可以为插槽命名，并由父组件指定内容放置到哪个插槽。

子组件 `MyComponent.vue`

```vue
<template>
  <slot name="header">默认标题</slot>
  <slot>默认内容</slot>
  <slot name="footer">默认页脚</slot>
</template>
```

父组件

```vue
<template>
  <MyComponent>
    <template v-slot:header>
      <h1>我来组成头部</h1>
    </template>
    <!-- 隐式的默认插槽 -->
    <p>我来组成身体</p>
    <template v-slot:footer>
      <p>我来组成尾部</p>
    </template>
  </MyComponent>
</template>
```

输出结果：

```html
<div>
  <h1>我来组成头部</h1>
  <p>我来组成身体</p>
  <p>我来组成尾部</p>
</div>
```

> `v-slot` 有对应的简写 `#` ，因此 `<template v-slot:header>` 可以简写为 `<template #header>` 。其意思就是“将这部分模板片段传入子组件的 header 插槽中”。

- **条件插槽**

我们可以根据插槽是否存在来渲染某些内容:

子组件 `MyComponent.vue`

```vue
<template>
  <div class="card">
    <div v-if="$slots.header" class="card-header">
      <slot name="header" />
    </div>

    <div v-if="$slots.default" class="card-content">
      <slot />
    </div>

    <div v-if="$slots.footer" class="card-footer">
      <slot name="footer" />
    </div>
  </div>
</template>
```

- **作用域插槽**

作用域插槽可以让子组件在渲染时将一部分数据提供给插槽，从而实现父组件的插槽访问到子组件的状态。

子组件 `MyComponent.vue`

```vue
<template>
  <ul>
    <!-- 定义作用域插槽，并将 items 数据传递给父组件 -->
    <slot :items="items"></slot>
  </ul>
</template>

<script setup>
import { ref } from 'vue'

// 定义数据 items
const items = ref(['华为', '小米', '苹果'])
</script>
```

```vue
<template>
  <MyComponent>
    <!-- 使用作用域插槽，接收子组件传递的 items 数据 -->
    <template #default="{ items }">
      <li v-for="(item, index) in items" :key="index">
        {{ item }}
      </li>
    </template>
  </MyComponent>
</template>

<script setup>
import MyComponent from './MyComponent.vue'
</script>
```

输出结果：

```html
<ul>
  <li>华为</li>
  <li>小米</li>
  <li>苹果</li>
</ul>
```

> Vue官方API： [插槽 Slots](https://cn.vuejs.org/guide/components/slots.html#scoped-slots)

::: tip 应用场景

💡灵活的组件内容插入：
插槽允许我我们将内容插入组件中，而无需修改子组件内部逻辑，极大提高了组件的灵活性。

💡构建通用组件：
比如开发卡片、模态框、列表等组件，使用插槽可以轻松实现内容的自定义。模态框组件可通过插槽自定义标题、正文和按钮。

💡减少重复代码：
通过插槽，将公共逻辑封装到子组件中，而在父组件中只需插入变化的内容。

:::

## 🚀Vue 项目可做哪些性能优化？

🔍在 Vue 项目中，我们可以利用 Vue 特有的功能和机制实现性能优化。

::: details 参考答案

1️⃣ **模板和指令优化**

- 合理的使用 `v-if` 和 `v-show` 指令，避免不必要的渲染。
- 使用 `v-for` 时，尽量提供唯一的 `key` ，避免重复渲染。
- 使用 `v-once` 指令，只渲染一次，避免不必要的计算。
- 使用 `v-memo` 指令，对使用`v-for`生成的列表进行渲染优化。`(vue3.2新增)`

2️⃣ **组件优化**

- 合理使用 `keep-alive` 组件，缓存组件实例，避免重复渲染。
- 使用异步组件加载，减少首屏加载时间。

```js
const AsyncComponent = defineAsyncComponent(() => import('./MyComponent.vue'))
```

- 配合 Vue Router 使用路由懒加载，实现路由页面按需加载。
- 合理划分组件，提升复用性和渲染性能。

3️⃣ **响应式优化**

- 使用 `Object.freeze` 冻结对象，避免不必要的响应式。
- 使用 stop 停止 不必要的watchEffect副作用执行，以减少性能消耗。
- watch的优化

  💡 避免滥用深度监听，降低性能开销。

  💡 对于频繁触发的响应式数据变化，可以通过防抖和节流优化监听逻辑。

```js
import { debounce } from 'lodash'

watch(
  () => searchQuery,
  debounce((newQuery) => {
    fetchSearchResults(newQuery)
  }, 300)
)
```

💡 可以通过返回函数只监听具体的依赖，减少不必要的触发。

```js
watch([() => user.name, () => user.age], ([newName, newAge]) => {
  //...
})
```

💡 当监听器在某些条件下不再需要时，可以通过返回的 stop 方法手动停止监听，以节省资源

```js
const stop = watch(
  () => data.value,
  (newValue) => {
    if (newValue === 'done') {
      stop() // 停止监听
    }
  }
)
```

💡 当多个监听器的回调逻辑类似时，可以合并监听

```js
watch([() => user.name, () => user.age], ([newName, newAge]) => {
  //...
})
```

:::

## 什么是 nextTick 如何应用它

::: details 参考答案

在 Vue.js 中， `nextTick` 是一个核心工具方法，用于处理 DOM 更新时机问题。它的核心作用是：**在下次 DOM 更新循环结束后执行回调，确保我们能操作到最新的 DOM 状态。**
它的使用场景如下：

- 数据变化后操作 DOM

```vue
<script setup>
async function increment() {
  count.value++
  // DOM 还未更新
  console.log(document.getElementById('counter').textContent) // 0
  await nextTick()
  // DOM 此时已经更新
  console.log(document.getElementById('counter').textContent) // 1
}
</script>

<template>
  <button id="counter" @click="increment">{{ count }}</button>
</template>
```

- 在生命周期钩子中操作 DOM

```vue
<script setup>
import { ref, onMounted, nextTick } from 'vue'
// 创建 DOM 引用
const element = ref(null)

onMounted(() => {
  // 直接访问可能未渲染完成
  console.log(element.value.offsetHeight) // 0 或未定义
  // 使用 nextTick 确保 DOM 已渲染
  nextTick(() => {
    console.log(element.value.offsetHeight) // 实际高度
  })
})
</script>
```

注意，在vue2中和vue3的选项式 API中，我们使用this.$nextTick(callback)的方式调用。

```js
this.$nextTick(() => {
  console.log(this.$refs.text.innerText) // "更新后的文本"
})
```

:::

## 使用 Vue3 Composable 组合式函数，实现 useCount

::: tip

在 Vue 应用的概念中，“**组合式函数**”(Composables) 是一个利用 Vue 的组合式 API 来封装和复用有状态逻辑的函数。它和自定义 `React hooks` 非常相似。

:::

使用组合式函数实现如下需求：useCount 是一个计数逻辑管理的组合式函数，它返回一个 `count` 变量和增加、减少、重置count的方法。

::: details 参考答案

```vue
<script setup>
import { ref } from 'vue'

// 实现 useCount 组合式函数
function useCount() {
  const count = ref(0)
  const increment = () => {
    count.value++
  }
  const decrement = () => {
    count.value--
  }
  const reset = () => {
    count.value = 0
  }
  return {
    count,
    increment,
    decrement,
    reset,
  }
}

// 使用 useCount 组合式函数
const { count, increment, decrement, reset } = useCount()
</script>

<template>
  <div>
    <h2>计数器: {{ count }}</h2>
    <button @click="increment">增加</button>
    <button @click="decrement">减少</button>
    <button @click="reset">重置</button>
  </div>
</template>
```

:::

## 使用 Vue3 Composable 组合式函数，实现 useRequest

```js
const { loading, data, error } = useRequest(url) // 可只考虑 get 请求
```

::: details 参考答案

```ts
import { ref, computed } from 'vue';
import axios from 'axios';

// 实现 useRequest 组合式函数
function useRequest(url) {
  const loading = ref(false); // 请求状态
  const data = ref(null); // 响应数据
  const error = ref(null); // 错误信息

  const fetchData = async () => {
    loading.value = true;
    error.value = null;
    try {
      const response = await axios.get(url); /
      data.value = response.data;
    } catch (err) {
      error.value = err.message || '请求失败'; /
    } finally {
      loading.value = false;
    }
  };

  // 自动触发请求
  fetchData();

  return {
    loading,
    data,
    error,
  };
}

export default useRequest;
```

使用

```vue
<script setup>
import useRequest from './useRequest'
const url = 'https://www.mianshipai.com/'
const { loading, data, error } = useRequest(url)
</script>
<template>
  <div>
    <h2>请求数据</h2>
    <div v-if="loading">加载中...</div>
    <div v-else-if="error">{{ error }}</div>
    <div v-else>
      <p>{{ data }}</p>
    </div>
  </div>
</template>
```

:::

## 自定义组件如何实现 v-model

`v-model` 可以在组件上使用以实现双向绑定。

::: details vue2
在vue2中，自定义组件使用 `v-model` ，需要在组件内部定义 `value` prop，然后通过 `this.$emit('input', newValue)` 触发更新即可。

```vue
<!-- CustomInput.vue -->
<template>
  <input :value="value" @input="$emit('input', $event.target.value)" />
</template>

<script>
export default {
  props: ['value'],
}
</script>
```

使用方式：

```vue
<CustomInput v-model="searchText" />
```

:::

::: details vue3
与vue2类似，vue3自定义组件使用 `v-model` ，需要在组件内部定义 `modelValue` prop，然后通过 `emit('update:modelValue', newValue)` 触发更新

```vue
<!-- CustomInput.vue -->
<template>
  <input :value="modelValue" @input="$emit('update:modelValue', $event.target.value)" />
</template>

<script setup>
defineProps(['modelValue'])
defineEmits(['update:modelValue'])
</script>
```

使用方式：

```vue
<CustomInput v-model="searchText" />
```

---

**👉注意，从 Vue 3.4 开始，官方推荐的实现方式是使用 defineModel() 宏：**

```vue
<!-- Child.vue -->
<script setup>
const model = defineModel()

function update() {
  model.value++
}
</script>

<template>
  <div>父组件的 v-model 值为: {{ model }}</div>
  <button @click="update">Increment</button>
</template>
```

父组件使用 v-model 绑定一个值：

```vue
<!-- Parent.vue -->
<Child v-model="countModel" />
```

`defineModel` 是一个便利宏，其返回的值是一个 `ref` 。它可以像其他 `ref` 一样被访问以及修改，不过它能起到在父组件和当前变量之间的双向绑定的作用：

- 它的 `.value` 和父组件的 `v-model` 的值同步；
- 当它被子组件变更了，会触发父组件绑定的值一起更新。
  根据 `defineModel` 的特性，我们可以用 `v-model` 把这个 `ref` 绑定到一个原生 `input` 元素上：

```vue
<script setup>
const model = defineModel()
</script>

<template>
  <input v-model="model" />
</template>
```

> 此外，v-model 可以接受自定义参数、添加修饰符，组件也可以绑定多个 v-model ，具体用法请参考
> 官网文档：[组件 v-model](https://cn.vuejs.org/guide/components/v-model)

:::

## 如何统一监听 Vue 组件报错

::: details 参考答案

在 Vue 3 中，可以通过 全局错误处理器 `（errorHandler）` 和 生命周期钩子（例如 `onErrorCaptured` ）来统一监听和处理组件中的错误。

- **通过全局错误处理器 `app.config.errorHandler`**

```TypeScript
import { createApp } from 'vue';
const app = createApp(App);
// 设置全局错误处理器
app.config.errorHandler = (err, instance, info) => {
  console.error('捕获到组件错误: ', err);
  console.log('发生错误的组件实例: ', instance);
  console.log('错误信息: ', info);
};

app.mount('#app');
```

- **局部错误捕获（onErrorCaptured）**

`onErrorCaptured` 钩子可以捕获后代组件传递过程中的错误信息

```vue
<script setup>
import { onErrorCaptured } from 'vue'

onErrorCaptured((err, instance, info) => {
  console.error('局部捕获到错误: ', err)
  console.log('错误来源组件: ', instance)
  console.log('错误信息: ', info)

  // 这个钩子可以通过返回 false 来阻止错误继续向上传递。
  return false // 如果需要让错误冒泡到全局，省略或返回 true
})
</script>

<template>
  <div>
    <h2>局部错误捕获示例</h2>
    <ErrorProneComponent />
  </div>
</template>
```

> Vue官方API： [onErrorCaptured](https://cn.vuejs.org/api/composition-api-lifecycle.html#onerrorcaptured)、[errorHandler](https://cn.vuejs.org/api/application.html#app-config-errorhandler)

:::

## Vuex 中 mutation 和 action 有什么区别？

在 Vuex 中， `mutation` 和 `action` 是用于管理状态的两种核心概念。

::: details 参考答案
`mutation` 可以直接修改 `store` 中的 **state**值，它只支持同步操作。 `Action` 不能直接修改 **state**，而是通过调用 `mutation` 来间接修改，它用于处理异步操作。

```js
const store = createStore({
  state: {
    count: 0, // 定义状态
  },
  mutations: {
    // Mutation 示例（同步）
    increment(state, payload) {
      state.count += payload
    },
  },
})

// 组件中调用
this.$store.commit('increment', 5)
```

```js
const store = createStore({
  state: {
    count: 0, // 定义状态
  },
  mutations: {
    // Mutation：同步修改状态
    increment(state, payload) {
      state.count += payload
    },
  },
  actions: {
    // Action：异步操作，延迟1秒后调用 mutation
    asyncIncrement({ commit }, payload) {
      setTimeout(() => {
        commit('increment', payload) // 提交 mutation 修改状态
      }, 1000)
    },
  },
})

// 组件中调用
this.$store.dispatch('asyncIncrement', 5)
```

**总结：**
| 特性 | Mutation | Action |
| --- | --- | --- |
| 是否同步 | ✅ 同步 | ⏳ 异步（也可以处理同步） |
| 是否直接修改 state | ✅ 直接修改 | ❌ 通过调用 mutation 修改 |
| 调用方式 | `commit('mutationName')` | `dispatch('actionName')` |
| 适用场景 | 简单的状态修改 | 异步操作（如 API 调用） |
| 调试支持 | 完全支持，易于追踪 | 依赖于 mutation 的日志 |

::: tip ⚠️ 为什么要有这样的区分？

- 数据可预测性：通过强制 `Mutation` 同步修改 **State**，使得状态变更可追踪
- 调试友好性：DevTools 可以准确捕捉每次状态快照
- 代码组织：将同步逻辑与异步逻辑分离，提高代码可维护性

:::

参考文章：[VueX用法快速回顾](https://juejin.cn/post/7249033891809329212)

## Vuex 和 Pinia 有什么区别？

::: details 参考答案

`Pinia` 和 `Vuex` 都是 Vue 的专属状态管理库，允许用户跨组件或页面共享状态。

- **区别**

| 特性                | **Vuex**                                | **Pinia**                                       |
| ------------------- | --------------------------------------- | ----------------------------------------------- |
| **版本支持**        | Vue 2 和 Vue 3                          | 仅支持 Vue 3（基于 `Composition API` ）         |
| **API 风格**        | 基于传统的对象式 API                    | 基于 Composition API，类似于 `setup` <br/> 语法 |
| **模块管理**        | 支持模块化（modules），但语法较复杂     | 模块化简单，**每个 store 就是一个独立模块**     |
| **TypeScript 支持** | `TypeScript` 支持不完善，需手动定义类型 | 开箱即用的 `TypeScript` 支持，类型推导更强大    |
| **性能**            | 更适合大型项目，但冗余代码较多          | 更加轻量，性能更好，支持按需加载                |
| **状态持久化**      | 需要额外插件                            | 插件系统更加灵活，支持状态持久化插件            |

- **代码对比**

📝 **vuex**

```javascript
// store.js
import { createStore } from 'vuex'

const store = createStore({
  state: {
    count: 0,
  },
  mutations: {
    increment(state) {
      state.count++
    },
  },
  actions: {
    asyncIncrement({ commit }) {
      setTimeout(() => {
        commit('increment')
      }, 1000)
    },
  },
  getters: {
    doubleCount: (state) => state.count * 2,
  },
})

export default store
```

vue组件中使用

```vue
<script>
export default {
  // 计算属性
  computed: {
    count() {
      return this.$store.state.count
    },
    doubleCount() {
      return this.$store.getters.doubleCount
    },
  },
  methods: {
    // 同步增加
    increment() {
      this.$store.commit('increment')
    },
    // 异步增加
    asyncIncrement() {
      this.$store.dispatch('asyncIncrement')
    },
  },
}
</script>
```

📝**Pinia**

```typescript
// store.js
import { defineStore } from 'pinia'

export const useCounterStore = defineStore('counter', {
  state: () => ({
    count: 0,
  }),
  actions: {
    increment() {
      this.count++
    },
    async asyncIncrement() {
      setTimeout(() => {
        this.increment()
      }, 1000)
    },
  },
  getters: {
    doubleCount: (state) => state.count * 2,
  },
})
```

组件中使用：

```vue
<script setup>
import { useCounterStore } from './store'
const counter = useCounterStore()
</script>

<template>
  <h1>Count的计算值 {{ counter.count }}</h1>
  <h2>Double的计算值 {{ counter.doubleCount }}</h2>
  <button @click="counter.increment">同步增加</button>
  <button @click="counter.asyncIncrement">异步增加</button>
</template>
```

- **如何选择？**

对于vue3项目，官方推荐使用pinia。因为它**更轻量、TypeScript 支持更好、模块化更简单且拥有更强的 DevTools 支持**。

:::

## Vue-router 导航守卫能用来做什么？

::: details 参考答案

`vue Router` 的**导航守卫**用于在路由跳转过程中对导航行为进行**拦截**和**控制**。这些守卫在路由进入、离开或更新时执行，可以用于多种场景，确保应用的导航逻辑符合预期。以下是常见的用途：

- 认证和授权

用于检查用户的登录状态或权限，防止未授权用户访问受限页面。

```javascript
router.beforeEach((to, from, next) => {
  const isAuthenticated = !!localStorage.getItem('token')
  if (to.meta.requiresAuth && !isAuthenticated) {
    next('/login') // 未登录，跳转到登录页
  } else {
    next() // 已登录，正常导航
  }
})
```

- 数据预加载

在进入路由前预加载必要的数据，确保页面渲染时数据已准备好。

```javascript
router.beforeEach(async (to, from, next) => {
  if (to.name === 'userInfo') {
    await store.dispatch('fetchUserData') // 预加载用户数据
  }
  next()
})
```

- 动态修改页面标题

根据路由信息动态更改浏览器标签页的标题，提升用户体验。

```javascript
router.afterEach((to) => {
  document.title = to.meta.title || '自定义标题'
})
```

- 动画和加载效果

在路由切换时展示加载动画或过渡效果，提升用户体验。

```javascript
router.beforeEach((to, from, next) => {
  store.commit('setLoading', true) // 开始加载动画
  next()
})

router.afterEach(() => {
  store.commit('setLoading', false) // 结束加载动画
})
```

- 日志记录和分析

在路由切换时记录用户行为，用于分析或调试。

```javascript
router.afterEach((to, from) => {
  console.log(`用户从 ${from.fullPath} 跳转到 ${to.fullPath}`)
})
```

- 防止访问不存在的页面

通过守卫检查路由是否存在，避免导航到无效页面。

```javascript
router.beforeEach((to, from, next) => {
  const routeExists = router.getRoutes().some((route) => route.name === to.name)
  if (!routeExists) {
    next('/404') // 跳转到 404 页面
  } else {
    next()
  }
})
```

:::

## Vue3中组件通信有哪些方式？

::: details 参考答案
Vue3提供了8种主要的组件通信方式，覆盖了父子、兄弟、跨层级等各种场景。

核心通信方式 🎯

- Props/Emits：父子组件的经典通信方案
- v-model：双向数据绑定的语法糖
- Provide/Inject：跨层级依赖注入
- Slots：内容分发机制
- Teleport：跨DOM层级渲染
- ref/expose：父组件直接访问子组件
- 状态管理：Pinia/Vuex全局状态
- EventBus：事件总线（需第三方库）
  选择原则 📋
- 父子通信：优先使用Props/Emits
- 跨层级：Provide/Inject或状态管理
- 兄弟组件：状态管理或EventBus
- 内容传递：Slots插槽

父子组件通信

```vue
<!-- 父组件 -->
<template>
  <UserCard :user="currentUser" :show-avatar="true" :theme="'dark'" @update-user="handleUserUpdate" />
</template>

<script setup>
import { ref } from 'vue'
import UserCard from './UserCard.vue'

const currentUser = ref({
  name: 'John Doe',
  email: 'john@example.com',
  avatar: '/avatar.jpg',
})

const handleUserUpdate = (newUser) => {
  currentUser.value = { ...newUser }
}
</script>
```

```vue
<!-- 子组件 UserCard.vue -->
<script setup>
// 🎯 Vue3中props的定义方式
const props = defineProps({
  user: {
    type: Object,
    required: true,
  },
  showAvatar: {
    type: Boolean,
    default: true,
  },
  theme: {
    type: String,
    default: 'light',
    validator: (value) => ['light', 'dark'].includes(value),
  },
})

// 🎯 定义事件
const emit = defineEmits(['update-user'])

const updateUserInfo = () => {
  emit('update-user', {
    ...props.user,
    lastUpdated: new Date(),
  })
}
</script>
```

v-model双向绑定

```vue
<!-- 父组件 -->
<template>
  <CustomInput v-model="searchText" />
  <CustomInput v-model:value="inputValue" v-model:visible="showInput" />
</template>

<script setup>
import { ref } from 'vue'

const searchText = ref('')
const inputValue = ref('')
const showInput = ref(true)
</script>
```

```vue
<!-- 子组件 CustomInput.vue -->
<script setup>
// 🎯 单个v-model
const props = defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue'])

// 🎯 多个v-model
const props = defineProps(['value', 'visible'])
const emit = defineEmits(['update:value', 'update:visible'])

const updateValue = (newValue) => {
  emit('update:value', newValue)
}
</script>

<template>
  <input :value="value" @input="updateValue($event.target.value)" v-show="visible" />
</template>
```

ref直接访问

```vue
<!-- 父组件 -->
<template>
  <ChildComponent ref="childRef" />
  <button @click="callChildMethod">调用子组件方法</button>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import ChildComponent from './ChildComponent.vue'

const childRef = ref()

const callChildMethod = () => {
  // 🎯 直接调用子组件的方法
  childRef.value.doSomething()
}

onMounted(() => {
  // 🎯 访问子组件的数据
  console.log(childRef.value.message)
})
</script>
```

```vue
<!-- 子组件 ChildComponent.vue -->
<script setup>
import { ref } from 'vue'

const message = ref('Hello from child')

const doSomething = () => {
  console.log('子组件方法被调用了！')
}

// 🎯 暴露给父组件的方法和数据
defineExpose({
  message,
  doSomething,
})
</script>
```

跨层级通信

```vue
<!-- 祖先组件 -->
<script setup>
import { provide, ref, readonly } from 'vue'

const theme = ref('light')
const user = ref({ name: 'Admin' })

// 🎯 提供数据（只读）
provide('theme', readonly(theme))
provide('user', readonly(user))

// 🎯 提供方法
provide('updateTheme', (newTheme) => {
  theme.value = newTheme
})

provide('updateUser', (newUser) => {
  user.value = { ...user.value, ...newUser }
})
</script>
```

```vue
<!-- 后代组件 -->
<script setup>
import { inject } from 'vue'

// 🎯 注入数据和方法
const theme = inject('theme', 'light') // 默认值
const user = inject('user')
const updateTheme = inject('updateTheme')
const updateUser = inject('updateUser')

// 🎯 使用注入的数据
const switchTheme = () => {
  updateTheme(theme.value === 'light' ? 'dark' : 'light')
}
</script>

<template>
  <div :class="`theme-${theme}`">
    <h3>User: {{ user.name }}</h3>
    <button @click="switchTheme">切换主题</button>
  </div>
</template>
```

```vue
<!-- 后代组件 -->
<script setup>
import { inject } from 'vue'

// 🎯 注入数据和方法
const theme = inject('theme', 'light') // 默认值
const user = inject('user')
const updateTheme = inject('updateTheme')
const updateUser = inject('updateUser')

// 🎯 使用注入的数据
const switchTheme = () => {
  updateTheme(theme.value === 'light' ? 'dark' : 'light')
}
</script>

<template>
  <div :class="`theme-${theme}`">
    <h3>User: {{ user.name }}</h3>
    <button @click="switchTheme">切换主题</button>
  </div>
</template>
```

Teleport传送门

```vue
<!-- 组件内部 -->
<template>
  <div class="component">
    <h3>组件内容</h3>

    <!-- 🎯 将模态框传送到body -->
    <Teleport to="body">
      <div v-if="showModal" class="modal">
        <div class="modal-content">
          <h2>模态框标题</h2>
          <p>这个模态框被传送到了body元素中</p>
          <button @click="showModal = false">关闭</button>
        </div>
      </div>
    </Teleport>

    <button @click="showModal = true">显示模态框</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const showModal = ref(false)
</script>
```

EventBus事件总线

```js
// 🎯 创建事件总线 (使用mitt库)
import mitt from 'mitt'

export const eventBus = mitt()

// 组件A - 发送事件
import { eventBus } from '@/utils/eventBus'

const sendMessage = () => {
  eventBus.emit('user-login', {
    userId: 123,
    username: 'john',
  })
}

// 组件B - 监听事件
import { onMounted, onUnmounted } from 'vue'
import { eventBus } from '@/utils/eventBus'

const handleUserLogin = (userData) => {
  console.log('用户登录:', userData)
}

onMounted(() => {
  eventBus.on('user-login', handleUserLogin)
})

onUnmounted(() => {
  eventBus.off('user-login', handleUserLogin)
})
```

Pinia状态管理

```js
// stores/user.js
import { defineStore } from 'pinia'
import { ref, computed } from 'vue'

export const useUserStore = defineStore('user', () => {
  // 🎯 状态
  const user = ref(null)
  const isLoggedIn = computed(() => !!user.value)

  // 🎯 方法
  const login = async (credentials) => {
    const userData = await api.login(credentials)
    user.value = userData
  }

  const logout = () => {
    user.value = null
  }

  const updateProfile = (profileData) => {
    if (user.value) {
      user.value = { ...user.value, ...profileData }
    }
  }

  return {
    user,
    isLoggedIn,
    login,
    logout,
    updateProfile,
  }
})
```

```vue
<!-- 任意组件中使用 -->
<script setup>
import { useUserStore } from '@/stores/user'

const userStore = useUserStore()

// 🎯 响应式地访问状态
const { user, isLoggedIn } = storeToRefs(userStore)

// 🎯 调用方法
const handleLogin = async () => {
  await userStore.login({ email: 'user@example.com', password: '123' })
}
</script>

<template>
  <div v-if="isLoggedIn">
    欢迎, {{ user.name }}!
    <button @click="userStore.logout">退出登录</button>
  </div>
</template>
```

作用域插槽

```vue
<!-- 子组件 DataList.vue -->
<template>
  <div class="data-list">
    <div v-for="item in items" :key="item.id" class="list-item">
      <!-- 🎯 作用域插槽：将数据传递给父组件 -->
      <slot :item="item" :index="index" :isActive="activeId === item.id" :toggle="() => toggleItem(item.id)">
        <!-- 默认插槽内容 -->
        <span>{{ item.name }}</span>
      </slot>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

defineProps(['items'])

const activeId = ref(null)

const toggleItem = (id) => {
  activeId.value = activeId.value === id ? null : id
}
</script>
```

```vue
<!-- 父组件使用作用域插槽 -->
<template>
  <DataList :items="userList">
    <template #default="{ item, isActive, toggle }">
      <div :class="{ active: isActive }" @click="toggle">
        <img :src="item.avatar" :alt="item.name" />
        <div>
          <h4>{{ item.name }}</h4>
          <p>{{ item.email }}</p>
        </div>
      </div>
    </template>
  </DataList>
</template>
```

避免过度通信

```js
// ❌ 避免频繁的深层通信
// 祖先组件 → 父组件 → 子组件 → 孙组件

// ✅ 使用Provide/Inject直接通信
// 祖先组件 → 孙组件
```

合理选择通信粒度

```js
// ❌ 过细的状态拆分
const firstName = ref('')
const lastName = ref('')
const email = ref('')

// ✅ 合理的状态聚合
const user = ref({
  firstName: '',
  lastName: '',
  email: '',
})
```

:::

## 为什么不建议v-if和v-for一起使用？

::: details

在Vue中，应当避免在同一元素上同时使用v-if和v-for，主要原因是它们的优先级问题：

- 在Vue 2中，v-for的优先级高于v-if
- 在Vue 3中，v-if的优先级高于v-for
  这种优先级差异会导致：

- 性能浪费：每次渲染时都会先遍历整个列表，再判断显示条件
- 代码逻辑不明确：阅读代码时难以理解真正的渲染逻辑
- 潜在错误：在Vue 2和Vue 3中可能产生完全不同的结果
- 正确做法是：要么使用计算属性先过滤数据，要么将v-if移到父元素或子元素上。

:::

## 如何传递路由参数？params和query的区别？

::: details
Vue Router传递参数有params和query两种方式，核心区别在于URL表现形式和使用场景。

主要区别 🎯

- params参数：路径参数，集成在URL路径中 /user/123
- query参数：查询参数，以?形式拼接 /user?id=123&tab=profile

```js
// params传参
this.$router.push({ name: 'User', params: { id: 123 } })
// 结果：/user/123

// query传参
this.$router.push({ path: '/user', query: { id: 123, tab: 'profile' } })
// 结果：/user?id=123&tab=profile
```

```js
// 获取params参数
const userId = this.$route.params.id

// 获取query参数
const tab = this.$route.query.tab
```

:::

## $router和$route的区别是什么？

:::details

- $router是路由器实例对象，用于执行路由操作（如跳转、前进、后退）。

- $route是当前路由信息对象，用于获取当前路由的参数、查询、路径等信息。

核心区别 🎯

- $router：我要去哪里（导航操作）
- $route：我在哪里（信息获取）
  简单记忆 💡
- $router：动词，执行操作 → push(), go(), back()
- $route：名词，获取信息 → params, query, path

```js
// $router - 路由跳转
this.$router.push('/user/123')

// $route - 获取参数
const userId = this.$route.params.id
```

$router详解 - 路由器实例

```js
export default {
  methods: {
    // 🎯 编程式导航 - 添加新的历史记录
    goToUser() {
      this.$router.push('/user/123')
      this.$router.push({ name: 'User', params: { id: 123 } })
      this.$router.push({ path: '/user', query: { tab: 'profile' } })
    },

    // 🎯 替换当前历史记录
    replaceRoute() {
      this.$router.replace('/login')
    },

    // 🎯 历史记录导航
    goBack() {
      this.$router.back() // 后退一步
      this.$router.forward() // 前进一步
      this.$router.go(-2) // 后退两步
      this.$router.go(1) // 前进一步
    },

    // 🎯 获取路由信息
    getRouteInfo() {
      console.log('总路由数:', this.$router.options.routes.length)
      console.log('当前模式:', this.$router.mode)
    },
  },
}
```

$router的实际应用

```js
<template>
  <div>
    <!-- 🎯 条件性导航 -->
    <button @click="handleSubmit">提交表单</button>
    <button @click="goToPreviousPage">返回上一页</button>
    <button @click="goToUserProfile">查看个人资料</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {}
    }
  },
  methods: {
    // 🎯 表单提交后跳转
    async handleSubmit() {
      try {
        await this.submitForm(this.formData)
        // 成功后跳转到成功页面
        this.$router.push({
          name: 'Success',
          query: { message: '提交成功' }
        })
      } catch (error) {
        // 失败时跳转到错误页面
        this.$router.push({
          name: 'Error',
          query: { error: error.message }
        })
      }
    },

    // 🎯 智能返回上一页
    goToPreviousPage() {
      // 如果有历史记录就后退，否则跳转到首页
      if (window.history.length > 1) {
        this.$router.back()
      } else {
        this.$router.push('/')
      }
    },

    // 🎯 根据权限跳转
    goToUserProfile() {
      if (this.isLoggedIn) {
        this.$router.push('/profile')
      } else {
        this.$router.push('/login')
      }
    }
  }
}
</script>
```

$route详解 - 路由信息对象

```js
export default {
  created() {
    // 🎯 当前路由的完整信息
    console.log('完整路由对象:', this.$route)

    // 🎯 路径信息
    console.log('当前路径:', this.$route.path) // /user/123
    console.log('完整路径:', this.$route.fullPath) // /user/123?tab=profile
    console.log('路由名称:', this.$route.name) // 'User'

    // 🎯 参数信息
    console.log('路径参数:', this.$route.params) // { id: '123' }
    console.log('查询参数:', this.$route.query) // { tab: 'profile' }
    console.log('哈希值:', this.$route.hash) // #section1

    // 🎯 匹配信息
    console.log('匹配的路由记录:', this.$route.matched)
    console.log('路由元信息:', this.$route.meta)
  },

  watch: {
    // 🎯 监听路由变化
    $route(to, from) {
      console.log('路由从', from.path, '跳转到', to.path)
      this.loadData(to.params.id)
    },
  },
}
```

Vue 3 Composition API用法

```vue
<script setup>
import { useRoute, useRouter } from 'vue-router'
import { computed, watch } from 'vue'

// 🎯 获取路由相关对象
const route = useRoute()
const router = useRouter()

// 🎯 响应式计算属性
const userId = computed(() => route.params.id)
const searchQuery = computed(() => route.query.search)

// 🎯 监听路由变化
watch(
  () => route.params.id,
  (newId) => {
    console.log('用户ID变化:', newId)
    loadUserData(newId)
  }
)

// 🎯 编程式导航
const goToHome = () => {
  router.push('/')
}

const updateQuery = (newQuery) => {
  router.push({
    path: route.path,
    query: { ...route.query, ...newQuery },
  })
}
</script>
```

商品详情页面

```vue
<script>
export default {
  data() {
    return {
      product: null,
      loading: false,
    }
  },

  computed: {
    // 🎯 使用$route获取商品ID
    productId() {
      return this.$route.params.id
    },

    // 🎯 获取当前选中的规格
    selectedSpec() {
      return this.$route.query.spec || 'default'
    },
  },

  methods: {
    // 🎯 使用$router进行页面操作
    addToCart() {
      // 添加到购物车后跳转
      this.addProductToCart(this.product)
      this.$router.push('/cart')
    },

    buyNow() {
      // 立即购买，跳转到订单页面
      this.$router.push({
        name: 'Order',
        query: {
          productId: this.productId,
          spec: this.selectedSpec,
          quantity: 1,
        },
      })
    },

    changeSpec(spec) {
      // 更新商品规格（更新查询参数）
      this.$router.replace({
        params: this.$route.params,
        query: { ...this.$route.query, spec },
      })
    },
  },

  watch: {
    // 🎯 监听商品ID变化
    productId: {
      immediate: true,
      handler(newId) {
        this.loadProduct(newId)
      },
    },
  },
}
</script>
```

记忆技巧

```js
// 🎯 记忆口诀：
// $router = 路由器 = 司机 = 负责开车（导航）
// $route = 路线 = 地图 = 显示位置（信息）

// 实际使用中的思维模式：
// 想要去某个地方 → 使用 $router
// 想知道当前位置 → 使用 $route

// 代码示例：
// 我要去用户页面
this.$router.push('/user/123')

// 我现在在哪个用户页面
const userId = this.$route.params.id
```

:::

## 如何安装和配置Vue Router？

:::details
Vue Router的安装和配置分为安装依赖、创建路由配置、注册到Vue应用三个步骤。

```js
# Vue 3项目
npm install vue-router@4

# Vue 2项目
npm install vue-router@3
```

快速配置

```js
// 1. 创建路由配置
import { createRouter, createWebHistory } from 'vue-router'
const router = createRouter({
  history: createWebHistory(),
  routes: [
    { path: '/', component: Home },
    { path: '/about', component: About }
  ]
})

// 2. 注册到应用
app.use(router)

// 3. 模板中使用
<router-view />
```

安装方式详解

```js
# 🎯 使用npm安装
npm install vue-router@4          # Vue 3版本
npm install vue-router@3          # Vue 2版本

# 🎯 使用yarn安装
yarn add vue-router@4

# 🎯 使用pnpm安装
pnpm add vue-router@4

# 🎯 安装指定版本
npm install vue-router@4.2.5
```

vue3项目结构组织

```bash
src/
├── main.js              # 应用入口
├── App.vue              # 根组件
├── router/
│   └── index.js         # 路由配置文件
└── views/               # 页面组件
    ├── Home.vue
    ├── About.vue
    └── User.vue
```

应用入口配置

```js
// src/main.js
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'

// 🎯 创建Vue应用实例
const app = createApp(App)

// 🎯 注册路由插件
app.use(router)

// 🎯 挂载应用
app.mount('#app')
```

根组件模板

```js
<!-- src/App.vue -->
<template>
  <div id="app">
    <!-- 🎯 导航菜单 -->
    <nav>
      <router-link to="/">首页</router-link>
      <router-link to="/about">关于</router-link>
      <router-link :to="{ name: 'User', params: { id: 123 }}">
        用户详情
      </router-link>
    </nav>

    <!-- 🎯 路由出口 -->
    <router-view />
  </div>
</template>

<style>
.router-link-active {
  color: #42b983;
  font-weight: bold;
}
</style>
```

Vue 2路由配置差异

```js
// Vue 2 路由配置
import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '@/views/Home.vue'

// 🎯 安装插件
Vue.use(VueRouter)

// 🎯 定义路由
const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home,
  },
  {
    path: '/about',
    name: 'About',
    component: () => import('@/views/About.vue'),
  },
]

// 🎯 创建路由实例
const router = new VueRouter({
  mode: 'history', // Vue 2中使用mode属性
  base: process.env.BASE_URL,
  routes,
})

export default router
```

```js
// Vue 2 main.js
import Vue from 'vue'
import App from './App.vue'
import router from './router'

Vue.config.productionTip = false

// 🎯 创建Vue实例
new Vue({
  router,
  render: (h) => h(App),
}).$mount('#app')
```

- 高级配置选项
  完整配置参数

```js
const router = createRouter({
  // 🎯 历史模式配置
  history: createWebHistory('/app/'),

  // 🎯 路由表
  routes,

  // 🎯 滚动行为
  scrollBehavior(to, from, savedPosition) {
    if (to.hash) {
      return { el: to.hash, behavior: 'smooth' }
    }
    if (savedPosition) {
      return savedPosition
    }
    return { top: 0 }
  },

  // 🎯 路由解析配置
  parseQuery: (query) => {
    // 自定义查询参数解析
    return JSON.parse(query)
  },

  stringifyQuery: (query) => {
    // 自定义查询参数序列化
    return JSON.stringify(query)
  },
})
```

环境配置优化 🌍

```js
// 🎯 根据环境动态配置
const router = createRouter({
  history: process.env.NODE_ENV === 'production' ? createWebHistory('/app/') : createWebHashHistory(),
  routes,

  // 🎯 开发环境启用严格模式
  strict: process.env.NODE_ENV !== 'production',
})

// 🎯 开发环境路由调试
if (process.env.NODE_ENV === 'development') {
  router.beforeEach((to, from, next) => {
    console.log('路由跳转:', from.path, '→', to.path)
    next()
  })
}
```

常见配置问题

- TypeScript配置 📝

```js
// router/index.ts
import { createRouter, createWebHistory, RouteRecordRaw } from 'vue-router'

// 🎯 类型定义
const routes: Array<RouteRecordRaw> = [
  {
    path: '/',
    name: 'Home',
    component: () => import('@/views/Home.vue')
  }
]

const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes
})

export default router
```

Vite项目配置 ⚡

```js
// vite.config.js
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import { resolve } from 'path'

export default defineConfig({
  plugins: [vue()],
  resolve: {
    alias: {
      '@': resolve(__dirname, 'src'),
    },
  },
  // 🎯 开发服务器配置
  server: {
    historyApiFallback: true, // 支持history模式
  },
})
```

安装验证方法 ✅

```js
// 🎯 检查路由是否正确安装
console.log('Vue Router版本:', router.options.version)

// 🎯 在组件中验证路由功能
export default {
  mounted() {
    console.log('当前路由:', this.$route.path)
    console.log('路由器实例:', this.$router)
  }
}

// 🎯 Composition API中验证
import { useRoute, useRouter } from 'vue-router'

export default {
  setup() {
    const route = useRoute()
    const router = useRouter()

    console.log('路由安装成功:', !!route && !!router)
  }
}
```

快速启动模板 🚀

```bash
# 🎯 使用Vue CLI创建项目（自动配置路由）
vue create my-project
# 选择 "Manually select features"
# 勾选 "Router"

# 🎯 使用Vite创建项目
npm create vue@latest my-project
# 选择 "Add Vue Router for Single Page Application development"
```
:::
## 🔥如何获取路由参数？
::: details
Vue Router中获取路由参数主要通过**$route对象**，包含params路径参数和query查询参数两种方式。

获取方式 🎯
- 路径参数：this.$route.params.参数名
- 查询参数：this.$route.query.参数名
- Vue3方式：useRoute().params 或 useRoute().query

```js
// 路径参数：/user/123
const userId = this.$route.params.id

// 查询参数：/user?tab=profile&page=1  
const tab = this.$route.query.tab
const page = this.$route.query.page
```
响应式获取
```js
// 计算属性方式（推荐）
computed: {
  userId() {
    return this.$route.params.id
  }
}
```
- 基础获取方式 🎯
```js
<template>
  <div>
    <h1>用户ID: {{ userId }}</h1>
    <h2>文章ID: {{ postId }}</h2>
    <p>完整路径: {{ $route.path }}</p>
  </div>
</template>

<script>
// 路由配置: /user/:id/post/:postId
export default {
  created() {
    // 🎯 直接获取
    console.log('用户ID:', this.$route.params.id)
    console.log('文章ID:', this.$route.params.postId)
    console.log('所有路径参数:', this.$route.params)
  },
  
  computed: {
    // 🎯 响应式获取（推荐）
    userId() {
      return this.$route.params.id
    },
    
    postId() {
      return this.$route.params.postId
    }
  }
}
</script>
```
- 参数类型处理 🔧
```js
export default {
  computed: {
    // 🎯 转换为数字类型
    userId() {
      return parseInt(this.$route.params.id) || 0
    },
    
    // 🎯 默认值处理
    categoryId() {
      return this.$route.params.categoryId || 'default'
    },
    
    // 🎯 参数验证
    validUserId() {
      const id = parseInt(this.$route.params.id)
      return id > 0 ? id : null
    }
  }
}
```
- 多种查询参数处理 📊
```js
<template>
  <div>
    <h2>搜索关键词: {{ searchKeyword }}</h2>
    <p>当前页码: {{ currentPage }}</p>
    <p>排序方式: {{ sortBy }}</p>
    <p>是否显示高级选项: {{ showAdvanced }}</p>
  </div>
</template>

<script>
// URL示例: /search?keyword=vue&page=2&sort=date&advanced=true
export default {
  computed: {
    // 🎯 字符串参数
    searchKeyword() {
      return this.$route.query.keyword || ''
    },
    
    // 🎯 数字参数
    currentPage() {
      return parseInt(this.$route.query.page) || 1
    },
    
    // 🎯 枚举参数
    sortBy() {
      const sort = this.$route.query.sort
      const validSorts = ['date', 'title', 'views']
      return validSorts.includes(sort) ? sort : 'date'
    },
    
    // 🎯 布尔参数
    showAdvanced() {
      return this.$route.query.advanced === 'true'
    },
    
    // 🎯 数组参数
    selectedTags() {
      const tags = this.$route.query.tags
      if (!tags) return []
      return Array.isArray(tags) ? tags : [tags]
    }
  }
}
</script>
```
- useRoute Hook使用 🪝
```js
<script setup>
import { useRoute } from 'vue-router'
import { computed, watch } from 'vue'

const route = useRoute()

// 🎯 响应式获取参数
const userId = computed(() => route.params.id)
const searchQuery = computed(() => route.query.search || '')
const currentPage = computed(() => parseInt(route.query.page) || 1)

// 🎯 监听参数变化
watch(userId, (newId, oldId) => {
  console.log(`用户ID从 ${oldId} 变为 ${newId}`)
  loadUserData(newId)
})

watch(
  () => route.query,
  (newQuery) => {
    console.log('查询参数变化:', newQuery)
    performSearch(newQuery)
  },
  { deep: true }
)

// 🎯 组合多个参数
const searchParams = computed(() => ({
  keyword: route.query.keyword || '',
  category: route.query.category || 'all',
  page: parseInt(route.query.page) || 1,
  limit: parseInt(route.query.limit) || 10
}))
</script>
```
实际应用场景 🎪
- 电商商品详情页 🛒
```js
<template>
  <div class="product-detail">
    <h1>{{ product.name }}</h1>
    
    <!-- 🎯 规格选择 -->
    <div class="specs">
      <button 
        v-for="spec in product.specs"
        :key="spec.id"
        :class="{ active: spec.id === selectedSpecId }"
        @click="selectSpec(spec.id)">
        {{ spec.name }}
      </button>
    </div>
    
    <!-- 🎯 评论区域 -->
    <div class="comments">
      <div class="comment-filters">
        <button 
          v-for="filter in commentFilters"
          :key="filter.value"
          :class="{ active: filter.value === currentCommentFilter }"
          @click="filterComments(filter.value)">
          {{ filter.label }}
        </button>
      </div>
      
      <div class="pagination">
        <button 
          v-for="page in totalPages"
          :key="page"
          :class="{ active: page === commentPage }"
          @click="goToCommentPage(page)">
          {{ page }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
// 路由: /product/:id?spec=color&comment_filter=all&comment_page=1
export default {
  data() {
    return {
      product: null,
      commentFilters: [
        { label: '全部', value: 'all' },
        { label: '好评', value: 'positive' },
        { label: '中评', value: 'neutral' },
        { label: '差评', value: 'negative' }
      ]
    }
  },
  
  computed: {
    // 🎯 获取商品ID
    productId() {
      return this.$route.params.id
    },
    
    // 🎯 获取选中的规格
    selectedSpecId() {
      return this.$route.query.spec || 'default'
    },
    
    // 🎯 获取评论过滤条件
    currentCommentFilter() {
      return this.$route.query.comment_filter || 'all'
    },
    
    // 🎯 获取评论页码
    commentPage() {
      return parseInt(this.$route.query.comment_page) || 1
    }
  },
  
  methods: {
    // 🎯 选择规格
    selectSpec(specId) {
      this.$router.push({
        params: this.$route.params,
        query: {
          ...this.$route.query,
          spec: specId
        }
      })
    },
    
    // 🎯 过滤评论
    filterComments(filter) {
      this.$router.push({
        params: this.$route.params,
        query: {
          ...this.$route.query,
          comment_filter: filter,
          comment_page: 1  // 重置页码
        }
      })
    },
    
    // 🎯 评论分页
    goToCommentPage(page) {
      this.$router.push({
        params: this.$route.params,
        query: {
          ...this.$route.query,
          comment_page: page
        }
      })
    }
  },
  
  watch: {
    // 🎯 监听商品ID变化
    productId: {
      immediate: true,
      handler(newId) {
        this.loadProduct(newId)
      }
    },
    
    // 🎯 监听查询参数变化
    '$route.query': {
      handler(newQuery) {
        this.loadComments(newQuery)
      }
    }
  }
}
</script>
```
用户管理列表页 👥
```js
<template>
  <div class="user-management">
    <!-- 🎯 搜索和过滤 -->
    <div class="filters">
      <input 
        v-model="searchForm.keyword"
        @input="debounceSearch"
        placeholder="搜索用户名或邮箱">
      
      <select v-model="searchForm.status" @change="applyFilters">
        <option value="">全部状态</option>
        <option value="active">激活</option>
        <option value="inactive">未激活</option>
        <option value="banned">已封禁</option>
      </select>
      
      <select v-model="searchForm.role" @change="applyFilters">
        <option value="">全部角色</option>
        <option value="admin">管理员</option>
        <option value="user">普通用户</option>
        <option value="vip">VIP用户</option>
      </select>
    </div>
    
    <!-- 🎯 用户列表 -->
    <div class="user-list">
      <div v-for="user in users" :key="user.id" class="user-item">
        <router-link :to="{ name: 'UserDetail', params: { id: user.id }}">
          {{ user.name }}
        </router-link>
      </div>
    </div>
    
    <!-- 🎯 分页 -->
    <div class="pagination">
      <button 
        v-for="page in totalPages"
        :key="page"
        :class="{ active: page === currentPage }"
        @click="goToPage(page)">
        {{ page }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: [],
      totalPages: 0,
      searchForm: {
        keyword: '',
        status: '',
        role: '',
        page: 1,
        limit: 20
      }
    }
  },
  
  computed: {
    // 🎯 从URL同步搜索条件
    currentPage() {
      return parseInt(this.$route.query.page) || 1
    }
  },
  
  created() {
    // 🎯 初始化时从URL获取搜索条件
    this.syncFromRoute()
  },
  
  methods: {
    // 🎯 从路由同步搜索条件
    syncFromRoute() {
      const query = this.$route.query
      this.searchForm = {
        keyword: query.keyword || '',
        status: query.status || '',
        role: query.role || '',
        page: parseInt(query.page) || 1,
        limit: parseInt(query.limit) || 20
      }
    },
    
    // 🎯 应用过滤条件
    applyFilters() {
      this.$router.push({
        path: this.$route.path,
        query: {
          ...this.searchForm,
          page: 1  // 重置页码
        }
      })
    },
    
    // 🎯 防抖搜索
    debounceSearch: debounce(function() {
      this.applyFilters()
    }, 300),
    
    // 🎯 分页跳转
    goToPage(page) {
      this.$router.push({
        path: this.$route.path,
        query: {
          ...this.$route.query,
          page
        }
      })
    }
  },
  
  watch: {
    // 🎯 监听路由变化，重新加载数据
    '$route.query': {
      immediate: true,
      handler() {
        this.syncFromRoute()
        this.loadUsers()
      }
    }
  }
}
</script>
```
- 错误处理和验证 ⚠️
```js
export default {
  computed: {
    // 🎯 安全的参数获取
    safeUserId() {
      const id = this.$route.params.id
      
      // 参数存在性检查
      if (!id) {
        this.$router.push('/404')
        return null
      }
      
      // 类型转换和验证
      const numId = parseInt(id)
      if (isNaN(numId) || numId <= 0) {
        this.$router.push('/400')
        return null
      }
      
      return numId
    },
    
    // 🎯 查询参数的默认值处理
    searchFilters() {
      const query = this.$route.query
      return {
        keyword: query.keyword || '',
        category: query.category || 'all',
        sortBy: ['date', 'name', 'price'].includes(query.sort) 
          ? query.sort 
          : 'date',
        page: Math.max(1, parseInt(query.page) || 1),
        limit: [10, 20, 50].includes(parseInt(query.limit)) 
          ? parseInt(query.limit) 
          : 20
      }
    }
  }
}
```
性能优化技巧 ⚡
```js
// 🎯 缓存计算结果
export default {
  computed: {
    expensiveUserData() {
      // 复杂的用户数据计算
      return this.processUserData(this.$route.params.id)
    }
  },
  
  // 🎯 使用防抖处理频繁的参数变化
  watch: {
    '$route.query.search': {
      handler: debounce(function(newSearch) {
        this.performSearch(newSearch)
      }, 300)
    }
  }
}
```
掌握路由参数的获取方法，是Vue开发中的基本技能！记住：params用于路径参数，query用于查询参数，计算属性是最佳的响应式获取方式。

:::
## 🔥什么是动态路由匹配？如何实现？

::: details

动态路由匹配是Vue Router中使用参数化路径来匹配多个相似路由的技术，通过在路径中使用冒号(:)定义参数。

核心概念 🎯
- 路径参数：用:定义可变部分，如/user/:id
- 参数获取：通过$route.params获取参数值
- 灵活匹配：一个路由规则可以匹配多个具体路径
```js
// 路由配置
const routes = [
  { path: '/user/:id', component: User }
]

// 匹配结果
'/user/123' → { id: '123' }
'/user/456' → { id: '456' }

// 获取参数
const userId = this.$route.params.id
```
基础语法和规则 📝
- 单参数匹配 🎯
```js
// 🎯 基础动态路由
const routes = [
  {
    path: '/user/:id',
    name: 'User',
    component: UserProfile
  }
]

// 匹配示例
'/user/123'     // ✅ { id: '123' }
'/user/abc'     // ✅ { id: 'abc' }
'/user/123/456' // ❌ 不匹配
'/user'         // ❌ 不匹配
```
多参数匹配 🎪
```js
// 🎯 多个路径参数
const routes = [
  {
    path: '/user/:userId/post/:postId',
    name: 'UserPost',
    component: PostDetail
  },
  {
    path: '/category/:type/product/:id',
    name: 'Product',
    component: ProductDetail
  }
]

// 匹配示例
'/user/123/post/456'        // ✅ { userId: '123', postId: '456' }
'/category/electronics/product/789' // ✅ { type: 'electronics', id: '789' }
```
高级匹配模式 💡
- 正则表达式约束 🔧
```js
// 🎯 使用正则表达式限制参数格式
const routes = [
  {
    // 只匹配数字ID
    path: '/user/:id(\\d+)',
    name: 'User',
    component: UserProfile
  },
  {
    // 只匹配字母用户名
    path: '/profile/:username([a-zA-Z]+)',
    name: 'Profile',
    component: UserProfile
  },
  {
    // 自定义正则模式
    path: '/article/:slug([a-z0-9-]+)',
    name: 'Article',
    component: ArticleDetail
  }
]

// 匹配示例
'/user/123'     // ✅ 数字ID匹配
'/user/abc'     // ❌ 不是数字
'/profile/john' // ✅ 字母用户名匹配
'/profile/123'  // ❌ 不是字母
```
重复参数匹配 🔄
```js
// 🎯 匹配多个路径段
const routes = [
  {
    // 匹配一个或多个段
    path: '/files/:path+',
    name: 'Files',
    component: FileExplorer
  },
  {
    // 匹配零个或多个段
    path: '/docs/:path*',
    name: 'Docs',
    component: Documentation
  }
]

// 匹配示例
'/files/folder1'              // ✅ { path: ['folder1'] }
'/files/folder1/folder2'      // ✅ { path: ['folder1', 'folder2'] }
'/files/folder1/folder2/file.txt' // ✅ { path: ['folder1', 'folder2', 'file.txt'] }
'/docs'                       // ✅ { path: [] }
'/docs/guide'                 // ✅ { path: ['guide'] }
```
实际应用场景 🚀
- 电商网站商品页 🛒
```js
<template>
  <div class="product-detail">
    <div v-if="loading">加载中...</div>
    <div v-else-if="product">
      <h1>{{ product.name }}</h1>
      <p>分类: {{ categoryName }}</p>
      <p>商品ID: {{ productId }}</p>
      <p>规格: {{ selectedSpec }}</p>
      
      <!-- 🎯 相关商品导航 -->
      <div class="related-products">
        <router-link 
          v-for="item in relatedProducts"
          :key="item.id"
          :to="{ 
            name: 'Product', 
            params: { category: categoryType, id: item.id }
          }">
          {{ item.name }}
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
// 路由配置: /category/:category/product/:id
export default {
  data() {
    return {
      product: null,
      relatedProducts: [],
      loading: false
    }
  },
  
  computed: {
    // 🎯 从路由参数获取分类
    categoryType() {
      return this.$route.params.category
    },
    
    // 🎯 从路由参数获取商品ID
    productId() {
      return this.$route.params.id
    },
    
    // 🎯 从查询参数获取规格
    selectedSpec() {
      return this.$route.query.spec || 'default'
    },
    
    // 🎯 分类名称映射
    categoryName() {
      const categories = {
        'electronics': '电子产品',
        'clothing': '服装',
        'books': '图书'
      }
      return categories[this.categoryType] || '未知分类'
    }
  },
  
  methods: {
    async loadProduct() {
      this.loading = true
      try {
        // 🎯 根据分类和ID加载商品
        this.product = await this.fetchProduct(
          this.categoryType, 
          this.productId
        )
        this.relatedProducts = await this.fetchRelatedProducts(
          this.categoryType
        )
      } catch (error) {
        this.$router.push('/404')
      } finally {
        this.loading = false
      }
    }
  },
  
  watch: {
    // 🎯 监听路由参数变化
    '$route.params': {
      immediate: true,
      handler() {
        this.loadProduct()
      }
    }
  }
}
</script>
```
- 用户管理系统 👥
```js
<template>
  <div class="user-management">
    <!-- 🎯 面包屑导航 -->
    <nav class="breadcrumb">
      <router-link to="/admin">管理后台</router-link>
      <span>></span>
      <router-link to="/admin/users">用户管理</router-link>
      <span>></span>
      <span v-if="isUserDetail">用户详情 {{ userId }}</span>
      <span v-else-if="isUserEdit">编辑用户 {{ userId }}</span>
    </nav>
    
    <!-- 🎯 用户操作导航 -->
    <div class="user-tabs" v-if="userId">
      <router-link 
        :to="{ name: 'UserDetail', params: { id: userId }}"
        :class="{ active: currentAction === 'detail' }">
        基本信息
      </router-link>
      <router-link 
        :to="{ name: 'UserEdit', params: { id: userId }}"
        :class="{ active: currentAction === 'edit' }">
        编辑资料
      </router-link>
      <router-link 
        :to="{ name: 'UserOrders', params: { id: userId }}"
        :class="{ active: currentAction === 'orders' }">
        订单历史
      </router-link>
    </div>
    
    <!-- 🎯 内容区域 -->
    <router-view />
  </div>
</template>

<script>
export default {
  computed: {
    // 🎯 获取用户ID
    userId() {
      return this.$route.params.id
    },
    
    // 🎯 获取当前操作类型
    currentAction() {
      return this.$route.params.action
    },
    
    // 🎯 判断是否为用户详情页
    isUserDetail() {
      return this.$route.name === 'UserDetail'
    },
    
    // 🎯 判断是否为用户编辑页
    isUserEdit() {
      return this.$route.name === 'UserEdit'
    }
  }
}

// 🎯 路由配置
const routes = [
  {
    path: '/admin/users/:id',
    name: 'UserDetail',
    component: UserDetail
  },
  {
    path: '/admin/users/:id/edit',
    name: 'UserEdit',
    component: UserEdit
  },
  {
    path: '/admin/users/:id/orders',
    name: 'UserOrders',
    component: UserOrders
  }
]
</script>
```
匹配优先级和注意事项 ⚠️
```js
// 🎯 路由定义顺序很重要
const routes = [
  // ✅ 静态路由放在前面
  { path: '/user/profile', component: UserProfile },
  { path: '/user/settings', component: UserSettings },
  
  // ✅ 动态路由放在后面
  { path: '/user/:id', component: UserDetail },
  
  // ❌ 错误：这个规则永远不会被匹配到
  { path: '/user/admin', component: AdminPanel }
]
```
- 参数验证和错误处理 🔧
```js
export default {
  computed: {
    validUserId() {
      const id = this.$route.params.id
      
      // 🎯 参数验证
      if (!id) return null
      
      const numId = parseInt(id)
      if (isNaN(numId) || numId <= 0) {
        // 无效ID，跳转到错误页面
        this.$router.replace('/404')
        return null
      }
      
      return numId
    }
  },
  
  watch: {
    validUserId: {
      immediate: true,
      handler(id) {
        if (id) {
          this.loadUserData(id)
        }
      }
    }
  }
}
```
Vue 3动态路由用法 💫
```vue
<script setup>
import { useRoute, useRouter } from 'vue-router'
import { computed, watch } from 'vue'

const route = useRoute()
const router = useRouter()

// 🎯 响应式参数获取
const articleId = computed(() => route.params.id)
const categorySlug = computed(() => route.params.category)

// 🎯 参数验证
const validArticleId = computed(() => {
  const id = parseInt(articleId.value)
  return !isNaN(id) && id > 0 ? id : null
})

// 🎯 监听参数变化
watch(validArticleId, async (newId) => {
  if (newId) {
    await loadArticle(newId)
  } else {
    router.push('/404')
  }
}, { immediate: true })

// 🎯 导航到相关文章
const goToRelatedArticle = (id) => {
  router.push({
    name: 'Article',
    params: {
      category: categorySlug.value,
      id: id
    }
  })
}
</script>
```
性能优化建议 ⚡

优化策略	实现方法	效果
参数缓存	使用computed缓存解析结果	🚀 减少重复计算
路由懒加载	动态import组件	🚀 按需加载
参数验证	早期验证，快速失败	🚀 避免无效请求
预加载	预获取相关数据	🚀 提升用户体验

```js
// 🎯 性能优化示例
export default {
  computed: {
    // 缓存参数解析
    parsedParams() {
      return {
        userId: parseInt(this.$route.params.id),
        category: this.$route.params.category,
        page: parseInt(this.$route.query.page) || 1
      }
    }
  },
  
  asyncData({ params }) {
    // 🎯 SSR中的参数处理
    return {
      user: await fetchUser(params.id),
      posts: await fetchUserPosts(params.id)
    }
  }
}
```
动态路由匹配是Vue Router的核心特性，掌握它就能构建出灵活且用户友好的单页应用！记住：合理的路由设计不仅能提升用户体验，还能让代码更加优雅和可维护。


::: 
## 什么是嵌套路由？如何配置？

::: details
嵌套路由是Vue Router中通过children属性实现路由层级嵌套的功能，允许在父组件内部渲染子路由组件。

核心概念 🎯
- 父子关系：路由之间存在层级关系，子路由在父路由内部渲染
- children配置：通过children数组定义子路由
- 多级router-view：父组件包含<router-view/>来渲染子组件
- 基础配置 ⚡
```js
const routes = [
  {
    path: '/admin',
    component: AdminLayout,
    children: [
      { path: '', component: Dashboard },        // /admin
      { path: 'users', component: UserList },    // /admin/users
      { path: 'settings', component: Settings }  // /admin/settings
    ]
  }
]
```
使用场景 📋
- 管理后台、用户中心、多级菜单等需要保持公共布局的页面结构。

详细解析📚
- 嵌套路由结构图 🏗️
- 基础配置详解 📋
- 完整路由配置 🎯
```js
// router/index.js
import { createRouter, createWebHistory } from 'vue-router'

const routes = [
  {
    path: '/',
    name: 'Home',
    component: () => import('@/views/Home.vue')
  },
  {
    path: '/admin',
    component: () => import('@/layouts/AdminLayout.vue'),
    // 🎯 重定向到默认子路由
    redirect: '/admin/dashboard',
    children: [
      {
        path: 'dashboard',  // 注意：子路由路径不加 /
        name: 'Dashboard',
        component: () => import('@/views/admin/Dashboard.vue')
      },
      {
        path: 'users',
        name: 'UserManagement',
        component: () => import('@/views/admin/UserList.vue')
      },
      {
        path: 'users/:id',
        name: 'UserDetail',
        component: () => import('@/views/admin/UserDetail.vue')
      },
      {
        path: 'settings',
        name: 'Settings',
        component: () => import('@/views/admin/Settings.vue')
      }
    ]
  }
]

export default createRouter({
  history: createWebHistory(),
  routes
})
```
父组件布局实现 🎨
```vue
<!-- layouts/AdminLayout.vue -->
<template>
  <div class="admin-layout">
    <!-- 🎯 公共头部 -->
    <header class="admin-header">
      <div class="logo">管理后台</div>
      <nav class="main-nav">
        <router-link to="/admin/dashboard">仪表盘</router-link>
        <router-link to="/admin/users">用户管理</router-link>
        <router-link to="/admin/settings">系统设置</router-link>
      </nav>
      <div class="user-info">
        <span>欢迎，{{ currentUser.name }}</span>
      </div>
    </header>
    
    <!-- 🎯 主要内容区域 -->
    <div class="admin-main">
      <!-- 侧边栏 -->
      <aside class="admin-sidebar">
        <nav class="sidebar-nav">
          <div class="nav-group">
            <h3>数据统计</h3>
            <router-link to="/admin/dashboard" exact>
              <Icon name="dashboard" />
              仪表盘
            </router-link>
          </div>
          
          <div class="nav-group">
            <h3>用户管理</h3>
            <router-link to="/admin/users">
              <Icon name="users" />
              用户列表
            </router-link>
            <router-link to="/admin/users/create">
              <Icon name="user-plus" />
              添加用户
            </router-link>
          </div>
          
          <div class="nav-group">
            <h3>系统管理</h3>
            <router-link to="/admin/settings">
              <Icon name="settings" />
              系统设置
            </router-link>
          </div>
        </nav>
      </aside>
      
      <!-- 🎯 子路由渲染区域 -->
      <main class="admin-content">
        <!-- 面包屑导航 -->
        <nav class="breadcrumb">
          <router-link to="/admin">首页</router-link>
          <span class="separator">></span>
          <span>{{ $route.meta.title || $route.name }}</span>
        </nav>
        
        <!-- 子组件渲染出口 -->
        <router-view />
      </main>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const currentUser = { name: 'Admin' }

// 🎯 动态计算当前页面标题
const pageTitle = computed(() => {
  return route.meta?.title || route.name || '管理后台'
})
</script>

<style scoped>
.admin-layout {
  display: flex;
  flex-direction: column;
  height: 100vh;
}

.admin-header {
  height: 60px;
  background: #001529;
  color: white;
  display: flex;
  align-items: center;
  padding: 0 20px;
}

.admin-main {
  flex: 1;
  display: flex;
}

.admin-sidebar {
  width: 250px;
  background: #f0f2f5;
  padding: 20px 0;
}

.admin-content {
  flex: 1;
  padding: 20px;
  background: white;
}

.router-link-active {
  background-color: #1890ff;
  color: white;
}
</style>
```
- 多级嵌套路由 🎪
- 三级路由配置 📊
```js
const routes = [
  {
    path: '/admin',
    component: AdminLayout,
    children: [
      {
        path: 'users',
        component: UserLayout,  // 🎯 二级布局组件
        children: [
          {
            path: '',
            name: 'UserList',
            component: UserList
          },
          {
            path: ':id',
            component: UserDetailLayout,  // 🎯 三级布局组件
            children: [
              {
                path: '',
                name: 'UserProfile',
                component: UserProfile
              },
              {
                path: 'edit',
                name: 'UserEdit',
                component: UserEdit
              },
              {
                path: 'orders',
                name: 'UserOrders',
                component: UserOrders
              }
            ]
          }
        ]
      }
    ]
  }
]

// URL结构：
// /admin/users              → UserList
// /admin/users/123          → UserProfile
// /admin/users/123/edit     → UserEdit
// /admin/users/123/orders   → UserOrders
```
二级布局组件 🔧
```vue
<!-- components/UserLayout.vue -->
<template>
  <div class="user-layout">
    <!-- 🎯 用户管理专用工具栏 -->
    <div class="user-toolbar">
      <div class="toolbar-left">
        <h2>用户管理</h2>
        <div class="quick-actions">
          <router-link to="/admin/users" class="btn btn-primary">
            <Icon name="list" />
            用户列表
          </router-link>
          <router-link to="/admin/users/create" class="btn btn-success">
            <Icon name="plus" />
            添加用户
          </router-link>
        </div>
      </div>
      
      <div class="toolbar-right">
        <input 
          type="search" 
          placeholder="搜索用户..."
          @input="handleSearch">
      </div>
    </div>
    
    <!-- 🎯 用户管理子路由出口 -->
    <div class="user-content">
      <router-view />
    </div>
  </div>
</template>
```
实际应用场景 🚀
- 电商管理后台 🛒
```vue
<!-- 商品管理嵌套路由示例 -->
<template>
  <div class="product-management">
    <!-- 🎯 商品管理导航 -->
    <nav class="product-nav">
      <router-link to="/admin/products" exact>商品列表</router-link>
      <router-link to="/admin/products/categories">分类管理</router-link>
      <router-link to="/admin/products/inventory">库存管理</router-link>
      <router-link to="/admin/products/analytics">销售分析</router-link>
    </nav>
    
    <!-- 🎯 当前路径显示 -->
    <div class="current-path">
      <span>当前位置：{{ currentPath }}</span>
    </div>
    
    <!-- 🎯 商品管理内容区域 -->
    <div class="product-content">
      <router-view />
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    currentPath() {
      const pathMap = {
        '/admin/products': '商品列表',
        '/admin/products/categories': '分类管理',
        '/admin/products/inventory': '库存管理',
        '/admin/products/analytics': '销售分析'
      }
      return pathMap[this.$route.path] || '商品管理'
    }
  }
}

// 🎯 对应的路由配置
const routes = [
  {
    path: '/admin',
    component: AdminLayout,
    children: [
      {
        path: 'products',
        component: ProductLayout,
        children: [
          { path: '', name: 'ProductList', component: ProductList },
          { path: 'categories', name: 'Categories', component: CategoryManagement },
          { path: 'inventory', name: 'Inventory', component: InventoryManagement },
          { path: 'analytics', name: 'Analytics', component: SalesAnalytics },
          {
            path: ':id',
            name: 'ProductDetail',
            component: ProductDetail,
            children: [
              { path: '', name: 'ProductInfo', component: ProductInfo },
              { path: 'edit', name: 'ProductEdit', component: ProductEdit },
              { path: 'variants', name: 'ProductVariants', component: ProductVariants }
            ]
          }
        ]
      }
    ]
  }
]
</script>
```
用户中心模块 👤
```vue
<!-- 用户中心嵌套路由 -->
<template>
  <div class="user-center">
    <!-- 🎯 用户信息卡片 -->
    <div class="user-card">
      <img :src="userInfo.avatar" alt="头像" class="avatar">
      <div class="user-info">
        <h3>{{ userInfo.name }}</h3>
        <p>{{ userInfo.email }}</p>
      </div>
    </div>
    
    <!-- 🎯 功能导航标签 -->
    <nav class="user-tabs">
      <router-link to="/user/profile" class="tab">
        <Icon name="user" />
        个人资料
      </router-link>
      <router-link to="/user/orders" class="tab">
        <Icon name="shopping-bag" />
        我的订单
      </router-link>
      <router-link to="/user/favorites" class="tab">
        <Icon name="heart" />
        我的收藏
      </router-link>
      <router-link to="/user/addresses" class="tab">
        <Icon name="map-pin" />
        收货地址
      </router-link>
      <router-link to="/user/security" class="tab">
        <Icon name="shield" />
        安全设置
      </router-link>
    </nav>
    
    <!-- 🎯 内容区域 -->
    <div class="user-content">
      <router-view />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const userInfo = ref({
  name: '张三',
  email: 'zhangsan@example.com',
  avatar: '/avatar.jpg'
})
</script>
```
```js
const routes = [
  {
    path: '/admin',
    component: AdminLayout,
    meta: { 
      requiresAuth: true,
      title: '管理后台'
    },
    children: [
      {
        path: 'dashboard',
        name: 'Dashboard',
        component: Dashboard,
        meta: { 
          title: '仪表盘',
          icon: 'dashboard',
          breadcrumb: ['管理后台', '仪表盘']
        }
      },
      {
        path: 'users',
        name: 'UserManagement',
        component: UserList,
        meta: { 
          title: '用户管理',
          icon: 'users',
          permissions: ['user:read'],
          breadcrumb: ['管理后台', '用户管理']
        }
      }
    ]
  }
]
```
常见问题解决 🔧
默认子路由配置 ⚡
```js
// ❌ 错误配置
{
  path: '/admin',
  component: AdminLayout,
  children: [
    { path: '/', component: Dashboard }  // 错误：不要在子路由使用绝对路径
  ]
}

// ✅ 正确配置
{
  path: '/admin',
  component: AdminLayout,
  children: [
    { path: '', component: Dashboard }   // 空字符串表示默认子路由
  ]
}

// ✅ 或者使用重定向
{
  path: '/admin',
  component: AdminLayout,
  redirect: '/admin/dashboard',
  children: [
    { path: 'dashboard', component: Dashboard }
  ]
}
```
动态面包屑生成 🍞
``` vue
<script setup>
import { computed } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()

// 🎯 根据路由元信息生成面包屑
const breadcrumbs = computed(() => {
  const matched = route.matched.filter(item => item.meta?.title)
  return matched.map(item => ({
    title: item.meta.title,
    path: item.path,
    name: item.name
  }))
})
</script>

<template>
  <nav class="breadcrumb">
    <router-link 
      v-for="(crumb, index) in breadcrumbs"
      :key="crumb.name"
      :to="crumb.path"
      :class="{ 'is-active': index === breadcrumbs.length - 1 }">
      {{ crumb.title }}
      <span v-if="index < breadcrumbs.length - 1" class="separator">></span>
    </router-link>
  </nav>
</template>
```
性能优化建议 🚀
``` js
// 🎯 路由懒加载配置
const routes = [
  {
    path: '/admin',
    component: () => import('@/layouts/AdminLayout.vue'),
    children: [
      {
        path: 'dashboard',
        component: () => import(
          /* webpackChunkName: "admin-dashboard" */
          '@/views/admin/Dashboard.vue'
        )
      },
      {
        path: 'users',
        component: () => import(
          /* webpackChunkName: "admin-users" */
          '@/views/admin/UserManagement.vue'
        )
      }
    ]
  }
]
```
嵌套路由是构建复杂应用布局的强大工具，通过合理的路由层级设计，可以创建出结构清晰、用户体验优秀的应用！掌握嵌套路由，就掌握了现代Web应用架构设计的核心技能。

:::
## 如何实现路由懒加载？有什么好处？
::: details

路由懒加载是通过动态import()实现按需加载路由组件的技术，将大型应用拆分成多个代码块。

实现方式 🎯
```js
// 懒加载写法
const Home = () => import('@/views/Home.vue')

// 路由配置
{
  path: '/home',
  component: () => import('@/views/Home.vue')
}
```
核心好处 ⚡
减少首屏加载时间：只加载当前需要的代码
按需加载：用户访问时才下载对应组件
代码分割：Webpack自动生成独立的chunk文件
用户体验提升：应用启动更快，响应更及时
关键原理 📋
利用ES2020的动态import()和Webpack的代码分割功能，将路由组件打包成独立文件，实现运行时按需加载。


实现方式对比 📊
传统同步加载 ❌
```js
// 传统方式 - 同步加载
import Home from '@/views/Home.vue'
import About from '@/views/About.vue'
import User from '@/views/User.vue'
import Product from '@/views/Product.vue'

const routes = [
  { path: '/', component: Home },
  { path: '/about', component: About },
  { path: '/user', component: User },
  { path: '/product', component: Product }
]

// 问题：所有组件都会打包到main.js中
// 结果：首屏加载包含所有页面代码，体积巨大
```
路由懒加载实现 ✅
```js
// 🎯 方式1：函数式动态import
const routes = [
  {
    path: '/',
    name: 'Home',
    component: () => import('@/views/Home.vue')
  },
  {
    path: '/about',
    name: 'About',
    component: () => import('@/views/About.vue')
  },
  {
    path: '/user/:id',
    name: 'User',
    component: () => import('@/views/User.vue')
  }
]

// 🎯 方式2：赋值给变量
const Home = () => import('@/views/Home.vue')
const About = () => import('@/views/About.vue')

const routes = [
  { path: '/', component: Home },
  { path: '/about', component: About }
]
```
Webpack代码分割配置 🔧
自定义chunk名称 📦
```js
const routes = [
  {
    path: '/admin',
    component: () => import(
      /* webpackChunkName: "admin" */
      '@/views/admin/AdminPanel.vue'
    )
  },
  {
    path: '/user',
    component: () => import(
      /* webpackChunkName: "user" */
      '@/views/user/UserProfile.vue'
    )
  },
  {
    path: '/product',
    component: () => import(
      /* webpackChunkName: "product" */
      '@/views/product/ProductDetail.vue'
    )
  }
]

// 打包结果：
// admin.chunk.js    - 管理员相关页面
// user.chunk.js     - 用户相关页面  
// product.chunk.js  - 商品相关页面
```
分组打包策略 🎪
```js
// 🎯 按功能模块分组
const routes = [
  // 管理员模块 - 打包到admin组
  {
    path: '/admin/dashboard',
    component: () => import(
      /* webpackChunkName: "admin" */
      '@/views/admin/Dashboard.vue'
    )
  },
  {
    path: '/admin/users',
    component: () => import(
      /* webpackChunkName: "admin" */
      '@/views/admin/UserManagement.vue'
    )
  },
  
  // 用户模块 - 打包到user组
  {
    path: '/profile',
    component: () => import(
      /* webpackChunkName: "user" */
      '@/views/UserProfile.vue'
    )
  },
  {
    path: '/settings',
    component: () => import(
      /* webpackChunkName: "user" */
      '@/views/UserSettings.vue'
    )
  }
]
```

```js
// 🎯 电商网站的路由懒加载配置
const routes = [
  // 首页 - 立即加载（用户首先访问）
  {
    path: '/',
    name: 'Home',
    component: () => import('@/views/Home.vue')
  },
  
  // 商品相关 - 按需加载
  {
    path: '/products',
    component: () => import(
      /* webpackChunkName: "product" */
      '@/views/ProductList.vue'
    )
  },
  {
    path: '/product/:id',
    component: () => import(
      /* webpackChunkName: "product" */
      '@/views/ProductDetail.vue'
    )
  },
  
  // 用户中心 - 登录后才需要
  {
    path: '/profile',
    component: () => import(
      /* webpackChunkName: "user" */
      '@/views/UserProfile.vue'
    )
  },
  {
    path: '/orders',
    component: () => import(
      /* webpackChunkName: "user" */
      '@/views/OrderHistory.vue'
    )
  },
  
  // 购物车和结算 - 高频但非首屏
  {
    path: '/cart',
    component: () => import(
      /* webpackChunkName: "cart" */
      '@/views/ShoppingCart.vue'
    )
  },
  {
    path: '/checkout',
    component: () => import(
      /* webpackChunkName: "cart" */
      '@/views/Checkout.vue'
    )
  },
  
  // 管理后台 - 权限限制，独立打包
  {
    path: '/admin',
    component: () => import(
      /* webpackChunkName: "admin" */
      '@/views/admin/AdminLayout.vue'
    ),
    children: [
      {
        path: 'dashboard',
        component: () => import(
          /* webpackChunkName: "admin" */
          '@/views/admin/Dashboard.vue'
        )
      }
    ]
  }
]
```
大型企业应用策略 🏢
```js
// 🎯 大型企业应用的模块化懒加载
const routes = [
  // 核心功能 - 预加载
  {
    path: '/dashboard',
    component: () => import(
      /* webpackChunkName: "core" */
      /* webpackPreload: true */
      '@/views/Dashboard.vue'
    )
  },
  
  // 人力资源模块
  {
    path: '/hr',
    component: () => import(
      /* webpackChunkName: "hr-module" */
      '@/modules/hr/HRLayout.vue'
    ),
    children: [
      {
        path: 'employees',
        component: () => import(
          /* webpackChunkName: "hr-module" */
          '@/modules/hr/EmployeeManagement.vue'
        )
      },
      {
        path: 'attendance',
        component: () => import(
          /* webpackChunkName: "hr-module" */
          '@/modules/hr/AttendanceSystem.vue'
        )
      }
    ]
  },
  
  // 财务模块
  {
    path: '/finance',
    component: () => import(
      /* webpackChunkName: "finance-module" */
      '@/modules/finance/FinanceLayout.vue'
    ),
    children: [
      {
        path: 'reports',
        component: () => import(
          /* webpackChunkName: "finance-module" */
          '@/modules/finance/FinancialReports.vue'
        )
      }
    ]
  }
]
```
高级优化技巧 💡
预加载和预获取 🎯
```js
// 🎯 预加载 - 立即下载但不执行
{
  path: '/important',
  component: () => import(
    /* webpackPreload: true */
    '@/views/ImportantPage.vue'
  )
}

// 🎯 预获取 - 空闲时间下载
{
  path: '/optional',
  component: () => import(
    /* webpackPrefetch: true */
    '@/views/OptionalPage.vue'
  )
}
```
条件懒加载 🔀
```js
// 🎯 根据用户权限决定是否懒加载
const createUserRoutes = (userRole) => {
  const routes = [
    {
      path: '/profile',
      component: () => import('@/views/UserProfile.vue')
    }
  ]
  
  // 只有管理员才需要加载管理模块
  if (userRole === 'admin') {
    routes.push({
      path: '/admin',
      component: () => import(
        /* webpackChunkName: "admin" */
        '@/views/AdminPanel.vue'
      )
    })
  }
  
  return routes
}
```
错误处理和重试机制 ⚠️
```js
// 🎯 懒加载错误处理
const lazyLoad = (componentPath) => {
  return () => 
    import(componentPath)
      .catch(() => {
        // 加载失败时的降级处理
        console.error(`Failed to load component: ${componentPath}`)
        return import('@/views/ErrorPage.vue')
      })
}

const routes = [
  {
    path: '/user',
    component: lazyLoad('@/views/UserProfile.vue')
  }
]
```
监控和分析 📊
- Webpack Bundle Analyzer 🔍
```bash
# 安装分析工具
npm install --save-dev webpack-bundle-analyzer

# 分析打包结果
npm run build --report
```
加载性能监控 📈
```js
// 🎯 监控懒加载性能
const trackRouteLoad = (routeName) => {
  const startTime = performance.now()
  
  return () => 
    import(`@/views/${routeName}.vue`)
      .then(component => {
        const loadTime = performance.now() - startTime
        console.log(`Route ${routeName} loaded in ${loadTime}ms`)
        
        // 发送性能数据到监控系统
        analytics.track('route_load_time', {
          route: routeName,
          loadTime: loadTime
        })
        
        return component
      })
}
```
最佳实践总结 🎪
懒加载策略选择 📋
```js
// 🎯 根据页面重要性分级加载
const routeConfig = {
  // 🔴 关键页面 - 预加载
  critical: [
    { path: '/', preload: true },
    { path: '/login', preload: true }
  ],
  
  // 🟡 重要页面 - 懒加载但分组
  important: [
    { path: '/dashboard', chunk: 'core' },
    { path: '/profile', chunk: 'user' }
  ],
  
  // 🟢 普通页面 - 独立懒加载
  normal: [
    { path: '/settings', chunk: 'settings' },
    { path: '/help', chunk: 'help' }
  ],
  
  // ⚪ 低频页面 - 按需加载
  rare: [
    { path: '/admin', chunk: 'admin' },
    { path: '/reports', chunk: 'reports' }
  ]
}
```
性能优化检查清单 ✅
- ✅ 首屏路由使用预加载或同步加载
- ✅ 按功能模块分组打包相关页面
- ✅ 低频页面独立打包避免影响常用功能
- ✅ 重要页面使用prefetch预获取
- ✅ 配置合理的缓存策略
- ✅ 监控加载性能及时优化
路由懒加载是现代前端应用的标配优化技术，合理的懒加载策略可以显著提升应用的首屏性能和用户体验！掌握这项技术，你就能构建出快速响应的大型应用。

:::
## Vue Router的导航守卫有哪些？分别什么时候执行？
::: details

Vue Router导航守卫分为三大类型，按特定顺序在路由跳转过程中执行。

三大类型 🎯
 全局守卫：应用于所有路由的守卫 
- beforeEach：全局前置守卫
- beforeResolve：全局解析守卫
- afterEach：全局后置钩子 

 路由独享守卫：单个路由配置的守卫 

- beforeEnter：进入路由前执行 

组件内守卫：组件内部定义的守卫 
- beforeRouteEnter：进入组件前
- beforeRouteUpdate：路由参数变化时
- beforeRouteLeave：离开组件前 

执行顺序 ⚡ 

 离开组件 → 全局beforeEach → 路由beforeEnter → 进入组件beforeRouteEnter → 全局beforeResolve → 确认导航 → 全局afterEach

详细解析📚 

导航守卫执行流程 🔄 

全局守卫详解 🌍 

beforeEach - 全局前置守卫 🚪 
```js
// 🎯 最常用的导航守卫，用于权限验证
router.beforeEach((to, from, next) => {
  console.log('全局前置守卫执行')
  
  // 检查是否需要登录
  if (to.meta.requiresAuth && !isLoggedIn()) {
    next('/login')  // 重定向到登录页
  } else {
    next()  // 继续导航
  }
})

// 🎯 实际项目中的权限控制
router.beforeEach(async (to, from, next) => {
  // 显示loading
  showLoading()
  
  const token = localStorage.getItem('token')
  const publicPages = ['/login', '/register', '/home']
  
  // 公开页面直接放行
  if (publicPages.includes(to.path)) {
    next()
    return
  }
  
  // 需要权限的页面
  if (!token) {
    next('/login')
    return
  }
  
  try {
    // 验证token有效性
    const userInfo = await validateToken(token)
    
    // 检查页面权限
    if (hasPermission(to.meta.permissions, userInfo.permissions)) {
      next()
    } else {
      next('/unauthorized')
    }
  } catch (error) {
    // token无效，清除并跳转登录
    localStorage.removeItem('token')
    next('/login')
  }
})
```

beforeResolve - 全局解析守卫 🔍
```js
// 🎯 在导航确认前，所有组件内守卫和异步路由组件解析后调用
router.beforeResolve((to, from, next) => {
  console.log('全局解析守卫执行')
  
  // 可以在这里处理一些需要等待所有守卫完成的逻辑
  // 比如数据预取、页面访问统计等
  
  // 记录页面访问
  analytics.track('page_view', {
    page: to.path,
    title: to.meta.title
  })
  
  next()
})
```
afterEach - 全局后置钩子 🏁
```js
// 🎯 导航确认后调用，不能改变导航
router.afterEach((to, from) => {
  console.log('全局后置钩子执行')
  
  // 隐藏loading
  hideLoading()
  
  // 设置页面标题
  document.title = to.meta.title || 'Default Title'
  
  // 页面统计
  if (typeof gtag !== 'undefined') {
    gtag('config', 'GA_MEASUREMENT_ID', {
      page_path: to.path
    })
  }
  
  // 重置滚动位置
  window.scrollTo(0, 0)
})
```
路由独享守卫 🎯
```js
// 🎯 在路由配置中直接定义
const routes = [
  {
    path: '/admin',
    component: AdminPanel,
    beforeEnter: (to, from, next) => {
      console.log('路由独享守卫执行')
      
      // 检查管理员权限
      if (hasAdminRole()) {
        next()
      } else {
        next('/unauthorized')
      }
    }
  },
  {
    path: '/vip',
    component: VipArea,
    beforeEnter: async (to, from, next) => {
      // 异步权限检查
      try {
        const userLevel = await getUserLevel()
        if (userLevel >= 5) {
          next()
        } else {
          next('/upgrade')
        }
      } catch (error) {
        next('/error')
      }
    }
  }
]
```
组件内守卫 🏠 

beforeRouteEnter - 进入组件前 🚪
```vue
<script>
export default {
  // 🎯 进入组件前调用，此时组件实例还未创建
  beforeRouteEnter(to, from, next) {
    console.log('组件内守卫：beforeRouteEnter')
    
    // 不能访问this，因为组件实例还未创建
    // console.log(this) // undefined
    
    // 数据预取
    fetchUserData(to.params.id).then(userData => {
      next(vm => {
        // 通过next的回调访问组件实例
        vm.userData = userData
        vm.loading = false
      })
    }).catch(() => {
      next('/error')
    })
  }
}
</script>
```
beforeRouteUpdate - 路由参数变化 🔄
```vue
<script>
export default {
  // 🎯 当前路由改变，但组件被复用时调用
  beforeRouteUpdate(to, from, next) {
    console.log('组件内守卫：beforeRouteUpdate')
    
    // 用户从 /user/1 跳转到 /user/2 时触发
    if (to.params.id !== from.params.id) {
      this.loading = true
      this.loadUserData(to.params.id)
        .then(() => {
          this.loading = false
          next()
        })
        .catch(() => {
          next('/error')
        })
    } else {
      next()
    }
  }
}
</script>
```
beforeRouteLeave - 离开组件前 🚶
```vue
<script>
export default {
  data() {
    return {
      hasUnsavedChanges: false,
      formData: {}
    }
  },
  
  // 🎯 离开当前组件前调用
  beforeRouteLeave(to, from, next) {
    console.log('组件内守卫：beforeRouteLeave')
    
    // 检查是否有未保存的更改
    if (this.hasUnsavedChanges) {
      const answer = confirm('您有未保存的更改，确定要离开吗？')
      if (answer) {
        next()
      } else {
        next(false)  // 取消导航
      }
    } else {
      // 清理定时器、事件监听器等
      this.cleanup()
      next()
    }
  },
  
  methods: {
    cleanup() {
      // 清理资源
      if (this.timer) {
        clearInterval(this.timer)
      }
      // 移除事件监听
      window.removeEventListener('beforeunload', this.handleBeforeUnload)
    }
  }
}
</script>
```
完整执行顺序示例 📋
```js
// 🎯 完整的导航守卫执行示例
// 假设从 /home 跳转到 /user/123

// 1. 离开/home组件
// Home组件的beforeRouteLeave

// 2. 全局前置守卫
router.beforeEach((to, from, next) => {
  console.log('1. 全局前置守卫 beforeEach')
  next()
})

// 3. 路由独享守卫
const routes = [
  {
    path: '/user/:id',
    component: UserProfile,
    beforeEnter: (to, from, next) => {
      console.log('2. 路由独享守卫 beforeEnter')
      next()
    }
  }
]

// 4. 组件内守卫 - 进入
// UserProfile组件的beforeRouteEnter

// 5. 全局解析守卫
router.beforeResolve((to, from, next) => {
  console.log('3. 全局解析守卫 beforeResolve')
  next()
})

// 6. 导航确认，开始解析异步组件

// 7. 全局后置钩子
router.afterEach((to, from) => {
  console.log('4. 全局后置钩子 afterEach')
})

// 8. DOM更新

// 9. beforeRouteEnter的next回调执行
```
实际应用场景 🚀
- 完整的权限管理系统 🔐
```js
// 🎯 多层权限验证
router.beforeEach(async (to, from, next) => {
  const token = store.getters.token
  const userInfo = store.getters.userInfo
  
  // 白名单页面
  const whiteList = ['/login', '/register', '/404', '/500']
  if (whiteList.includes(to.path)) {
    next()
    return
  }
  
  // 检查登录状态
  if (!token) {
    next(`/login?redirect=${to.path}`)
    return
  }
  
  // 获取用户信息
  if (!userInfo.id) {
    try {
      await store.dispatch('user/getInfo')
    } catch (error) {
      await store.dispatch('user/logout')
      next('/login')
      return
    }
  }
  
  // 检查路由权限
  if (to.meta.roles) {
    if (hasPermission(to.meta.roles, userInfo.roles)) {
      next()
    } else {
      next('/401')
    }
  } else {
    next()
  }
})
```
表单保护和数据预取 📝
```vue
<template>
  <div class="edit-form">
    <form @submit="handleSubmit">
      <input v-model="formData.name" @input="markAsChanged">
      <button type="submit">保存</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {},
      originalData: {},
      hasChanges: false,
      loading: true
    }
  },
  
  beforeRouteEnter(to, from, next) {
    // 🎯 数据预取
    Promise.all([
      fetchUserData(to.params.id),
      fetchUserPermissions(to.params.id)
    ]).then(([userData, permissions]) => {
      next(vm => {
        vm.formData = { ...userData }
        vm.originalData = { ...userData }
        vm.permissions = permissions
        vm.loading = false
      })
    }).catch(() => {
      next('/error')
    })
  },
  
  beforeRouteUpdate(to, from, next) {
    // 🎯 切换用户时重新加载数据
    if (to.params.id !== from.params.id) {
      this.loadUserData(to.params.id).then(() => next())
    } else {
      next()
    }
  },
  
  beforeRouteLeave(to, from, next) {
    // 🎯 表单保护
    if (this.hasChanges) {
      this.$confirm('您有未保存的更改，确定要离开吗？')
        .then(() => next())
        .catch(() => next(false))
    } else {
      next()
    }
  },
  
  methods: {
    markAsChanged() {
      this.hasChanges = JSON.stringify(this.formData) !== JSON.stringify(this.originalData)
    }
  }
}
</script>
```
Vue 3 Composition API用法 💫
```vue
<script setup>
import { ref, onMounted } from 'vue'
import { onBeforeRouteLeave, onBeforeRouteUpdate } from 'vue-router'

const hasUnsavedChanges = ref(false)
const userData = ref({})

// 🎯 组合式API中的路由守卫
onBeforeRouteUpdate(async (to, from) => {
  if (to.params.id !== from.params.id) {
    const newUserData = await fetchUserData(to.params.id)
    userData.value = newUserData
  }
})

onBeforeRouteLeave((to, from) => {
  if (hasUnsavedChanges.value) {
    const answer = window.confirm('确定要离开吗？您有未保存的更改。')
    if (!answer) return false
  }
})
</script>
```
常见问题和解决方案 🔧 

next()函数的正确使用 ✅ 
```js
// ✅ 正确用法
router.beforeEach((to, from, next) => {
  if (condition) {
    next()  // 继续导航
  } else {
    next('/login')  // 重定向
  }
})

// ❌ 错误用法 - 没有调用next()
router.beforeEach((to, from, next) => {
  if (condition) {
    // 忘记调用next()，导航会卡住
  }
})

// ❌ 错误用法 - 多次调用next()
router.beforeEach((to, from, next) => {
  next()
  next('/home')  // 错误：不能多次调用
})
```
掌握Vue Router导航守卫的执行顺序和使用场景，是构建安全、用户友好的Vue应用的关键技能！合理运用这些守卫，能让你的应用在用户体验和安全性之间找到完美平衡。

:::

## 全局守卫、路由独享守卫、组件内守卫的使用场景？
:::details 
三种守卫各有明确的使用场景，按作用范围和职责分工来选择。

核心使用场景 🎯
全局守卫：应用级通用逻辑 

用户登录验证、权限检查
页面访问统计、埋点上报
Loading状态管理、页面标题设置 

路由独享守卫：特定路由的专属逻辑
特殊权限验证（如VIP页面、管理员后台）
特定路由的参数校验
单个页面的访问限制 

组件内守卫：组件级的业务逻辑
数据预取和初始化
表单未保存提醒
组件资源清理 

选择原则 📋 

全局性需求用全局守卫，路由特定需求用路由守卫，组件相关需求用组件守卫。 


详细解析📚 

全局守卫使用场景 🌍 

用户认证和权限管理 🔐
```js
// 🎯 全局前置守卫 - 最常用场景
router.beforeEach(async (to, from, next) => {
  // 场景1: 用户登录状态检查
  const token = localStorage.getItem('token')
  const publicPages = ['/login', '/register', '/home', '/about']
  
  if (!publicPages.includes(to.path) && !token) {
    // 未登录用户访问受保护页面
    next(`/login?redirect=${to.path}`)
    return
  }
  
  // 场景2: 用户权限验证
  if (token && to.meta.requiresAuth) {
    try {
      const userInfo = await store.dispatch('user/getUserInfo')
      
      // 检查页面权限
      if (to.meta.roles && !hasRole(userInfo.roles, to.meta.roles)) {
        next('/unauthorized')
        return
      }
      
      next()
    } catch (error) {
      // token失效，清除并重新登录
      localStorage.removeItem('token')
      next('/login')
    }
  } else {
    next()
  }
})

// 🎯 全局后置钩子 - 通用处理
router.afterEach((to, from) => {
  // 场景3: 页面标题管理
  document.title = to.meta.title ? `${to.meta.title} - 我的应用` : '我的应用'
  
  // 场景4: 页面访问统计
  analytics.track('page_view', {
    page_title: to.meta.title,
    page_path: to.path,
    referrer: from.path
  })
  
  // 场景5: 隐藏全局Loading
  hideGlobalLoading()
})
```
多语言和主题管理 🌐
```js
// 🎯 全局守卫处理应用级配置
router.beforeEach((to, from, next) => {
  // 场景6: 多语言处理
  const locale = to.params.locale || getDefaultLocale()
  if (locale !== getCurrentLocale()) {
    setLocale(locale)
  }
  
  // 场景7: 主题切换
  if (to.meta.theme) {
    document.body.className = `theme-${to.meta.theme}`
  }
  
  // 场景8: 页面Meta信息
  updateMetaTags(to.meta)
  
  next()
})
```
路由独享守卫使用场景 🎯 

特殊权限和业务限制 👑
```js
const routes = [
  {
    path: '/admin',
    component: AdminPanel,
    // 🎯 场景1: 管理员专属验证
    beforeEnter: async (to, from, next) => {
      const userInfo = store.getters.userInfo
      
      if (!userInfo.isAdmin) {
        ElMessage.error('需要管理员权限')
        next('/home')
        return
      }
      
      // 检查管理员级别
      if (to.path.includes('/admin/system') && userInfo.adminLevel < 3) {
        next('/admin/dashboard')
        return
      }
      
      next()
    }
  },
  
  {
    path: '/vip',
    component: VipArea,
    // 🎯 场景2: VIP会员验证
    beforeEnter: async (to, from, next) => {
      try {
        const memberInfo = await api.getMemberInfo()
        
        if (!memberInfo.isVip) {
          // 非VIP用户，展示升级提示
          showUpgradeDialog()
          next('/membership')
          return
        }
        
        if (memberInfo.expireDate < new Date()) {
          ElMessage.warning('VIP已过期，请续费')
          next('/renew')
          return
        }
        
        next()
      } catch (error) {
        next('/error')
      }
    }
  },
  
  {
    path: '/beta/:feature',
    component: BetaFeature,
    // 🎯 场景3: 测试功能访问控制
    beforeEnter: (to, from, next) => {
      const userInfo = store.getters.userInfo
      const feature = to.params.feature
      
      // 检查用户是否在beta测试名单中
      if (!userInfo.betaFeatures.includes(feature)) {
        ElMessage.info('该功能正在内测中')
        next('/home')
        return
      }
      
      // 记录beta功能访问
      analytics.track('beta_feature_access', {
        feature: feature,
        userId: userInfo.id
      })
      
      next()
    }
  }
]
```
特定业务规则验证 📋 

```js
const routes = [
  {
    path: '/exam/:id',
    component: ExamPage,
    // 🎯 场景4: 考试规则验证
    beforeEnter: async (to, from, next) => {
      const examId = to.params.id
      
      try {
        const exam = await api.getExamInfo(examId)
        const userStatus = await api.getUserExamStatus(examId)
        
        // 检查考试是否开放
        if (exam.status !== 'active') {
          ElMessage.error('考试尚未开始或已结束')
          next('/exams')
          return
        }
        
        // 检查用户是否已完成
        if (userStatus.completed) {
          ElMessage.info('您已完成此考试')
          next(`/exam/${examId}/result`)
          return
        }
        
        // 检查剩余次数
        if (userStatus.attempts >= exam.maxAttempts) {
          ElMessage.error('考试次数已用完')
          next('/exams')
          return
        }
        
        next()
      } catch (error) {
        next('/error')
      }
    }
  }
]
```
组件内守卫使用场景 🏠 

数据预取和组件初始化 📡
``` vue
<script>
export default {
  name: 'UserProfile',
  
  // 🎯 场景1: 数据预取
  beforeRouteEnter(to, from, next) {
    const userId = to.params.id
    
    // 并行获取用户数据
    Promise.all([
      api.getUserInfo(userId),
      api.getUserPosts(userId),
      api.getUserFollowers(userId)
    ]).then(([userInfo, posts, followers]) => {
      next(vm => {
        // 组件实例创建后设置数据
        vm.userInfo = userInfo
        vm.posts = posts
        vm.followers = followers
        vm.loading = false
      })
    }).catch(error => {
      if (error.status === 404) {
        next('/user-not-found')
      } else {
        next('/error')
      }
    })
  },
  
  // 🎯 场景2: 路由参数变化处理
  beforeRouteUpdate(to, from, next) {
    const newUserId = to.params.id
    const oldUserId = from.params.id
    
    if (newUserId !== oldUserId) {
      // 用户ID变化，重新加载数据
      this.loading = true
      this.loadUserData(newUserId)
        .then(() => {
          this.loading = false
          next()
        })
        .catch(() => {
          next('/error')
        })
    } else {
      // 只是查询参数变化，直接继续
      next()
    }
  },
  
  // 🎯 场景3: 组件清理和保护
  beforeRouteLeave(to, from, next) {
    // 清理定时器
    if (this.refreshTimer) {
      clearInterval(this.refreshTimer)
    }
    
    // 取消未完成的请求
    if (this.cancelTokenSource) {
      this.cancelTokenSource.cancel('Route changed')
    }
    
    next()
  }
}
</script>
```
表单保护和状态管理 📝 

```vue
<script>
export default {
  name: 'ArticleEditor',
  
  data() {
    return {
      article: {
        title: '',
        content: '',
        tags: []
      },
      originalArticle: {},
      hasUnsavedChanges: false,
      autoSaveTimer: null
    }
  },
  
  // 🎯 场景4: 编辑器数据初始化
  beforeRouteEnter(to, from, next) {
    if (to.params.id === 'new') {
      // 新建文章
      next(vm => {
        vm.initNewArticle()
      })
    } else {
      // 编辑已有文章
      api.getArticle(to.params.id)
        .then(article => {
          next(vm => {
            vm.article = { ...article }
            vm.originalArticle = { ...article }
            vm.startAutoSave()
          })
        })
        .catch(() => {
          next('/articles')
        })
    }
  },
  
  // 🎯 场景5: 表单保护
  beforeRouteLeave(to, from, next) {
    // 停止自动保存
    if (this.autoSaveTimer) {
      clearInterval(this.autoSaveTimer)
    }
    
    // 检查未保存的更改
    if (this.hasUnsavedChanges) {
      this.$confirm(
        '您有未保存的更改，确定要离开吗？',
        '提示',
        {
          confirmButtonText: '保存并离开',
          cancelButtonText: '直接离开',
          distinguishCancelAndClose: true,
          type: 'warning'
        }
      ).then(() => {
        // 保存并离开
        this.saveArticle().then(() => next())
      }).catch(action => {
        if (action === 'cancel') {
          // 直接离开
          next()
        } else {
          // 取消离开
          next(false)
        }
      })
    } else {
      next()
    }
  }
}
</script>
```
实际项目应用案例 🚀 

电商网站的完整守卫策略 🛒 

```js
// 🎯 全局守卫 - 处理通用逻辑
router.beforeEach(async (to, from, next) => {
  // 显示页面加载状态
  showPageLoading()
  
  // 用户认证
  const token = getToken()
  const needsAuth = to.matched.some(record => record.meta.requiresAuth)
  
  if (needsAuth && !token) {
    next('/login')
    return
  }
  
  // 购物车数据同步
  if (token && !store.getters.cartLoaded) {
    await store.dispatch('cart/loadCart')
  }
  
  next()
})

// 🎯 路由独享守卫 - 特定页面逻辑
const routes = [
  {
    path: '/checkout',
    component: Checkout,
    beforeEnter: (to, from, next) => {
      // 结算页面需要购物车有商品
      const cartItems = store.getters.cartItems
      if (cartItems.length === 0) {
        ElMessage.warning('购物车为空')
        next('/cart')
        return
      }
      
      // 检查商品库存
      const hasOutOfStock = cartItems.some(item => item.stock <= 0)
      if (hasOutOfStock) {
        ElMessage.error('购物车中有商品缺货')
        next('/cart')
        return
      }
      
      next()
    }
  },
  
  {
    path: '/vip-sale',
    component: VipSale,
    beforeEnter: async (to, from, next) => {
      // VIP专享活动
      const userLevel = await getUserLevel()
      if (userLevel < 3) {
        next('/vip-upgrade')
        return
      }
      next()
    }
  }
]

// 🎯 组件内守卫 - 组件特定逻辑
// 商品详情页
export default {
  beforeRouteEnter(to, from, next) {
    // 预取商品数据
    Promise.all([
      api.getProduct(to.params.id),
      api.getProductReviews(to.params.id),
      api.getRelatedProducts(to.params.id)
    ]).then(([product, reviews, related]) => {
      next(vm => {
        vm.product = product
        vm.reviews = reviews
        vm.relatedProducts = related
      })
    })
  }
}
```

性能和维护建议 ⚡
```js
// 🎯 避免在守卫中执行耗时操作
router.beforeEach(async (to, from, next) => {
  // ❌ 避免每次都重新获取用户信息
  // const userInfo = await api.getUserInfo()
  
  // ✅ 使用缓存或状态管理
  let userInfo = store.getters.userInfo
  if (!userInfo.id) {
    userInfo = await store.dispatch('user/fetchUserInfo')
  }
  
  next()
})

// 🎯 合理使用守卫优先级
// 全局守卫处理通用逻辑，路由守卫处理特殊逻辑
// 避免在多个地方重复相同的逻辑
```
理解三种守卫的使用场景，是构建安全、高效的Vue应用的关键！选择合适的守卫类型，不仅能让代码更清晰，还能提升应用的性能和可维护性。