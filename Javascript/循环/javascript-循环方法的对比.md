# 循环方法的对比

| 方法名称  | 可循环的数值类型      | 参数                                                      | 优点                              | 缺点                                            | 兼容性                            |
| --------- | --------------------- | --------------------------------------------------------- | --------------------------------- | ----------------------------------------------- | --------------------------------- |
| `forEach` | Array、Map、Set       | value,index,array(详见:[[javascript-array-forEach#参数]]) | 代码简洁，不需要关注下标问题;     | 1. callback中不支持异步 ； 2. 无法正常跳出循环; | IE9+                              |
| `for in`    | Array(不建议)、Object | variable 、object （详见：[[javascript-for...in#参数]]）  | 方便遍历键值对类型的数据进行遍历; |                                                 | -([[javascript-for...in#兼容性]]) |
|   `for of`        |    任何可迭代对象（Array,Map,Set,String,TypedArray,arguments）                   |                                                           |                                   |                                               |         IE不兼容                            |





----

参考：

1. [[javascript-array-forEach]]
2. [[javascript-for...in]]
3. [[javascript-for...of]]