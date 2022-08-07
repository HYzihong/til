# Array.prototype.flat()


> https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat



按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组中的元素合并为一个新数组返回。

### 语法

```js

let newArray = arr.flat([depth])

```

`depth` 可选

指定要提取嵌套数组的结构深度，默认值为 1。

返回值

一个包含将数组与子数组中所有元素的新数组。


特点：

1. `flat()` 方法会移除数组中的空项：
2. 使用 Infinity，可展开任意深度的嵌套数组



---

替代方案：

> https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat#%E6%9B%BF%E4%BB%A3%E6%96%B9%E6%A1%88



### [使用 `reduce` 与 `concat`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat#%E4%BD%BF%E7%94%A8_reduce_%E4%B8%8E_concat "Permalink to 使用 reduce 与 concat")

```js
var arr = [1, 2, [3, 4]];

// 展开一层数组
// arr.flat();
// 等效于
arr.reduce((acc, val) => acc.concat(val), []);
// [1, 2, 3, 4]

// 使用扩展运算符 ...
const flattened = arr => [].concat(...arr);
```

### [reduce + concat + isArray + recursivity](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat#reduce_concat_isarray_recursivity "Permalink to reduce + concat + isArray + recursivity")

```js

	// 使用 reduce、concat 和递归展开无限多层嵌套的数组
	var arr1 = [1,2,3,[1,2,3,4, [2,3,4]]];
	
	function flatDeep(arr, d = 1) {
	   return d > 0 ?
	    arr.reduce((acc, val) => 
		    acc.concat(
			    Array.isArray(val) ?
			    flatDeep(val, d - 1) : val), [])
			    : arr.slice();
	};
	
	flatDeep(arr1, Infinity);
	// [1, 2, 3, 1, 2, 3, 4, 2, 3, 4]

```

Copy to Clipboard

### [forEach+isArray+push+recursivity](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat#foreachisarraypushrecursivity "Permalink to forEach+isArray+push+recursivity")

```js
// forEach 遍历数组会自动跳过空元素
const eachFlat = (arr = [], depth = 1) => {
  const result = []; // 缓存递归结果
  // 开始递归
  (function flat(arr, depth) {
    // forEach 会自动去除数组空位
    arr.forEach((item) => {
      // 控制递归深度
      if (Array.isArray(item) && depth > 0) {
        // 递归数组
        flat(item, depth - 1)
      } else {
        // 缓存元素
        result.push(item)
      }
    })
  })(arr, depth)
  // 返回递归结果
  return result;
}

// for of 循环不能去除数组空位，需要手动去除
const forFlat = (arr = [], depth = 1) => {
  const result = [];
  (function flat(arr, depth) {
    for (let item of arr) {
      if (Array.isArray(item) && depth > 0) {
        flat(item, depth - 1)
      } else {
        // 去除空元素，添加非 undefined 元素
        item !== void 0 && result.push(item);
      }
    }
  })(arr, depth)
  return result;
}
```

Copy to Clipboard

### [使用堆栈 stack](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat#%E4%BD%BF%E7%94%A8%E5%A0%86%E6%A0%88_stack "Permalink to 使用堆栈 stack")

// 无递归数组扁平化，使用堆栈
// 注意：深度的控制比较低效，因为需要检查每一个值的深度
// 也可能在 shift / unshift 上进行 w/o 反转，但是末端的数组 OPs 更快
var arr1 = [1,2,3,[1,2,3,4, [2,3,4]]];
function flatten(input) {
  const stack = [...input];
  const res = [];
  while (stack.length) {
    // 使用 pop 从 stack 中取出并移除值
    const next = stack.pop();
    if (Array.isArray(next)) {
      // 使用 push 送回内层数组中的元素，不会改动原始输入
      stack.push(...next);
    } else {
      res.push(next);
    }
  }
  // 反转恢复原数组的顺序
  return res.reverse();
}
flatten(arr1);// [1, 2, 3, 1, 2, 3, 4, 2, 3, 4]

// 递归版本的反嵌套
function flatten(array) {
  var flattend = [];
  (function flat(array) {
    array.forEach(function(el) {
      if (Array.isArray(el)) flat(el);
      else flattend.push(el);
    });
  })(array);
  return flattend;
}

### [Use `Generator` function](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat#use_generator_function "Permalink to Use Generator function")

```
function* flatten(array) {
    for (const item of array) {
        if (Array.isArray(item)) {
            yield* flatten(item);
        } else {
            yield item;
        }
    }
}

var arr = [1, 2, [3, 4, [5, 6]]];
const flattened = [...flatten(arr)];
// [1, 2, 3, 4, 5, 6]
```

Please do not add polyfills on this article. For reference, please check: [https://discourse.mozilla.org/t/mdn-rfc-001-mdn-wiki-pages-shouldnt-be-a-distributor-of-polyfills/24500](https://discourse.mozilla.org/t/mdn-rfc-001-mdn-wiki-pages-shouldnt-be-a-distributor-of-polyfills/24500)