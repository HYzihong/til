<!--
 * @Author: hy
 * @Date: 2022-06-09 23:24:18
 * @LastEditors: hy
 * @Description:
 * @LastEditTime: 2022-06-10 17:47:04
 * @FilePath: /til/vim/vim_search_in_file.md
 * Copyright 2022 hy, All Rights Reserved.
 * 仅供学习使用~
-->

# 文件内搜索

## 单行搜索

- `f` 正向（向右）移动到下一个匹配的字符
- `F` 反向（向左）移动到下一个匹配的字符
- `t` 正向移动到下一个字符所在位置的前一个字符上
- `T` 反向移动到下一个字符所在位置的后一个字符上
- `;` 重复上一个搜索操作
- `,` 反转方向重复上一个搜索操作

```js
function fff(f) {
  retrun f; // 1//
}
```

> 只会在一行内进行搜索，搜索结束会听到搜到的最后一个字符上

> 使用技巧：
> 正常移动查找字符的时候使用 f
> 操作最好使用`t` or `T`结合进行操作

## 全局搜索

- `/+搜索的字符+enter(回车键)` 全局搜索向后查找
- `?+搜索的字符+enter(回车键)` 全局搜索向前查找
- `n/N` 下一个 / 上一个
- `/+方向键的上下` 查看搜索历史
- `#` 向上查找
- `*` 向下查找