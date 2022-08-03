# JS函数实现重载


---


### 什么是函数重载

-    函数重载是一个同名函数完成不同的功能，编译系统在编译阶段通过函数参数个数、参数类型不同，函数的返回值来区分该调用哪一个函数，即实现的是静态的多态性。但是记住：不能仅仅通过函数返回值不同来实现函数重载。
    
-    重载函数是指在同一作用域内，可以有一组具有相同函数名，不同参数列表的函数，这组函数被称为重载函数。
    

**总结**：函数名相同，函数的参数不同(包括参数个数和参数类型)，根据参数的不同去执行不同的操作。


### 我们为什么需要重载

<!--todo -->

1. 减少了函数名的数量，避免了名字空间的污染，对于程序的可读性有很大的好处。 在强类型语言中(如`Java`)，因为有数据类型的限制，很多构造函数实现功能类似，但接收的数据类型不同，如果没有函数重载，那么构造函数要为每一种数据类型分别命名。 
    但是JavaScript作为弱类型语言，不存在这种问题，函数可以任意接受参数，那这种情况下为啥要强行模拟一个所谓'函数重载'呢。其实一个粗糙的例子就可以很好的说明问题： 一个数组，调用一个函数，不传参返回原数组，一个参数是数字时返回对应下标内容，，两个参数(数字)时，返回对应数组下标截取，返回新数组。
	正常情况下，针对不定量的参数对应不同的操作内容，我们需要写三个对应的函数，三个变量名，但其实是一套逻辑程序的三个功能。
	
	 
2. 将你从数据结构或格式类型中解放思维，关注函数的抽象概念和其提供的功能逻辑设计。 例子：Array.splice()

3. 针对已存在的正在使用的公共函数的修改与扩展提供另类可行思路。（可借用的有意义思路） 例子：已存在工具函数(例1)并在项目内大量使用，现在需求要在此基础上修改第三个参数，在第三个参数为固定内容时，对数组进行统一格式化处理。 见底部 


<!-- js 是否有函数重载的例子 -->

  ---
  

##### 1. 根据arguments对象的length值进行判断

```js

function funcOverLoading() {
　　// 根据arguments.length，对不同的值进行不同的操作
　　switch(arguments.length) {
　　　　case 0:
　　　　　　/*操作1的代码写在这里*/
　　　　　　break;
　　　　case 1:
　　　　　　/*操作2的代码写在这里*/
　　　　　　break;
　　　　case 2:
　　　　　　/*操作3的代码写在这里*/
 　　　　　　
　　//后面还有很多的case......
}
 
}

funcOverLoading(arg1)
funcOverLoading(arg1,arg2)
funcOverLoading(arg1,arg2,arg3)

```

优点：通俗易懂，实现简单
缺点：不便于维护和扩展，有时也需要判断数据类型


##### 2.利用对象和闭包特性
 

> JQuery之父John Resig写的《secrets of the JavaScript ninja》(《JavaScript忍者秘籍》) 中提到的一种方法

主要核心思路是利用`闭包`的原理，将不同的函数以相同的属性名层层嵌套在传入的对象中，将对象与对应的方法名设计好后，利用`arguments传入参数`与`fn实际所需参数`对比判断真正的执行函数。

```js

//addMethod
function addMethod(object, name, fn) {
　　var old = object[name]; //把前一次添加的方法存在一个临时变量old里面
　　object[name] = function() { // 重写了object[name]的方法
　　　　// 如果调用object[name]方法时，传入的参数个数跟预期的一致，则直接调用
　　　　if(fn.length === arguments.length) {
　　　　　　return fn.apply(this, arguments);
　　　　// 否则，判断old是否是函数，如果是，就调用old
　　　　} else if(typeof old === "function") {
　　　　　　return old.apply(this, arguments);
　　　　}
　　}
}
 
 
var people = {
　　values: ["Dean Edwards", "Alex Russell", "Dean Tom"]
};
 
/* 下面开始通过addMethod来实现对people.find方法的重载 */
 
// 不传参数时，返回peopld.values里面的所有元素
addMethod(people, "find", function() {
　　return this.values;
});
 
// 传一个参数时，按first-name的匹配进行返回
addMethod(people, "find", function(firstName) {
　　var ret = [];
　　for(var i = 0; i < this.values.length; i++) {
　　　　if(this.values[i].indexOf(firstName) === 0) {
　　　　　　ret.push(this.values[i]);
　　　　}
　　}
　　return ret;
});
 
// 传两个参数时，返回first-name和last-name都匹配的元素
addMethod(people, "find", function(firstName, lastName) {
　　var ret = [];
　　for(var i = 0; i < this.values.length; i++) {
　　　　if(this.values[i] === (firstName + " " + lastName)) {
　　　　　　ret.push(this.values[i]);
　　　　}
　　}
　　return ret;
});
 
// 测试：
console.log(people.find()); //["Dean Edwards", "Alex Russell", "Dean Tom"]
console.log(people.find("Dean")); //["Dean Edwards", "Dean Tom"]
console.log(people.find("Dean","Edwards")); //["Dean Edwards"]


// 展开看people对象
people
	{values: Array(3), find: ƒ}
		find: ƒ ()
		arguments: null
		caller: null
		length: 0
		name: ""
		prototype: {constructor: ƒ}
		[[FunctionLocation]]: VM341:3
		[[Prototype]]: ƒ ()
		[[Scopes]]: Scopes[2]
			0: Closure (addMethod)
				fn: ƒ (firstName, lastName)
				old: ƒ () //
					arguments: null
					caller: null
					length: 0
					name: ""
					prototype: {constructor: ƒ}
					[[FunctionLocation]]: VM341:3
					[[Prototype]]: ƒ ()
					[[Scopes]]: Scopes[2]
						0: Closure (addMethod)
							fn: ƒ (firstName)
							old: ƒ () //
								arguments: null
								caller: null
								length: 0
								name: ""
								prototype: {constructor: ƒ}
								[[FunctionLocation]]: VM341:3
								[[Prototype]]: ƒ ()
								[[Scopes]]: Scopes[2]
									0: Closure (addMethod)
										fn: ƒ ()
										old: undefined  // 
											[[Prototype]]: Object
											1: Global {0: Window, 1: Window, window: Window, self: Window, document: document, name: '', location: Location, …}
											[[Prototype]]: Object
											1: Global {0: Window, 1: Window, window: Window, self: Window, document: document, name: '', location: Location, …}
											[[Prototype]]: Object
											1: Global {0: Window, 1: Window, window: Window, self: Window, document: document, name: '', location: Location, …}
	values: (3) ['Dean Edwards', 'Alex Russell', 'Dean Tom']
	[[Prototype]]: Object

```
优点：逻辑清晰可读性高，方便扩展
缺点：代码量会很大


##### 3. 利用ES6可选参数

```js

function funcOverLoading(arg1=null,arg2=null) {
	this.arg1 = arg1; this.arg2 = arg2;
	if(arg1!==null && arg2!==null) return `${arg1} and ${arg2}`
	 if(arg1!==null) return `${arg1}`
    return 'return null'

}
 

funcOverLoading() // 'return null'
funcOverLoading(1) // '1
funcOverLoading(1,2) // '1 and 2'

```

优缺点同->1. 根据arguments对象的length值进行判断

<!--  TODO测试ts 重载会生成什么ES5代码 -->



---



参考：

1. [浅谈JavaScript函数重载](https://www.cnblogs.com/yugege/p/5539020.html)
2. [JS的函数重载](https://juejin.cn/post/6844903933480009741)