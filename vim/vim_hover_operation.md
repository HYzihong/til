<!--
 * @Author: hy
 * @Date: 2022-06-18 17:02:41
 * @LastEditors: hy
 * @Description:
 * @LastEditTime: 2022-06-18 17:33:10
 * @FilePath: /til/vim/# vim_hover_operation.md
 * Copyright 2022 hy, All Rights Reserved.
 * 仅供学习使用~
-->

# 悬浮操作

> `gh`
> 退出悬浮模式，使用 `esc` 和自定义快捷键( `C+[` or `jj` )

类似于鼠标悬浮上的操作

文件导出的方法上使用`gh` 命令可以显示方法的详情

在第三方包上显示包的详情

eg:

```javascript
import { defineStore } from "pinia";

//  在 defineStore 上使用 `gh` 显示方法的详情 如下

/*

 (alias) function defineStore<Id extends string, S extends StateTree = {}, G extends _GettersTree<S> = {}, A = {}>(id: Id, options: Omit<DefineStoreOptions<Id, S, G, A>, 'id'>): StoreDefinition<Id, S, G, A> (+2 overloads)
import defineStore
Creates a useStore function that retrieves the store instance
@param id — id of the store (must be unique)
@param options — options to define the store

 */

//  在 pinia 上使用 `gh` 显示方法的详情 如下

/*
 module "/Users/hy/code/Taro/clock-in/node_modules/pinia/dist/pinia"
 */
```
