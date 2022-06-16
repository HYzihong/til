<!--
 * @Author: hy
 * @Date: 2022-06-16 23:12:07
 * @LastEditors: hy
 * @Description:
 * @LastEditTime: 2022-06-16 23:52:42
 * @FilePath: /til/vim/vim_substitute_operation.md
 * Copyright 2022 hy, All Rights Reserved.
 * 仅供学习使用~
-->

# 替换字符串

> 替换命令 `:substitute`

##### 替换公式 `:[range]s[ubstitute]/{pattern}/{string}/{flags} +enter`

##### rang

> 范围

- `$` ==> 到尾部
- `%` ==> 到全文
- number1,number2 ==> 到指定行 number1 到 number2

##### `[s]ubstitute`

##### pattern

要替换的字符串，支持正则表达式

##### flag

- g 全文匹配 默认只匹配到每行第一个
- c 对话框的形式进行替换
  - y 当前的要替换，并移到下一个
  - n 当前的不替换，并移到下一个
  - a 全部的要替换，并退出
  - l 当前的要替换，并退出
  - q 全部的不替换, 并退出

eg:

```javascript
//
vue;
// vue=> vvv :%s/vue/vvv + enter 全文的vue替换成vvv
// vue=> vvv :$s/vue/vvv + enter 行尾的vue替换成vvv
// vue=> vvv :2,3s/vue/vvv + enter 第2到第3行的vue替换成vvv
vvv;
//
d12c;
d12a;
d12d;

d12c sss d12c;
d12a `d12c` d12a;
d12d;
// hh1c ==>d12c
// hh2a ==>d12a
// hh3d ==>d12d
// :%s/hh\d/d12 + enter
//
```

##### 可视化模式下

> 全部替换，因为在可视化模式下已经指定了一个范围了，所以不需要指定范围

> 先进入可视化模式，在`:`开始输入 ，会自动生成`:<,>``

##### 多选操作

> `gb`

> 在一个字符串上按下 gb，会自动选中当前字符串，继续按会继续选中下一个匹配到的字符串,按下`c`进行编辑
> 区分大小写

```javascript
const a = "1234567890 hhhbd";
const b = "1234567890abd aa hhhbd Abd";
const c = "123456abd7890";
const d = "123 abd4567890";
```

adds another cursor on the next word it finds which is the same as the word under the cursor
