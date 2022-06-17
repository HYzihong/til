<!--
 * @Author: hy
 * @Date: 2022-06-18 17:35:07
 * @LastEditors: hy
 * @Description:
 * @LastEditTime: 2022-06-18 18:29:38
 * @FilePath: /til/vim/vim_case_switch_operation.md
 * Copyright 2022 hy, All Rights Reserved.
 * 仅供学习使用~
-->

# 大小写切换

### normal 模式下

> `gu`

> `gU`
> 多用于定义常量

```javascript
const a = `absdD`;
// absdD ==> absdd `guiw`
// absdD ==> absdD `gUiw`
//
```

### 可视化模式下

> `u`

范围中全部小写

> `U`

范围中全部大写

### 单个字母的大小写切换

> `~`
