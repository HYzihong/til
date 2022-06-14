<!--
 * @Author: hy
 * @Date: 2022-06-14 21:58:59
 * @LastEditors: hy
 * @Description:
 * @LastEditTime: 2022-06-16 23:12:17
 * @FilePath: /til/vim/vim_surround_plugin.md
 * Copyright 2022 hy, All Rights Reserved.
 * 仅供学习使用~
-->

# vim-surround

> 处理包裹字符的符号

### Change existing surround to desired

> `cs<existing><desired>`

```javascript
// const a ="${name}" ==> `${name}` cs"`
// const a =`${name}` ==> '${name}' cs`'
// const a =`${name}` ==> "${name}" cs`"
const a = "${name}";
// [a] ==> {a} cs[{
const a = { a };
```

### Add desired surround around text defined by

> `ys<motion><desired>`

```javascript
// add ==> {add} `ys+iw(范围 text object)+{`
// {add} ==> add `ds+{`
import add from "./add";

const a = "${name}";
```

### Delete existing surround

> `ds<existing>`

### Surround when in visual model (surround full selection)

> `S<desired>`
