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
### 特点

1.  `非惰性`：一旦运行就会立即执行；
2. `更加抽象`：使用时不需要具体指定监听的谁，回调函数内直接使用就可以；
3. `不可访问之前的值`：只能访问当前最新的值，访问不到修改之前的值；


### 监听停止

- 当 `watchEffect` 在组件的 setup() 函数或生命周期钩子被调用时，侦听器会被链接到该组件的生命周期，并在组件卸载时自动停止。
- 可以显式的调用 `watchEffect()` 的返回开实现停止监听。


### 清除副作用 `onInvalidate()`

- 有时副作用函数会执行一些异步的副作用，这些响应需要在其失效时清除。
- 侦听副作用传入的函数可以接收一个 onInvalidate 函数作入参，用来注册清理失效时的回调。
- 前提条件：
	- 1. 当前副作用一般是`可以被中断开的异步操作`（定时器、axios请求、Promise、async）
	- 2. 副作用即将重新执行时会执行 `onInvalidate()`
	- 3. 侦听器被停止 (如果在 setup() 或生命周期钩子函数中使用了 watchEffect，则在组件卸载时)执行 `onInvalidate()`

> 我们之所以是通过传入一个函数去注册失效回调，而不是从回调返回它，是因为返回值对于异步错误处理很重要。

example[link]()

```javascript

	watchEffect((onInvalidate) => {
      const CancelToken = axios.CancelToken;
      const source = CancelToken.source();
      onInvalidate(() => {
        source.cancel();
      });
      
      axios.get(url, {
        cancelToken: source.token,
      }).then((response) => {
        content.value = response.data.content;
      }).catch(function (err) {
        if (axios.isCancel(err)) {
          console.log('Request canceled', err.message);
        }
      });
    });

```

对于axios请求，最新的会覆盖前面的请求返回，响应快的请求会被最新的请求结果覆盖，响应慢的请求会被中断执行最新的请求


在执行数据请求时，副作用函数往往是一个异步函数：
```javascript

const data = ref(null)
watchEffect(async onInvalidate => {
  onInvalidate(() => {
    /* ... */
  }) // 我们在Promise解析之前注册清除函数
  data.value = await fetchData(props.id)
})

```
我们知道异步函数都会隐式地返回一个 Promise，但是清理函数必须要在 Promise 被 resolve 之前被注册。另外，Vue 依赖这个返回的 Promise 来自动处理 Promise 链上的潜在错误。



### 副作用刷新时机

#### 先执行监听器，然后更新DOM

> Vue 的响应性系统会缓存副作用函数，并异步地刷新它们，这样可以避免同一个“tick”中多个状态改变导致的不必要的重复调用。
> 
> 在核心的具体实现中，组件的 update 函数也是一个被侦听的副作用。当一个用户定义的副作用函数进入队列时，默认情况下，会在所有的组件update前执行。 (所谓组件的 update 函数是 Vue 内置的用来更新DOM的函数，它也是副作用）
> 
同一个“tick”的意思是，Vue的内部机制会以最科学的计算规则将视图刷新请求合并成一个一个的"tick"，每个“tick”刷新一次视图，如：a=1; b=2; 只会触发一次视图刷新。$nextTick的Tick就是指这个。





### 参数 `flush`

- `pre`  (default) 在组件更新后执行  (`watchEffect` + `{flush:pre}` ==> `watchEffect`)
- `post`在组件更新后执行 (这样你就可以访问更新的 DOM;这也将推迟副作用的初始运行，直到组件的首次渲染完成)(`watchEffect` + `{flush:post}` ==> `watchPostEffect`  Vue 3.2.0+)
- `sync`强制效果始终同步触发(与watch一样使其为每个更改都强制触发侦听器，然而，这是低效的，应该很少需要) (`watchEffect` + `{flush:sync}` ==> `watchSyncEffect` Vue 3.2.0+)



### 侦听器调试(开发模式下)

- 参数 `onTrack` 将在响应式 property 或 ref 作为依赖项被追踪时被调用
- 参数 `onTrigger`  将在依赖项变更导致副作用被触发时被调用


```javascript

	watchEffect(
	  () => {
	    /* ... */
	  },
	  {
	    onTrigger(e) {
	      debugger
	    }
	  }
	)

```
---

参考:
1. [聊一聊函数式编程中的副作用概念](https://juejin.cn/post/6908512860683370503)
2. [Vue3中 watch、watchEffect 详解](https://juejin.cn/post/7092412488725037087)




---

<!-- TODO vue2 watch debugger 是怎么使用的，是放在直接放在内部还是放在get set函数中的 -->
<!-- TODO vue3 watch watchEffect 和 computed 的对比 还有filter的迁移-->
<!-- TODO vue2 watch filter computed  的区别-->