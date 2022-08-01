<!--
 * @Author: hy
 * @Date: 2022-07-31 17:13:41
 * @LastEditors: hy
 * @Description: 
 * @LastEditTime: 2022-07-31 17:14:15
 * @FilePath: /til/vue3/watcher/watch.md
 * Copyright 2022 hy, All Rights Reserved. 
 * 仅供学习使用~
-->


# watch 

>
>语法
>`watch( source , ( curVal , preVal )=>{ //... }, options )`
>
> `source` : 
> 	**监视复杂表达式的函数**  (等同于监听一个getter()函数)
> 	**监听 ref 定义的响应式数据**ref() 
> 	**监听 reactive 定义的响应式数据**reactive() 
> 	**监听多个响应式数据**[`...ref()` ,   ` ...reactive()`] 
> 	**监听响应式对象中某个属性的变化**()=>sxxx.xxx (`{ deep: true }`)
> 	
> `options` (tyep `WatchOption`)
> - immediate?: boolean // 默认：false
> - deep?: boolean 
> - 与watchEffect 共享的属性 （type `WatchEffectOptions`）
> 	- flush?: 'pre' | 'post' | 'sync' // 默认：'pre'
> 	- onTrack?: (event: DebuggerEvent) => void
> 	- onTrigger?: (event: DebuggerEvent) => void
> 	

注：
1. 当变更（不是替换）对象或数组并使用 deep 选项时，旧值将与新值相同，因为它们的引用指向同一个对象/数组。Vue 不会保留变更之前值的副本。


---

###  $watch

-   **参数：**
    -   `{string | Function} source`
    -   `{Function | Object} callback`
    -   `{Object} [options]`
        -   `{boolean} deep`
        -   `{boolean} immediate`
        -   `{string} flush`
-   **返回：**`{Function} unwatch`
-   **用法：**
	- 侦听组件实例上的响应式 property 或函数计算结果的变化。回调函数得到的参数为新值和旧值。我们只能将顶层的 `data`、`props` 或 `computed` property 名作为字符串传递。对于更复杂的表达式，用一个函数取代。


参考：
1. https://v3.cn.vuejs.org/api/instance-methods.html#watch

---


### Watch vs [[vue3-watchEffect#特点]]

watch拥有不同的：
    - 懒执行副作用(即回调仅在侦听源发生变化时被调用)；
    - 更具体地说明什么状态应该触发侦听器重新运行；(`immediate\deep`)  (不确定)
    - 可以访问侦听状态变化前后的值(`( curVal , preVal )`)
`watch` 与 `watchEffect` 相同的：
	- 副作用刷新时机(`flush`)
	- 调试方面（`onTrack\onTrigger`)
	- 清除副总用（`onInvalidate`)
	- 手动停止监听 （type `StopHandle`)


### example [->](https://v3.cn.vuejs.org/guide/reactivity-computed-watchers.html#watch)

```javascript

// 侦听一个 getter
const state = reactive({ count: 0 })
watch(
  () => state.count, //  接受一个getter函数
  (count, prevCount) => {
    /* ... */
  }
)

 // 用于监视复杂表达式的函数
    this.$watch(
      // 表达式 `this.a + this.b` 每次得出一个不同的结果时
      // 处理函数都会被调用。
      // 这就像监听一个未被定义的计算属性
      () => this.a + this.b,
      (newVal, oldVal) => {
        // 做点什么
      }
    )

// 直接侦听ref
const count = ref(0)
watch(count, (count, prevCount) => {
  /* ... */
})

//  侦听多个数据源
const firstName = ref('')
const lastName = ref('')

watch([firstName, lastName], (newValues, prevValues) => {
  console.log(newValues, prevValues)
})

firstName.value = 'John' // logs: ["John", ""] ["", ""]
lastName.value = 'Smith' // logs: ["John", "Smith"] ["John", ""]


// 同一个函数里同时改变这些被侦听的来源，侦听器仍只会执行一次
// ==>多个同步更改只会触发一次侦听器
 const changeValues = () => {
    firstName.value = 'John'
    lastName.value = 'Smith'
  }

 changeValues() // 打印 ["John", "Smith"] ["", ""]

注意多个同步更改只会触发一次侦听器。

通过更改设置 `flush: 'sync'`，我们可以为每个更改都强制触发侦听器，尽管这通常是不推荐的。或者，可以用 [nextTick](https://v3.cn.vuejs.org/api/global-api.html#nexttick) 等待侦听器在下一步改变之前运行。例如：

const changeValues = async () => {
  firstName.value = 'John' // 打印 ["John", ""] ["", ""]
  await nextTick()
  lastName.value = 'Smith' // 打印 ["John", "Smith"] ["John", ""]
}


// 侦听响应式对象
//使用侦听器来比较一个数组或对象的值，这些值是响应式的，要求它有一个由值构成的副本。

const numbers = reactive([1, 2, 3, 4])

watch(
  () => [...numbers],
  (numbers, prevNumbers) => {
    console.log(numbers, prevNumbers)
  }
)

numbers.push(5) // logs: [1,2,3,4,5] [1,2,3,4]


// 尝试检查深度嵌套对象或数组中的 property 变化时，仍然需要 `deep` 选项设置为 true。

const state = reactive({ 
  id: 1,
  attributes: { 
    name: '',
  }
})

watch(
  () => state,
  (state, prevState) => {
    console.log('not deep', state.attributes.name, prevState.attributes.name)
  }
)

watch(
  () => state,
  (state, prevState) => {
    console.log('deep', state.attributes.name, prevState.attributes.name)
  },
  { deep: true }
)

state.attributes.name = 'Alex' // 日志: "deep" "Alex" "Alex"


// 然而，侦听一个响应式对象或数组将始终返回该对象的当前值和上一个状态值的引用。为了完全侦听深度嵌套的对象和数组，可能需要对值进行深拷贝。这可以通过诸如 [lodash.cloneDeep](https://lodash.com/docs/4.17.15#cloneDeep) 这样的实用工具来实现。
import _ from 'lodash'

const state = reactive({
  id: 1,
  attributes: {
    name: '',
  }
})

watch(
  () => _.cloneDeep(state),
  (state, prevState) => {
    console.log(state.attributes.name, prevState.attributes.name)
  }
)

state.attributes.name = 'Alex' // 日志: "Alex" ""


```


----

参考：

1. [vue3 watch](https://v3.cn.vuejs.org/api/computed-watch-api.html#watch)
2.  [Vue3中 watch、watchEffect 详解](https://juejin.cn/post/7092412488725037087)