# forEach中执行push操作为什么不会造成死循环


先上代码：

```js

let arr = [1,2,3]

arr.forEach((item,index)=>{
	console.log(item,index)
	arr.push(item)
})

 // 1 0
 // 2 1
 // 3 2


```

我们思考，按道理每次循环判断时获取this.lenght后for循环就不会停止，造成死循环，所以我们试着写一下我们理解的源码：

```js
// 第一版
Array.prototype.mForEach = function(cb){
	// 这里的this每次都是会变化的
    for(let i = 0;i<this.length;i++){
        cb(this[i],i,this)
    }
}

let arr = [1,2,3]

arr.mForEach((item,index)=>{
	console.log(item,index)
	arr.push(item)
})



```

此时的确会死循环，所以原生的forEach肯定就不是这个逻辑，应该是一开始就把this.length缓存一份,所以第二版来了

```js
// 第二版
Array.prototype.mmForEach = function(cb){
	let _array = this
	let len = _array.length
    for(let i = 0;i<len;i++){
	    console.log('_len:',len,'this.length:',this.length,'_array:',_array,'item:',_array[i],'index:',i)
        cb(_array[i],i,_array)
    }
}


let arr = [1,2,3]

arr.mForEach((item,index)=>{
	// console.log(item,index)
	arr.push(item)
})

_len: 3 this.length: 3 _array: (3) [1, 2, 3] item: 1 index: 0
_len: 3 this.length: 4 _array: (4) [1, 2, 3, 1] item: 2 index: 1
_len: 3 this.length: 5 _array: (5) [1, 2, 3, 1, 2] item: 3 index: 2


```

---

扩展阅读：

1. [Array.prototype.forEach 源码分析)](https://zhuanlan.zhihu.com/p/385521894)

 作者实现的简易版 forEach:
```js

function forEach(callback, thisArg) {
  const array = this
  const len = array.length
  for (i = 0; i < len; i++) {
    callback.call(thisArg, array[i], i, array)
  }
  return undefined
}

```

2.  MDN-forEach

> [描述](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach#%E6%8F%8F%E8%BF%B0 "Permalink to 描述")
> `forEach()` 方法按升序为数组中含有效值的每一项执行一次 `callback` 函数，那些**已删除**或者**未初始化**的项将被跳过（例如在稀疏数组上）

3. [ecma262:sec-array.prototype.foreach](https://link.zhihu.com/?target=https%3A//tc39.es/ecma262/%23sec-array.prototype.foreach)

>23.1.3.15 Array.prototype.forEach ( callbackfn [ , thisArg ] )
> 
> NOTE 1
> 
> callbackfn should be a function that accepts three arguments. `forEach` calls callbackfn once for each element present in the array, in ascending order. callbackfn is called only for elements of the array which actually exist; it is not called for missing elements of the array.
> 
> If a thisArg parameter is provided, it will be used as the this value for each invocation of callbackfn. If it is not provided, undefined is used instead.
> 
> callbackfn is called with three arguments: the value of the element, the index of the element, and the object being traversed.
> 
> `forEach` does not directly mutate the object on which it is called but the object may be mutated by the calls to callbackfn.
 >  forEach不会直接改变调用它的对象，但可以通过调用callbackfn来改变对象。
> 
> The range of elements processed by `forEach` is set before the first call to callbackfn. Elements which are appended to the array after the call to `forEach` begins will not be visited by callbackfn. If existing elements of the array are changed, their value as passed to callbackfn will be the value at the time `forEach` visits them; elements that are deleted after the call to `forEach` begins and before being visited are not visited.
> forEach处理的元素范围在第一次调用callbackfn之前设置。callbackfn不会访问在forEach调用开始后添加到数组中的元素。如果数组中已有的元素被更改，传递给callbackfn的值将是forEach访问它们时的值;在forEach调用开始之后和访问之前删除的元素不会被访问。(机器翻译)
> 
> When the `forEach` method is called, the following steps are taken:
> 
> 1.  Let O be ? [ToObject](https://tc39.es/ecma262/#sec-toobject)(this value).
> 2.  Let len be ? [LengthOfArrayLike](https://tc39.es/ecma262/#sec-lengthofarraylike)(O).
> 3. If [IsCallable](https://tc39.es/ecma262/#sec-iscallable)(callbackfn) is false, throw a TypeError exception.
> 4. Let k be 0.
> 5. Repeat, while k < len.
> 
> 	a. Let Pk be ! [ToString](https://tc39.es/ecma262/#sec-tostring)([𝔽](https://tc39.es/ecma262/#%F0%9D%94%BD)(k)).
> 	
> 	b. Let kPresent be ? [HasProperty](https://tc39.es/ecma262/#sec-hasproperty)(O, Pk).
> 	
> 	c. If kPresent is true, then
> 	
> 	    1.  i. Let kValue be ? [Get](https://tc39.es/ecma262/#sec-get-o-p)(O, Pk).
>
> 	    2.  ii. Perform ? [Call](https://tc39.es/ecma262/#sec-call)(callbackfn, thisArg, « kValue, [𝔽](https://tc39.es/ecma262/#%F0%9D%94%BD)(k), O »).
>
> 	d. Set k to k + 1.
> 	    
> 6. Return undefined.
> 
