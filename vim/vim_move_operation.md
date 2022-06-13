<!--
 * @Author: hy
 * @Date: 2022-06-13 21:00:02
 * @LastEditors: hy
 * @Description:
 * @LastEditTime: 2022-06-13 21:00:24
 * @FilePath: /til/vim/vim_move_operation.md
 * Copyright 2022 hy, All Rights Reserved.
 * 仅供学习使用~
-->

# 移动操作

#### 上下左右

- 向左移动一个字符 : `h`
- 向下移动一个字符 : `j`
- 向上移动一个字符 : `k`
- 向右移动一个字符 : `l`

### 移动到行首

- `0`
- `^`
  - 到本行第一个不是 blank 字符的位置

---

> vscode settings.json

```json
{
  "before": ["H"],
  "after": ["^"] // 快速移动到行首
}
```

# 移动到行尾

- `$`
- `g_`
  - 到本行最后一个不是 blank 字符的位置

---

> vscode settings.json

```json
{
  "before": ["L"],
  "after": ["g", "_"] // 快速移动到行尾
}
```
