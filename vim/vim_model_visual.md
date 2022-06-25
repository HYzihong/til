<!--
 * @Author: hy
 * @Date: 2022-07-24 12:14:53
 * @LastEditors: hy
 * @Description: 
 * @LastEditTime: 2022-07-24 12:33:50
 * @FilePath: /til/vim/vim_model_visual.md
 * Copyright 2022 hy, All Rights Reserved. 
 * 仅供学习使用~
-->

# visual 模式 

## vim 退出 `visual模式`操作

- `Esc`
- `C+[`
- 自定义映射 我映射了`jj`
- `v`
- `V`

> 直接进入 ` insert 模式`进行多行操作 需要使用 `visval 模式`时 `A`or`I`进行多行的前后插入操作
> 直接复制 `y`(or`Y`)再使用 `p`(or`P`) 将内容粘贴到光标处
> 思考什么时候使用 visual 模式,比如`v`+`e`+`d`可以替换成 `d`+`e`,使用 visual 模式就会增加操作量


## 选中（可视化）操作

- `v`: 光标选中一个字符
- `V`: 光标选中一行
  > `v` 和 `V` 任意切换
- `C+v`: 光标选块
  > - 多选 hjkl
  > - o 切换可视区域的光标位置
  > - gv 回到上一次选择的选中区域
