<!--
 * @Author: hy
 * @Date: 2022-06-13 20:49:22
 * @LastEditors: hy
 * @Description:
 * @LastEditTime: 2022-06-21 20:18:32
 * @FilePath: /til/vim/vim_delete_operation.md
 * Copyright 2022 hy, All Rights Reserved.
 * 仅供学习使用~
-->

# 删除操作

> 删除函数的操作有:
>
> - 对单个字符串的删除
> - 对多个字符串的删除
> - 对函数的内容删除
> - 对函数的参数删除
> - 对函数的整个删除
> - 对在单行中某个字符串前后的删除
> - 对整行的删除
> - 对段落的删除

### `d`

```js
function name(params) {
  return params;
}
```

d+动作（范围）

#### 实例：

#### 对在单行中某个字符串前后的删除

- 前 `dL`
- 后 `dH`

#### 单个字符串的删除

- `diw`
