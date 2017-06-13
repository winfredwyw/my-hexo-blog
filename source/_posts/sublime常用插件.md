---
title: sublime常用插件
date: 2016-07-25 09:09:29
tags:
---
## 1、Babel ##
### 作用 ###
支持ES6， React.js, jsx代码高亮，对 JavaScript, jQuery 也有很好的扩展
### 配置 ###
1. 打开.js, .jsx 后缀的文件;
2. 打开菜单view， Syntax -> Open all with current extension as... -> Babel -> JavaScript (Babel)，选择babel为默认   javascript 打开syntax

## 2、Emmet ##
### 作用 ###
emmet 作为前端开发必备插件之一非常方便快捷，默认情况下使用快捷键ctrl+e可以自动扩展成适应于react的className形式
### 配置 ###
1. 打开 preferences -> Key bindings - Users，把下面代码复制到[]内部;
```
{
  "keys": ["tab"], 
  "command": "expand_abbreviation_by_tab", 

  // put comma-separated syntax selectors for which 
  // you want to expandEmmet abbreviations into "operand" key 
  // instead of SCOPE_SELECTOR.
  // Examples: source.js, text.html - source
  "context": [
    {
      "operand": "source.js", 
      "operator": "equal", 
      "match_all": true, 
      "key": "selector"
    }, 
    // run only if there's no selected text
    {
      "match_all": true, 
      "key": "selection_empty"
    },

    // don't work if there are active tabstops
    {
      "operator": "equal", 
      "operand": false, 
      "match_all": true, 
      "key": "has_next_field"
    }, 

    // don't work if completion popup is visible and you
    // want to insert completion with Tab. If you want to
    // expand Emmet with Tab even if popup is visible -- 
    // remove this section
    {
      "operand": false, 
      "operator": "equal", 
      "match_all": true, 
      "key": "auto_complete_visible"
    }, 
    {
      "match_all": true, 
      "key": "is_abbreviation"
    }]}
```

## 3、JsFormat ##
### 作用 ###
jsformat 是 sublime 上 js 格式化比较好用的插件之一，通过修改它的e4x 属性可以使它支持 jsx。
### 配置 ###
1. 打开preferences -> Package Settings -> JsFormat -> Setting - Users,输入以下代码
```
{
  "e4x": true,
  // jsformat options
  "format_on_save": true,
}
```

## 4、Terminal ##
### 作用 ###
当你想要打开在当前文件所在的目录的终端，这个插件可以帮助你。不过，在默认情况下，它设置按 Ctrl / Cmd + Shift + T 键的快捷方式打开终端。不过这也是打开上次关闭的文件的快捷方式，你需要修改一个快捷键来兼容两个功能。

