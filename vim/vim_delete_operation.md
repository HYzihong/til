<!--
 * @Author: hy
 * @Date: 2022-06-13 20:49:22
 * @LastEditors: hy
 * @Description:
 * @LastEditTime: 2022-07-24 13:41:18
 * @FilePath: /til/vim/vim_delete_operation.md
 * Copyright 2022 hy, All Rights Reserved.
 * 仅供学习使用~
-->

# 删除操作

> 删除函数的操作有:
>
> - [ ] 对单个字符串的删除
> - [ ] 对多个字符串的删除
> - [ ] 对函数的内容删除
> - [ ] 对函数的参数删除
> - [ ] 对函数的整个删除
> - [ ] 对在单行中某个字符串前后的删除
> - [ ] 对整行的删除
> - [ ] 对段落的删除

## `d`


语法：`d`+动作（范围）

### 单个字符串的删除

- 整个字符全部删除 `diw`
- 光标以前的前半个
- 光标以后的后半个字符的删除 `dL`

### 单行操作

- 单行全部删除 `dd`
- 光标以前的前半行的删除  `d0`
- 光标以后的后半行的删除 `dg_` 

#### 实例：

```js
function name(params) {
  return params;
}
```