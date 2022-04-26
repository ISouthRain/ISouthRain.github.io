---
layout:     post
title:      "Org-mode 使用 Org-protocol-capture-html 网页收集(Org-protocol 使用)"
subtitle:   "Org-protocol 和 Org-protocol-cature-html 插件的使用"
date:       2022-01-12
author:     "ISouthRain"
catalog: true
header-img: img/post-bg-hacker.jpg
tags:
  - Blog
  - Emacs
---

## 前言
**Notion** 和 **Obsidian** 都有收集网页的功能, Org-mode 自然也有, Org-mode 是调用 Org-protocol 协议使用的, 而插件 `Org-protocol-capture-html` 是其中能使 `Org-protocol` 收集的网页更加美观和可视化

因为很多人都不会都不理解 `Org-protocol` 和怎么去使用, 以及`Org-protocol-capture-html`, 说得只是怎么用这个插件, 却没有说怎么配置, 所以才有了本教程.

## 相关链接
- [Org-protocol-capture-html 官网](https://github.com/alphapapa/org-protocol-capture-html)
- [Org-protocol 协议官网](https://orgmode.org/manual/Protocols.html)

### 效果如下
`请自己下载观看，大约7mb`👉  [效果视频](https://raw.githubusercontent.com/ISouthRain/ISouthRain.github.io/main/_posts/Attachment/2022-01-12-Org-protocol-capture-html/2022-01-22-14-24-59.mkv)   
`效果动图`👉 [效果动图](https://raw.githubusercontent.com/ISouthRain/ISouthRain.github.io/main/_posts/Attachment/2022-01-12-Org-protocol-capture-html/2022-01-22-14-24-59.gif)  
![效果动图](https://raw.githubusercontent.com/ISouthRain/ISouthRain.github.io/main/_posts/Attachment/2022-01-12-Org-protocol-capture-html/2022-01-22-14-24-59.gif)

# 安装 Org-protocol-capture-html

这个插件是不需要配置, 直接安装此插件就可以调用  

`请自己按装此插件`

- 使用 use-package 安装
- 手动安装

## 配置 Org-protocol-capture-html
此插件是调用 `org-capture` 功能, 请自觉检查如下配置

```Elisp
(server-start)
(require 'org-protocol)

(use-package s) ;;依赖

;; 安装 org-protocol-capture-html 
;; 如果跟我的不同, 请将下面两行删除
(add-to-list 'load-path "~/.emacs.d/plugins/org-protocol-capture-html/") ;;
(require 'org-protocol-capture-html)

(setq org-capture-templates
      '(
	 ;;Org-protocol网页收集, 按键 w 调用
	 ("w" "网页收集" entry (file "~/Org/网页收集.org")
	 "* [[%:link][%:description]] \n %U \n %:initial \n")
	))
```

## 系统安装 org-protocol
`如果下面的方法无法安装, 请见官网 👇`
- [官网安装 org-protocol 教程](https://orgmode.org/worg/org-contrib/org-protocol.html)

### Windows 用户👇
- 桌面新建 `org-protocol.reg` 文件, 使用 记事本 软件打开 , 并将以下👇代码放进去并保存, 然后运行安装并给权限
- `请把下面的 emacsclientw.exe 路径换成你自己的路径`

```
REGEDIT4

[HKEY_CLASSES_ROOT\org-protocol]
@="URL:Org Protocol"
"URL Protocol"=""
[HKEY_CLASSES_ROOT\org-protocol\shell]
[HKEY_CLASSES_ROOT\org-protocol\shell\open]
[HKEY_CLASSES_ROOT\org-protocol\shell\open\command]
@="\"C:\\Programme\\Emacs\\emacs\\bin\\emacsclientw.exe\" \"%1\""
```

### Linux 用户请见 👉 [Linux 使用 org-protocl](https://kisaragi-hiu.com/org-protocol-linux)

## 根据自己使用的浏览器添加书签

`关于 org-protocol-capture-html 对不同的 浏览书签 见` 
- [Org-protocol-capture-html 官网](https://github.com/alphapapa/org-protocol-capture-html)

### 例如 Chrome
#### 在 Chrome 新建 书签
1. 书签名称随便取
2. 书签地址如下👇


```javascript
javascript:location.href = 'org-protocol:///capture-html?template=w&url=' + encodeURIComponent(location.href) + '&title=' + encodeURIComponent(document.title || "[untitled page]") + '&body=' + encodeURIComponent(function () {var html = ""; if (typeof window.getSelection != "undefined") {var sel = window.getSelection(); if (sel.rangeCount) {var container = document.createElement("div"); for (var i = 0, len = sel.rangeCount; i < len; ++i) {container.appendChild(sel.getRangeAt(i).cloneContents());} html = container.innerHTML;}} else if (typeof document.selection != "undefined") {if (document.selection.type == "Text") {html = document.selection.createRange().htmlText;}} var relToAbs = function (href) {var a = document.createElement("a"); a.href = href; var abs = a.protocol + "//" + a.host + a.pathname + a.search + a.hash; a.remove(); return abs;}; var elementTypes = [['a', 'href'], ['img', 'src']]; var div = document.createElement('div'); div.innerHTML = html; elementTypes.map(function(elementType) {var elements = div.getElementsByTagName(elementType[0]); for (var i = 0; i < elements.length; i++) {elements[i].setAttribute(elementType[1], relToAbs(elements[i].getAttribute(elementType[1])));}}); return div.innerHTML;}());

javascript:location.href = 'org-protocol:///capture-eww-readable?template=w&url=' + encodeURIComponent(location.href) + '&title=' + encodeURIComponent(document.title || "[untitled page]");
```

### Firefox 如下
#### 在 Firefox 新建 书签
1. 书签名称随便取
2. 书签地址如下👇


```javascript
javascript:location.href = 'org-protocol://capture-html?template=w&url=' + encodeURIComponent(location.href) + '&title=' + encodeURIComponent(document.title || "[untitled page]") + '&body=' + encodeURIComponent(function () {var html = ""; if (typeof document.getSelection != "undefined") {var sel = document.getSelection(); if (sel.rangeCount) {var container = document.createElement("div"); for (var i = 0, len = sel.rangeCount; i < len; ++i) {container.appendChild(sel.getRangeAt(i).cloneContents());} html = container.innerHTML;}} else if (typeof document.selection != "undefined") {if (document.selection.type == "Text") {html = document.selection.createRange().htmlText;}} var relToAbs = function (href) {var a = document.createElement("a"); a.href = href; var abs = a.protocol + "//" + a.host + a.pathname + a.search + a.hash; a.remove(); return abs;}; var elementTypes = [['a', 'href'], ['img', 'src']]; var div = document.createElement('div'); div.innerHTML = html; elementTypes.map(function(elementType) {var elements = div.getElementsByTagName(elementType[0]); for (var i = 0; i < elements.length; i++) {elements[i].setAttribute(elementType[1], relToAbs(elements[i].getAttribute(elementType[1])));}}); return div.innerHTML;}());
```

## 享受使用 👇
### 使用之前
`请把你的 Chrome 或者 Firefox 的 书签 始终可见(比如在你浏览网页选中文字时可以点击你的书签)`

### 开始使用
1. 打开 Emacs
2. 使用浏览器浏览网页
3. 在网页 `选择你想收集的文本`
4. 点击你刚才新建的书签, 点击确定授权之类的
5. 回到 Emacs 你会看到你已经收集到的 Capture
6. 自己记得保存
7. 你收集到的会 保存到 `~/Org/网页收集.org` 文件中

## 如果你有更多的需求, 请自己学习, 因为网上并没有详细的教程使用 org-protocol 所以才有了本教程  
`祝你使用愉快🤓⚡👉♥️🌹`
