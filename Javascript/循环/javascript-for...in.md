# for...in

> https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in

**`for...in`语句**以任意顺序迭代一个对象的除[Symbol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)以外的[可枚举](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Enumerability_and_ownership_of_properties)属性，包括继承的可枚举属性。

主要是对于键值对（对象）的属性进行检查，不建议用于关注索引的array这种类型

### 语法

```js

for (variable in object)
  statement

```

##### 参数

`variable`

在每次迭代时，variable 会被赋值为不同的属性名。

`object`

非 Symbol 类型的可枚举属性被迭代的对象。

#### 优缺点


优点:

1.  方便遍历对象的属性

缺点：

1.  会遍历出对象上可枚举的方法(`Object.defineProperty(xxx,'xxx',{value:function(){},emumerable:false// 不可枚举})`)
2. 如果有关注索引的数组类型进行`for in`    ，可能会出现网上所说的 顺序错乱问题，而且 `for in`    遍历的    `variable`    类型是 `string` ，会出现类型转化问题
```


### 案例

```js

var triangle = {a: 1, b: 2, c: 3};

function ColoredTriangle() {
  this.color = 'red';
}

ColoredTriangle.prototype = triangle;

var obj = new ColoredTriangle();

for (var prop in obj) {console.log(prop)}
// output:
// color
// a
// b
// c


// 输出对象本身的属性，而不是它的原型
for (var prop in obj) {
  if (obj.hasOwnProperty(prop)) {// hasOwnProperty 继承的属性不显示
    console.log(`obj.${prop} = ${obj[prop]}`);
  }
}

// Output:
// "obj.color = red"

```

> 只针对对象本身的属性可以用 [[javascript-object-propertyIsEnumerable]]  、 [[javascript-object-hasOwnProperty]]  、  [[javascript-object-getOwnPropertyNames]]   进行约束


### 兼容性

- IE3+
- [Firefox 40+](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in#%E5%85%BC%E5%AE%B9%E6%80%A7%EF%BC%9A%E5%88%9D%E5%A7%8B%E5%8C%96%E5%87%BD%E6%95%B0%E8%A1%A8%E8%BE%BE%E5%BC%8F)