# javascript-map-forEach

`forEach` 方法会对 map 中每个真实存在的键执行一次给定的 `callback` 函数。它不会对被删除的和改变的键执行函数。然而，它会对每个值为 `undefined` 的键执行函数。

### 语法


```js

new Map(...).forEach(callback([value][,key][,map])[, thisArg])

```

#### 参数

`callback`

`myMap` 中每个元素所要执行的函数。它具有如下的参数

`value` 可选

每个迭代的值。(当前的 `value`)

`key` 可选

每个迭代的键。（当前的 `key`）

`map` 可选

被迭代的 map（上文语法框中的 `new Map(...)`）。

`thisArg` 可选

在 `callback` 执行中使用的 `this` 的值。

##### 返回值

`undefined


