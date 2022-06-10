<!--
 * @Author: hy
 * @Date: 2022-06-08 23:16:09
 * @LastEditors: hy
 * @Description:
 * @LastEditTime: 2022-06-09 00:02:43
 * @FilePath: /til/vim/in_file_operation.md
 * Copyright 2022 hy, All Rights Reserved.
 * 仅供学习使用~
-->

# 单文件中移动

### 基础滚动

- 向下滚动一屏`C+f` (f-forward)
- 向上滚动一屏`C+b` (b-backward)
- 向下滚动半屏`C+d` (d-down)
- 向上滚动半屏`C+u` (u-up)
- 向下滚动一行`C+o`
- 向上滚动一行`C+y`
  > 一行的移动是不会影响光标的位置
- 向下移动多行`${行数}+j`
- 向上移动多行`${行数}+k`

##### 基于配置的易用性改造

- setting.json

```json

    {
      "before": ["H"],
      "after": ["^"] // 快速移动到行首
    },
    {
      "before": ["L"],
      "after": ["g", "_"] // 快速移动到行尾
    },
    {
      "before": ["J"],
      "after": ["5", "j"] // 快速向下移动5行
    },
    {
      "before": ["K"],
      "after": ["5", "k"] // 快速向上移动5行
    }

```

### 特殊操作

- 将当前行置于屏幕中央 `zz`
- 将当前行置于屏幕顶部 `zt`(t-top)
- 将当前行置于屏幕底部 `zb`(b-bottom)
- 跳到文件首行 `gg`
- 跳到文件尾行 `G`
- 跳到文件指定行数 `${行数}gg` + `${行数}G`
