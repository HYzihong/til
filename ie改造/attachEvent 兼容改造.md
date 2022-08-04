# attachEvent 兼容改造

今天访问了公司一个远古系统，Chrome报错 ` xxx.attachEvent is not a function ` ，我想了一下，可能是ie专用方法，我又去 `IE11`（1809）使用，还报错。

在 IE7,8的绑定事件方法 ，IE不支持 `addEventListener`  和  `removeEventListener` 方法 , 所以用   `attachEvent` 和  `detachEvent`   。

### 语法:

`attachEvent(事件类型, 处理函数);`
> `addEventListener(事件类型, 处理函数, 使用捕获);`


```js
// 方法必须带 on 前缀 onclick，onmouseove
btn = document.getElementById("btn");
btn.attachEvent('onclick',function(){{alert('1');});
btn.attachEvent('onclick',function(){{alert('2');});
btn.attachEvent('onclick',function(){{alert('3');}); 
// this => window
// 执行顺序 后绑定先执行 3，2，1
//
btn = document.getElementById("btn");
btn.addEventListener('click',function(){{alert('1');},false);
obj.addEventListener('click',function(){{alert('2');},false);
btn.addEventListener('click',function(){{alert('3');},false);
// 执行顺序 先绑定先执行 1，2，3

```


### 兼容性

- attachEvent 
只兼容`IE7、IE8`
不兼容firefox、chrome、IE9+、safari、opera  
addEventListener
- 兼容：firefox、chrome、IE9+、safari、opera
不兼容IE7、IE8

- 网上的兼容代码:

```js

function addEvent(elm, evType, fn, useCapture) 
{
    if (elm.addEventListener) {
        // W3C标准
        elm.addEventListener(evType, fn, useCapture);
        return true;
    }
    else if (elm.attachEvent) {
        //IE
        var r = elm.attachEvent(‘on‘ + evType, fn);//IE5+
        return r;
    }
    else {
        elm['on' + evType] = fn;//DOM事件
    }
}

```

更多见[link>](https://www.cnblogs.com/dacuotecuo/p/3510823.html)

