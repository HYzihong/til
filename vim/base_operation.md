<!--
 * @Author: hy
 * @Date: 2022-06-05 18:14:29
 * @LastEditors: hy
 * @Description:
 * @LastEditTime: 2022-06-10 17:57:50
 * @FilePath: /til/vim/base_operation.md
 * Copyright 2022 hy, All Rights Reserved.
 * 仅供学习使用~
-->

# vim

### 三种模式

insert 模式：插入模式
normal 模式：普通模式
visual 模式：选择(可视化)模式

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

#### vim 退出 `visual模式`操作

- `Esc`
- `C+[`
- 自定义映射 我映射了`jj`
- `v`
- `V`

> 直接进入 ` insert 模式`进行多行操作 需要使用 `visval 模式`时 `A`or`I`进行多行的前后插入操作
> 直接复制 `y`(or`Y`)再使用 `p`(or`P`) 将内容粘贴到光标处
> 思考什么时候使用 visual 模式,比如`v`+`e`+`d`可以替换成 `d`+`e`,使用 visual 模式就会增加操作量

#### 进入 `insert 模式`

- `I`
- `A`
- `O`
- `o`

#### 移动操作

- `0`: 光标移动到行首
- `^`: 光标移动到行首的第一个不是 `block 字符`(空格、Tab、换行、回车等)的位置

```js
function a() {
  return 1;
}
```

#### 选中（可视化）操作

- `v`: 光标选中一个字符
- `V`: 光标选中一行
  > `v` 和 `V` 任意切换
- `C+v`: 光标选块
  > - 多选 hjkl
  > - o 切换可视区域的光标位置
  > - gv 回到上一次选择的选中区域

#### 文本对象

> 文本是结构的，可以快速选择
> 有一定选择范围

##### 语法

operator + 内部 or 外部 + 文本对象

##### 内部 + 外部

内部 : `i`
外部 : `a`

##### 一些文本对象

- `w`: 单词
  > 例子:`viw`,`diw`or `vaw`,`daw`
- `(`or`)` or `b`: ()
- `[`or`]` : []
- `{`or`}` or `B`: {}
- `<`or`>`: `<>`
- t :xml 标签
- ' : ''
- " : ""
- ` : ``
- s: 一个句子
- p : 一个段落
- vim-text-arguments
  - ia : 不包含分隔符
  - aa : 包含分隔符
  - 技巧:
    - 删掉一个参数 `daa`
    - 修改一个参数 `iaa`
- vim-text-entire
  - ae 删除当前文本所有内容
  - ie 删除当前文本所有内容,但是不包含前后的空格

```javascript
function a(str string,arr string[]) {
  return 1;
}


const w = 'hello';
const w = `hevllo`;
const w = "hello";


```

```html
<div>div</div>
```

> 注意事项：
>
> 1. `viw` 框选此处单词，`ve` 框选的是光标到单词末尾
> 2. `a` 默认优先选中尾部的空格，然后才会选中头部的空格
> 3. vim 中只有以 . ? ! 结尾的才算一个完整的句子的结束
