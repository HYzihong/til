# 怎么样让forEach 支持跳出循环

>  除了抛出异常以外，没有办法中止或跳出 `forEach()` 循环。


所以我们想让forEach支持中止或跳出循环，需要写在`try/cach`中：

```js

let arr = [0, 1, 2, 3];
try {
    arr.forEach(item => {
        if (item > 2 ) {
            throw new Error("break");
        }
        console.log(item);
    });
} catch (e) {
    console.log(e.message); // break
};

// 0
// 1
// 2
// break

```

看起来当循环体越来越大，代码的可读性和性能都会降低
当然 `for each`的中文就是`每一个`,对于跳出循环这种需求我们最好使用`for`循环


网上很火的修改源码的方法：

```js

Array.prototype.mForEach = function (fn) {
    for (let i = 0; i < this.length; i++) {
        let res = fn(this[i], i, this);
        if (typeof res !== "undefined" && (res == null || res == false)) break;
    }
}

```

---

扩展：


#### 支持跳出循环的循环方法

-   一个简单的 `for` 循环  （最常用的）
-   `for...of` / `for...in` 循环
-   `Array.prototype.every()`
-   `Array.prototype.some()`
-   `Array.prototype.find()
-   `Array.prototype.findIndex()`
