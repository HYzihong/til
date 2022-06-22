<!--
 * @Author: hy
 * @Date: 2022-07-24 12:32:54
 * @LastEditors: hy
 * @Description: 
 * @LastEditTime: 2022-07-24 12:36:12
 * @FilePath: /til/vim/vim_text_object.md
 * Copyright 2022 hy, All Rights Reserved. 
 * 仅供学习使用~
-->

# 文本对象

> 文本是结构的，可以快速选择
> 有一定选择范围

## 语法

operator + 内部 or 外部 + 文本对象

## 内部 + 外部

内部 : `i`
外部 : `a`

## 一些文本对象

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
