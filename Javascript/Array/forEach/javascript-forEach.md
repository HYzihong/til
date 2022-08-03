# forEach

> 半摘抄mdn，为了细粒度过一遍文档


### 语法

`arr.forEach(callback(currentValue [, index [, array]])[, thisArg])`

##### 参数

- `callback` 为数组中每个元素执行的函数，该函数接收一至三个参数：
	
	- `currentValue`数组中正在处理的当前元素。
	
	- `index` 可选 数组中正在处理的当前元素的索引。
	
	- `array` 可选 `forEach()` 方法正在操作的数组。

- `thisArg` 可选 可选参数。当执行回调函数 `callback` 时，用作 `this` 的值。

##### 返回值

- `undefined`

### 注意的点

- `forEach()` 方法按升序为数组中含有效值的每一项执行一次 `callback` 函数，那些`已删除`或者`未初始化`的项将被跳过（例如在稀疏数组上）。
- `forEach()` 遍历的范围在第一次调用 `callback` 前就会确定。调用 `forEach` 后添加到数组中的项不会被 `callback` 访问到。如果已经存在的值被改变，则传递给 `callback` 的值是 `forEach()` 遍历到他们那一刻的值。已删除的项不会被遍历到。如果已访问的元素在迭代时被删除了（例如使用 `shift()`），之后的元素将被跳过。
- `forEach()` 为每个数组元素执行一次 `callback` 函数；与 `map()` 或者 `reduce()` 不同的是，它总是返回 `undefined`值，并且不可链式调用。其典型用例是在一个调用链的最后执行副作用（side effects，函数式编程上，指函数进行 返回结果值 以外的操作）。
-  `forEach` 不会直接改变调用它的对象，但是那个对象可能会被 `callback` 函数改变。
-  除了抛出异常以外，没有办法中止或跳出 `forEach()` 循环。[[怎么样让forEach 支持跳出循环]]

总结就是：forEach 一调用就决定了遍历范围（范围只会变小不会变大），只遍历有效值（不遍历已删除和未初始化的），返回值只可能是`undefined`  ，不支持链式调用，只支持抛出异常的中止or跳出循环，不会直接改变调用它的对象，但是那个对象可能会被 `callback` 函数改变 。
 
### 优缺点

---

参考：

1. [MDN-forEach](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)