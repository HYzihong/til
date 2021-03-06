<!--
 * @Author: hy
 * @Date: 2022-06-13 23:09:42
 * @LastEditors: hy
 * @Description:
 * @LastEditTime: 2022-06-14 16:09:57
 * @FilePath: /til/vim/vim_jump_operation.md
 * Copyright 2022 hy, All Rights Reserved.
 * 仅供学习使用~
-->

# 跳转操作

### 理解跳转

- 任何大于一个单词或超过当前行导航的移动都是一个跳转

- 一些跳转操作

  - '
  - `
  - gg
  - /
  - ?
  - n
  - N
  - gd
  - {
  - }

- 一些不会记录的操作
  - 翻页
  - 自定义的（改）键
- 特别说明 `vim-sneak` 的跳转只记录一次

### 标记跳转

##### 标记

- 单文件之间的跳转的时候所用标记 `m+小写字母` 一般为`mm`
- 多文件之间的跳转的时候所用标记 `m+大写字母` 一般为`mM`

> 可以同时记录多个标记

##### 跳转

- ' 跳转到标记行
- ` 跳转到标记所在位置 （行+列）

### 跳转到定义

`gd`

- `j` `k` 可以上下选择
- `h` `l` 可以实现折叠展开的操作

### 跳转历史操作

- 向（历史跳转的下一次）后跳转 `CTRL+i`
- 向（历史跳转的上一次）前跳转 `CTRL+o`
