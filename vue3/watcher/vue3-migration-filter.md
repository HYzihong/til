<!--
 * @Author: hy
 * @Date: 2022-07-31 17:20:32
 * @LastEditors: hy
 * @Description: 
 * @LastEditTime: 2022-07-31 17:20:34
 * @FilePath: /til/vue3/watcher/migration-filter.md
 * Copyright 2022 hy, All Rights Reserved. 
 * 仅供学习使用~
-->

# migration-filter

### 组件内 filter

#### 2.x 语法([[vue2-filter]])

```vue
<template>
  <h1>Bank Account Balance</h1>
  <p>{{ accountBalance | currencyUSD }}</p>
</template>

<script>
  export default {
    props: {
      accountBalance: {
        type: Number,
        required: true
      }
    },
    filters: {
      currencyUSD(value) {
        return '$' + value
      }
    }
  }
</script>
```

#### 3.x 语法

```vue
<template>
  <h1>Bank Account Balance</h1>
  <p>{{ accountInUSD }}</p>
  or
  <p>{{ _accountInUSD(accountBalance) }}</p>
  
</template>

<script>
  export default {
    props: {
      accountBalance: {
        type: Number,
        required: true
      }
    },
    computed: {
      accountInUSD() {
        return '$' + this.accountBalance
      }
    }
    methods:{
	    _accountInUSD(value) {
		    return '$' + value
		}
	}
  }
</script>
```


### 全局 filter

#### 2.x 语法

#### 3.x 语法

使用全局属性进行替代

```js
// main.js
const app = createApp(App)

app.config.globalProperties.$filters = {
  currencyUSD(value) {
    return '$' + value
  }
}
```


```vue
<!-- component -->
<template>
  <h1>Bank Account Balance</h1>
  <p>{{ $filters.currencyUSD(accountBalance) }}</p>
</template>
```
---

参考：
1. https://v3.cn.vuejs.org/guide/migration/filters.html#_2-x-%E8%AF%AD%E6%B3%95