<!--
 * @Author: hy
 * @Date: 2022-06-13 23:44:41
 * @LastEditors: hy
 * @Description:
 * @LastEditTime: 2022-06-13 23:44:43
 * @FilePath: /til/vscode/vsocde_vim_setting.md
 * Copyright 2022 hy, All Rights Reserved.
 * 仅供学习使用~
-->

# vscode vim setting

```json

  // vim
  // base
  "vim.incsearch": true,
  "vim.useSystemClipboard": true,
  "vim.useCtrlKeys": true,
  "vim.hlsearch": true,
  "vim.leader": "<space>",
  // plugin
  "vim.easymotion": true,
  "vim.sneak": true,
  //
  "vim.handleKeys": {
    "C-c": false
    // "<C-a>": false,
    // "<C-f>": false
  },
  // alias
  "vim.insertModeKeyBindings": [
    {
      "before": ["j", "j"],
      "after": ["<Esc>"]
    }
  ],
  "vim.visualModeKeyBindings": [
    // 行内移动
    {
      "before": ["H"],
      "after": ["^"] // 快速移动到行首
    },
    {
      "before": ["L"],
      "after": ["g", "_"] // 快速移动到行尾
    },
    // 文件内移动
    {
      "before": ["J"],
      "after": ["5", "j"] // 快速向下移动5行
    },
    {
      "before": ["K"],
      "after": ["5", "k"] // 快速向上移动5行
    },
    //
    {
      "before": ["j", "j"],
      "after": ["<Esc>"]
    }
  ],
  "vim.normalModeKeyBindings": [
    // 行内移动
    {
      "before": ["H"],
      "after": ["^"] // 快速移动到行首
    },
    {
      "before": ["L"],
      "after": ["g", "_"] // 快速移动到行尾
    },
    // 文件内移动
    {
      "before": ["J"],
      "after": ["5", "j"] // 快速向下移动5行
    },
    {
      "before": ["K"],
      "after": ["5", "k"] // 快速向上移动5行
    }
  ],
  // normal 非递归模式下
  "vim.normalModeKeyBindingsNonRecursive": [
    // 把普通的f 替换成 sneak 模式下的s
    {
      "before": ["f"],
      "after": ["s"]
    },
    {
      "before": ["F"],
      "after": ["S"]
    },
    // 把s替换成 删除
    {
      "before": ["s"],
      "after": ["c", "l"]
    },
    {
      "before": ["S"],
      "after": ["^", "C"]
    }
  ],
  "vim.visualModeKeyBindingsNonRecursive": [
    {
      "before": ["f"],
      "after": ["s"]
    }
    // {
    //   "before": ["F"],
    //   "after": ["S"]
    // }
  ],
  "vim.operatorPendingModeKeyBindings": [
    // 行内移动
    {
      "before": ["H"],
      "after": ["^"] // 快速移动到行首
    },
    {
      "before": ["L"],
      "after": ["g", "_"] // 快速移动到行尾
    }
  ],
  "vim.operatorPendingModeKeyBindingsNonRecursive": [
    {
      "before": ["f"],
      "after": ["z"]
    },
    {
      "before": ["F"],
      "after": ["Z"]
    }
  ]

```
