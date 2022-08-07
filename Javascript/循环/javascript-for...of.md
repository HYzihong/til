# for...of


> https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...of



**`for...of`语句**在[可迭代对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Iteration_protocols)（包括 [`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)，[`Map`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Map)，[`Set`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set)，[`String`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String)，[`TypedArray`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/TypedArray)，[arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/arguments) 对象等等）上创建一个迭代循环，调用自定义迭代钩子，并为每个不同属性的值执行语句。


### 语法

```js

for (variable of iterable) {
    //_statements_
}
```

`variable`

在每次迭代中，将不同属性的值分配给变量。

`iterable`

被迭代枚举其属性的对象。


#### `for of`   vs  `for in`

> [[javascript-for...in]]

无论是`for...in`还是`for...of`语句都是迭代一些东西。它们之间的主要区别在于它们的迭代方式。

`for...in` 语句以**任意顺序**迭代对象的**可枚举属性**。

`for...of` 语句遍历可迭代对象定义**要迭代的数据**。

```js

Object.prototype.objCustom = function() {};
Array.prototype.arrCustom = function() {};

let iterable = [3, 5, 7];
iterable.foo = 'hello';

for (let i in iterable) {
  console.log(i); 
}
// logs 
// 数组索引 0->2
// 0
// 1
// 2
// "foo"
// "arrCustom" 继承自 Array.prototype
// "objCustom" 继承自 Object.prototype

for (let i in iterable) {
  if (iterable.hasOwnProperty(i)) {
    console.log(i); 
  }
}
// logs 
// 0
// 1
// 2
// "foo"

for (let i of iterable) {
  console.log(i); 
}
// logs 
// 3
// 5
// 7

```



### 案例

```js

// 

let iterable = [10, 20, 30];

for (let value of iterable) {
    value += 1;
    console.log(value);
}
// 11
// 21
// 31

// 防止更改原数组
let iterable = [10, 20, 30];

for (const value of iterable) {
  value+2
  console.log(value);
}
console.log(iterable)
// 10
// 20
// 30
// Array [10, 20, 30]

// 迭代String
let iterable = "boo";

for (let value of iterable) {
  console.log(value);
}
// "b"
// "o"
// "o"

// 迭代类数组
let iterable = new Uint8Array([0x00, 0xff]);

for (let value of iterable) {
  console.log(value);
}
// 0
// 255


// 迭代Map
let iterable = new Map([["a", 1], ["b", 2], ["c", 3]]);

for (let entry of iterable) {
  console.log(entry);
}
// ["a", 1]
// ["b", 2]
// ["c", 3]

for (let [key, value] of iterable) {
  console.log(value);
}
// 1
// 2
// 3

// 迭代Set
let iterable = new Set([1, 1, 2, 2, 3, 3]);

for (let value of iterable) {
  console.log(value);
}
// 1
// 2
// 3

// 迭代 argument 对象
(function() {
  for (let argument of arguments) {
    console.log(argument);
  }
})(1, 2, 3);

// 1
// 2
// 3

//迭代 DOM 元素集合，比如一个[`NodeList`](https://developer.mozilla.org/zh-CN/docs/Web/API/NodeList)对象：下面的例子演示给每一个 article 标签内的 p 标签添加一个 "`read`" 类。

//注意：这只能在实现了 NodeList.prototype[Symbol.iterator] 的平台上运行

let articleParagraphs = document.querySelectorAll("article > p");

for (let paragraph of articleParagraphs) {
  paragraph.classList.add("read");
}

// 关闭迭代器
// 对于`for...of`的循环，可以由 `break`, `throw` 或 `return` 终止。在这些情况下，迭代器关闭。

function* foo(){
  yield 1;
  yield 2;
  yield 3;
};

for (let o of foo()) {
  console.log(o);
  break; // closes iterator, triggers return
}
// 1

// 生成迭代器

function* fibonacci() { // 一个生成器函数
    let [prev, curr] = [0, 1];
    for (;;) { // while (true) {
        [prev, curr] = [curr, prev + curr];
        yield curr;
    }
}

for (let n of fibonacci()) {
     console.log(n);
    // 当 n 大于 1000 时跳出循环
    if (n >= 1000)
        break;
}



var gen = (function *(){
    yield 1;
    yield 2;
    yield 3;
})();
for (let o of gen) {
    console.log(o);
    break;//关闭生成器
}

//生成器不应该重用，以下没有意义！
for (let o of gen) {
    console.log(o);
}

// 1



// 迭代其他可迭代对象
var iterable = {
  [Symbol.iterator]() {
    return {
      i: 0,
      next() {
        if (this.i < 3) {
          return { value: this.i++, done: false };
        }
        return { value: undefined, done: true };
      }
    };
  }
};

for (var value of iterable) {
  console.log(value);
}
// 0
// 1
// 2

```



### 兼容性

IE不支持