# javascript-set-forEach

> 文档：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set/forEach


set `forEach` 函数为集合对象中每个元素(即使是undefined)都执行一次回调；它不会返回任何值。

### 语法

```js

new Set(xxx).forEach(callback[, thisArg])

```


#### 参数

`callback`

为集合中每个元素执行的回调函数，该函数接收三个参数：

- **`currentValue`**  (元素的值) ，   **`currentKey可选`**   （元素的索引） ：   **currentValue** 是正在被操作的元素。并且由于集合没有索引，所以 **currentKey** 也表示这个正在被操作的元素。

- **`set可选`**   (正在遍历的集合对象)      调用当前 `forEach` 方法的集合对象

 `thisArg`**`可选`**     回调函数执行过程中的 `this` 值。

#### 返回值

`undefined`


#### 案例

```js

function logSetElements(value1, value2, set) {
    console.log("s[" + value1 + "] = " + value2);
}

new Set(["foo", "bar", undefined]).forEach(logSetElements);

// logs:
// "s[foo] = foo"
// "s[bar] = bar"
// "s[undefined] = undefined"

```