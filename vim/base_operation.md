<!--
 * @Author: hy
 * @Date: 2022-06-05 18:14:29
 * @LastEditors: hy
 * @Description:
 * @LastEditTime: 2022-06-05 23:30:02
 * @FilePath: /til/vim/base_operation.md
 * Copyright 2022 hy, All Rights Reserved.
 * 仅供学习使用~
-->

# vim

### 三种模式

insert 模式：插入模式
normal 模式：普通模式

### 基本操作

#### 上下左右

h: 向左移动一个字符
j: 向下移动一个字符
k: 向上移动一个字符
l: 向右移动一个字符

#### vim 退出 `insert模式`操作

- `Esc`
- `C+[`
- 自定义映射 我映射了`jj`

#### 进入 `insert 模式`

- `I`
- `A`
- `O`
- `o`

#### 复制粘贴操作

- `yy`: 复制当前行
<!-- TODO 复制单个字符 复制单个单词 多选复制 多行复制-->

#### 删除操作

- `dd` 删除当前行
<!-- TODO 删除单个字符 删除单个单词 删除复制 删除复制-->
