# JS函数实现重载

### 什么是函数重载

-    函数重载是一个同名函数完成不同的功能，编译系统在编译阶段通过函数参数个数、参数类型不同，函数的返回值来区分该调用哪一个函数，即实现的是静态的多态性。但是记住：不能仅仅通过函数返回值不同来实现函数重载。
    
-    重载函数是指在同一作用域内，可以有一组具有相同函数名，不同参数列表的函数，这组函数被称为重载函数。
    

**总结**：函数名相同，函数的参数不同(包括参数个数和参数类型)，根据参数的不同去执行不同的操作。


### 我们为什么需要重载



  ---
  

##### 根据arguments对象的length值进行判断

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


 ##### 利用对象和闭包特性

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



<!--  TODO测试ts 重载会生成什么ES5代码 -->