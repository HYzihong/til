<!--
 * @Author: hy
 * @Date: 2022-07-31 17:13:02
 * @LastEditors: hy
 * @Description: 
 * @LastEditTime: 2022-07-31 17:13:02
 * @FilePath: /til/vue3/watcher/watchEffect.md
 * Copyright 2022 hy, All Rights Reserved. 
 * 仅供学习使用~
-->

# Vue3 watchEffect

> 立即执行传入的一个函数，同时响应式追踪其依赖，并在其依赖变更时重新运行该函数。[link](https://v3.cn.vuejs.org/api/computed-watch-api.html#watcheffect)
> 为了根据响应式状态自动应用和重新应用副作用，我们可以使用 watchEffect 函数。它立即执行传入的一个函数，同时响应式追踪其依赖，并在其依赖变更时重新运行该函数。[link](https://v3.cn.vuejs.org/guide/reactivity-computed-watchers.html#watcheffect)

---

> 前提提要：

副作用是什么？

副作用主是函数式编程中的概念
函数式编程中的隔离思想，它所想隔离的就是“副作用”
在程序中的副作用这个词存在的原因是为了引起人的注意，意思是在程序运行时会出现不可控的副作用（例如：在IO操作时，会在页面中显示IO操作的状态），所以程序执行时我们已经变得不可控了，后期测试时我们变的复杂了。
> PromiseA+规范的测试用例，官方提供了872种测试用例，Promise必须全部通过872种测试用例才符合官方规范

---

### 参数 `flush`

- `pre` default 在组件更新后执行  (`watchEffect` + `{flush:pre}` ==> `watchEffect`)
- `post`在组件更新后执行 (`watchEffect` + `{flush:post}` ==> `watchPostEffect`)
- `sync`强制效果始终同步触发 (`watchEffect` + `{flush:sync}` ==> `watchSyncEffect`)

### 侦听器调试

- 参数 `onTrack`
- 参数 `onTrigger` 

---

参考:
1. [聊一聊函数式编程中的副作用概念](https://juejin.cn/post/6908512860683370503)


---

<!-- TODO vue2 watch debugger 是怎么使用的，是放在直接放在内部还是放在get set函数中的 -->
<!-- TODO vue3 watch watchEffect 和 computed 的对比 还有filter的迁移-->
<!-- TODO vue2 watch filter computed  的区别-->