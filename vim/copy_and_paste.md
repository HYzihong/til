<!--
 * @Author: hy
 * @Date: 2022-06-10 17:51:07
 * @LastEditors: hy
 * @Description:
 * @LastEditTime: 2022-06-13 20:58:55
 * @FilePath: /til/vim/copy_and_paste.md
 * Copyright 2022 hy, All Rights Reserved.
 * 仅供学习使用~
-->

# vim 复制粘贴操作

#### 复制粘贴操作

- `yy`: 复制当前行
<!-- TODO 复制单个字符 复制单个单词 多选复制 多行复制-->
- `p`: 粘贴

> vim 跟系统的复制粘贴走的不是同一个，vim 复制删除走的是寄存器，所以`yy+p` 和`command c + command v`可以共存

- - `y+动作（范围）`：复制一个范围

#### 删除操作

- `dd` 删除当前行
<!-- TODO 删除单个字符 删除单个单词 删除复制 删除复制-->

> 因为删除` dd` 走的是也是 vim 寄存器，所以在 `dd` 之后也可以做 `p` 操作
