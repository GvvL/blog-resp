---
title: vscode 配置记录
date: 2016-07-17 15:00:16
categories: vscode
tags:
    - vscode
---
## 快捷键
``` bash
// 将键绑定放入此文件中以覆盖默认值
[
    { "key": "shift+u",                "command": "cursorPageUp",
                                     "when": "editorTextFocus" },
    { "key": "shift+i",              "command": "cursorPageDown",
                                     "when": "editorTextFocus" },
    { "key": "alt+l",            "command": "cursorWordEndRight",
                                     "when": "editorTextFocus" },
    { "key": "alt+h",            "command": "cursorWordEndLeft",
                                     "when": "editorTextFocus" },
    { "key": "alt+k",                 "command": "cursorRight",
                                     "when": "editorTextFocus" },
    { "key": "alt+j",                  "command": "cursorLeft",
                                     "when": "editorTextFocus" },
    { "key": "end",                   "command": "cursorEnd",
                                     "when": "editorTextFocus" },
    { "key": "alt+u",                    "command": "cursorUp",
                                     "when": "editorTextFocus" },
    { "key": "alt+i",                  "command": "cursorDown",
                                     "when": "editorTextFocus" },
   { "key": "ctrl+d",          "command": "editor.action.deleteLines",
                                     "when": "editorTextFocus" },
    { "key": "alt+d",                "command": "editor.action.addSelectionToNextFindMatch",
                                     "when": "editorFocus" },
    { "key": "alt+n",            "command": "editor.action.triggerSuggest",
                                     "when": "editorTextFocus" },
    { "key": "alt+o",             "command": "scrollLineDown",
                                     "when": "editorTextFocus" },
    { "key": "alt+y",               "command": "scrollLineUp",
                                     "when": "editorTextFocus" },
    { "key": "alt+;",               "command": "deleteWordEndRight",
                                     "when": "editorTextFocus" }
]

```

