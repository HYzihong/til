# JavaScript 创建一个[1...100]的数组

代码示例：

```javascript
let arr = []
// push方法
for(let i = 1,len=100;i<=100;i++){arr.push(i)}
//  or
//循环赋值
for(let i = 1,len=100;i<=100;i++){arr[i-1]=i}
// Array.from()方法 后面会有一点点的优化
Array.from({length:101}, (v,k) => k)
// or Array.from(Array(101), (v,k) =>k);
Array.from(Array(101).keys())
arr.splice(0,1)

// 使用递归实现
// 当前值
// 最大长度
let arr = []
function setArray(current,maxLength,arr){
  if(arr.length<maxLength){
    arr[current-1] = current
    setArray(++current,maxLength,arr)
  }else{
      arr.filter(i=>i)// 去除假值 empty
  }
}
setArray(1,100,arr)
// 暂且不知道有没有性能问题

// 在网上看到一些方法，也蛮好玩的，但是不知道来源

// 1
//let arr = Array(101).toString().split(',').map((item,index)=>index)// 0-> 99
let arr = Array(101).toString().split(',').map((item,index)=>index+1)// 1-> 100

// 2
//let i = 0,arr = [];
//let timer = setInterval(function(){
//  arr[i] = i++;
//  if(i>=100){
//    clearInterval(timer);
//    console.log(arr);
//  }
//},1); // 0-> 99
let i = 1,arr = [];
let timer = setInterval(function(){
  arr[i-1] = i++;
  if(i>100){
    clearInterval(timer);
    console.log(arr);
  }
},1); // 1-> 100


// 3
Object.keys(Array.apply(null, {length:100})).map(item=>+item);// 0-> 99

// 4
[...Array(100).keys()]// 0-> 99
[...Array(101).keys()].splice(1,101)// 1->100
[...Array.from({length:100}).keys()]// 0-> 99

// mdn 看见的 序列生成器(指定范围)
const range = (start, stop, step) => Array.from({ length: (stop - start) / step + 1}, (_, i) =>  + (i * step));

range(1,100,1)// 1-> 100

//优化我上面写的
Array.from({length:100},(_, i)=>1+(i)) // 1-> 100
```



----

前提知识：

#### `Array.from()`

> [`Array.from(arrayLike[, mapFn[, thisArg]])`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
>
> - `arrayLike`
>
>   想要转换成数组的伪数组对象或可迭代对象。
>
> - `mapFn` 可选
>
>   如果指定了该参数，新数组中的每个元素会执行该回调函数。
>
> - `thisArg` 可选
>
>   可选参数，执行回调函数 `mapFn` 时 `this` 对象。
>
>   **返回值**
>
>   一个新的`数组`实例。

用法：

- String 生成 数组
- Set 生成 数组
- Map 生成 数组
- 类数组 生成 数组

示例：从Map生成数组

```javascript
const map = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(map);
// [[1, 2], [2, 4], [4, 8]]

const mapper = new Map([['1', 'a'], ['2', 'b']]);
Array.from(mapper.values());
// ['a', 'b'];

Array.from(mapper.keys());
// ['1', '2'];
```

其他：

```javascript
Array.from({length: 100}) or  Array.from(Array(100))

// 都会生成
(100) [undefined,..., undefined]
```



#### 数组实例方法`keys()`

keys()是ES6中新增的对键名的遍历,返回一个遍历器对象



#### [`apply(thisArg, [argsArray])`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

> ### 参数
>
> - `thisArg`
>
>   必选的。在 *`func`* 函数运行时使用的 `this` 值。请注意，`this`可能不是该方法看到的实际值：如果这个函数处于[非严格模式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)下，则指定为 `null` 或 `undefined` 时会自动替换为指向全局对象，原始值会被包装。
>
> - `argsArray`
>
>   可选的。一个数组或者类数组对象，其中的数组元素将作为单独的参数传给 `func` 函数。如果该参数的值为 `null` 或 `undefined`，则表示不需要传入任何参数。从ECMAScript 5 开始可以使用类数组对象。
>
> ### 返回值
>
> 调用有指定`this`值和参数的函数的结果。

