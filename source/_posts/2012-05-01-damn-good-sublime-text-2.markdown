---
layout: post
title: "好用 好快 好強大的 Sublime Text 2"
date: 2012-05-01 20:04
comments: true
categories: Tool
tags: Tool
---

Sublime Text2 目前免費試用中，之後是 59 美金。

支援 Windows, Linux, MacOSX, 英文、CJK 支援良好。

快、狠、準、趕緊用吧！大哥。。。

<!-- More -->

## [安装 Sublime Text 2](http://www.sublimetext.com/dev)

点击链接、下载并安装。

针对 Rails 开发者的通用調校:

可參考此 >> [Repository][rails-setup] << from Michael Hartl

Sublime Text 2 透过 [Package Controll][pc] 安装插件是再容易不过了，省时又省心。

## 小技巧

### 自定義 Snippet

Tools -> New Snippet 可以自定義 Snippet，建議自己設，別人設的記不住。

Toggler 觸發熱鍵，Scope 是 Snippet 有效範圍，語言記得打全名: `source.ruby`。

`$1`, `$2`, `$3` ... 第一、二、三 tab 預設到達位置，可有預設值。

`Hello, ${1:this} is a ${2:snippet}.`

一開始包住 this，輸入、按 tab 跳到 snippet 的位置，試試便知。

### 設置自定義熱鍵

Sublime Text 2 → Preferences → KeyBindings - User

## Sublime 主題

自帶 **10+** 種 Color Themes

Sublime Text 2 > Preference > Color Themes

安裝方法各 repo 皆有說明。

[Soda][soda] 一個比較多人推薦的主題

[這裡有更多的 Themes](http://wiki.macromates.com/Themes/UserSubmittedThemes)

## 如何安装新的插件？

安裝方法 `Shift+Command+P` 叫出命令中心 -> Package Install -> 搜索關鍵字安裝即可。

## 一些推荐的插件

这些插件如何使用，請到每個 Github repo 頁面看說明及熱鍵，斟酌使用，不一定全都要裝。

### 通用

* [Gist][gst] 可以在 Sublime 裡面新增、抓取 Gist。

* [Advanced New File][anf] Command+Alt+N 可同時新增 File 及 Path
* [TrailingSpaces][ts] 抓出尾隨的空白。
* [Nettuts+ Fetch][nf] 自定抓取檔案。
* [Sublime Codeintel][scl] 跳到定義、自動補全、更多資訊。
* [WordCount][wc] 計算字數。
* [BracketHighlighter][bhl] 大括號、中括號、括號家族高亮匹配
* [GoToTab][goto] Command 1-N 跳到 1-N tab，似乎已經內建，沒有此功能再裝。

### 版本管理

* [Git][gt] Sublime + Git。
* [Hg][hg] Sublime + Hg。
* [SVN][svn] Sublime + SVN。

### 除错工具

* [Sublime Linter][slint] 可以把可能有错的代码高亮起来，支援各种语言。

### HTML CSS 前端

* [Zen Coding][zc] HTML 快速建型的高速魔法
* [LESS][less] LESS 語法支持、高亮、Snippet
* [Sass][sass] Sass 語法支持、高亮、Snippet
* [Scss][scss] Scss 語法支持、高亮、Snippet
* [Haml][haml] Haml 語法支持、高亮、Snippet
* [Prefixr][pfx] CSS Prefix，輸入 boder-radius 可回傳各家瀏覽器之前綴。

### Ruby & Rails

* [ERB and Toggle Comments][etc] ERB 語法支援
* [Beautify Ruby][BR] 自動對齊 Ruby
* [Ruby Test][RT] 直接在 Sublime Console 跑測試
* [RSpec][rspec] Snippet 及語法高亮



## 熱鍵列表 （待補全）

<table>
<tr>
<th>熱鍵</th>
<th>功能</th>
<tr>
<td>Command+K+B</td>
<td>側邊欄顯示/隱藏</td>
</tr>
</tr>
<td>Command+P or Command+T</td>
<td>極速隨意跳轉</td>
</tr>
<tr>
<td>Shift+Command+P</td>
<td>命令中心</td>
</tr>
<tr>
<td>Command+數字</td>
<td>切換至第 N 個 Tab</td>
</tr>
<tr>
<td>Control+Command+P</td>
<td>切換 Project</td>
</tr>
<tr>
<td>Command+]</td>
<td>縮排</td>
</tr>
<tr>
<td>Command+[</td>
<td>復原縮排</td>
</tr>
<tr>
<td>Control+Command+上</td>
<td>單行上移（或多行向上）</td>
</tr>
<tr>
<td>Control+Command+下</td>
<td>單行下移（或多行向下）</td>
</tr>
<tr>
<td>Shift+Command+F</td>
<td>搜索整個Project</td>
</tr>
<tr>
<td>Control+Shift+K</td>
<td>刪除此行或多行</td>
</tr>
<tr>
<td>Control+Shift+W</td>
<td>把選取內容用標籤包住</td>
</tr>
<tr>
<td>Option+Command+.</td>
<td>補上 Closing Tag</td>
</tr>
<tr>
<td>Shift+Command+A</td>
<td>標籤內內容全選</td>
</tr>
</table>



### 無干擾模式

Control+Shift+Command+F

### 叫出 Console

ctrl + `

## 更多教學文章

[Lucifr 的 Blog](https://www.google.com/search?q=site%3Alucifr.com&q=Sublime)

[9 reasons you should use sublime text 2](http://1p1e1.tumblr.com/post/14262857223/9-reasons-you-must-install-sublime-text-2-code-like-a)

[slint]:https://github.com/Kronuz/SublimeLinter
[bhl]:https://github.com/facelessuser/BracketHighlighter
[zc]: https://bitbucket.org/sublimator/sublime-2-zencoding
[BR]: https://github.com/CraigWilliams/BeautifyRuby
[RT]: https://github.com/maltize/sublime-text-2-ruby-tests
[rspec]: https://github.com/rspec/rspec-tmbundle
[less]:https://github.com/danro/LESS-sublime
[scss]: http://sass-lang.com/
[sass]: https://github.com/nathos/sass-textmate-bundle
[haml]: https://github.com/handcrafted/handcrafted-haml-textmate-bundle
[nf]:http://net.tutsplus.com/articles/news/introducing-nettuts-fetch/
[anf]:https://github.com/xobb1t/Sublime-AdvancedNewFile
[goto]: https://github.com/SublimeText/GotoTab
[wc]: https://github.com/SublimeText/WordCount
[ts]: https://github.com/SublimeText/TrailingSpaces
[gst]: https://github.com/condemil/Gist
[etc]: https://github.com/eddorre/SublimeERB
[gt]: https://github.com/kemayo/sublime-text-2-git/
[hg]: https://github.com/SublimeText/SublimeHg
[svn]:http://wbond.net/sublime_packages/svn
[rails-setup]: https://github.com/mhartl/rails_tutorial_sublime_text
[pc]:http://wbond.net/sublime_packages/package_control
[scl]:https://github.com/Kronuz/SublimeCodeIntel
[soda]:https://github.com/buymeasoda/soda-theme/
[pfx]: http://prefixr.com/
