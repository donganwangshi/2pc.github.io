---
layout: post
category : IDE
tagline: "Supporting tagline"
tags : [atom]
---
{% include JB/setup %}

# 配置

0. 在.atom目录下设置config.cson文件

```
"*":
  "exception-reporting":
    userId: "db6fc426-e8b2-de72-0100-ab3382303fb9"
  welcome:
    showOnStartup: false
  core:
    autoHideMenuBar: true
  editor:
    invisibles: {}
    fontFamily: "DejaVu Sans Mono,文泉驿正黑,文泉驿等宽微米黑,WenQuanYi Micro Hei Mono"


```

1. 在.atom目录下添加styles.less文件

```
.tree-view {
   font-size: 13px
 }
 // style the background and foreground colors on the atom-text-editor-element
 // itself
 atom-text-editor {
   font-family:DejaVu Sans Mono,文泉驿正黑,文泉驿等宽微米黑,WenQuanYi Micro Hei Mono;
 }
 // To style other content in the text editor's shadow DOM, use the ::shadow
 // expression
 atom-text-editor::shadow .cursor {
   font-family:DejaVu Sans Mono,文泉驿正黑,文泉驿等宽微米黑,WenQuanYi Micro Hei Mono;
 }
 html, body, .tree-view, .tab-bar .tab,.bottom{
   font-family:DejaVu Sans Mono,文泉驿正黑,文泉驿等宽微米黑,WenQuanYi Micro Hei Mono;
 }
 .terminal {
   font-size:12px;
   font-family: DejaVu Sans Mono,文泉驿正黑,文泉驿等宽微米黑,WenQuanYi Micro Hei Mono;
 }
 .markdown-preview {
     font-family: DejaVu Sans Mono,文泉驿正黑,文泉驿等宽微米黑,WenQuanYi Micro Hei Mono;
 }
 .code{
   font-family: DejaVu Sans Mono,文泉驿正黑,文泉驿等宽微米黑,WenQuanYi Micro Hei Mono;
 }

```
