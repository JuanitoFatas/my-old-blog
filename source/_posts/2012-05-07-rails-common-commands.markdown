---
layout: post
title: "Rails 3.2 命令及小技巧"
date: 2012-05-07 12:18
comments: true
categories: Rails
tags: Rails
published: false
---

列出一些常见的基本命令，注意有分**大小写** ，还有一些网络搜刮来的小技巧。

## Rails

<table>
<tr>
<th>命令</th>
<th>用途</th>
</tr>
<td>rails new app-name</td>
<td>建立一个新项目叫做 app-name</td>
</tr>
<tr>
<td>rails dbconsole</td>
<td>运行数据库，缩写 rails db</td>
</tr>
<tr>
<td>rails server</td>
<td>运行服务器，缩写：rails s</td>
</tr>
<tr>
<td>rails generate</td>
<td>产生代码，缩写：rails g</td>
</tr>
<tr>
<td>rails destroy</td>
<td>取消产生代码，缩写 rails d</td>
</tr>
</table>

### 使用非缺省的服务器 (WEBrick)

	rails server thin

[Thin][thin] 是一种服务器，效能比 WEBrick 好。




## Rake

Ruby 版的 `make` 命令。预设不带选项运行 `rake` 会运行所有测试。

<table>
<tr>
<th>命令</th>
<th>用途</th>
</tr>
<td>rake -T</td>
<td>列出可用的任务(task)</td>
</tr>
<tr>
<td>rake db:migrate</td>
<td>Migrate db/migrate 目录下的文件</td>
</tr>
<tr>
<tr>
<td>rake db:test:prepare</td>
<td>准备测试用的数据库</td>
</tr>
<td>rake db:migrate status</td>
<td>查看数据库的状态</td>
</tr>
<tr>
<td>rake db:reset</td>
<td>重置数据库</td>
</tr>




</table>

### Rake Annotation 小技巧

格式: `# KEYWORDS: `

注解井号、空白、关键字、冒号、空白。

关键字有：

使用 `TODO` 来标记之后应被加入的未实现功能或特色。

使用 `FIXME` 来标记一个需要修复的代码。

使用 `OPTIMIZE` 来标记可能影响效能的缓慢或效率低落的代码。

使用 `HACK` 来标记代码异味，其中包含了可疑的编码实践以及应该需要重构。

使用 `REVIEW` 来标记任何需要审视及确认正常动作的地方。

比如说在 `index.html.view` 文件：

	<%# OPTIMIZE: 记得实现分页 %>
	<%= render Post.all %>

这样子运行 `rake notes` 时，会出现以下相似的结果

	app/views/posts/index.html.erb
		* [ 1] [OPTIMIZE] Paginate this listing.

也可以单独查找 `TODO` 这个关键字：

	rake notes:todo

自定义关键字：

	rake notes:custom ANNOTATION=RAIN-CHECK

这样子我的代码当中有含的内容，运行上条命令时会显示出来：

	<% # RAIN-CHECK: ...... %>

## Rails Console

### 沙盒运行，不怕玩坏：

	rails console --sandbox

任何的改动在离开 console 时会 rollback。

### 在 Console 里调用 helper 内的方法：

	$ rails c
	>> helper.time_ago_in_words(100.days.ago)
	=> 3 months



[thin]: http://code.macournoyer.com/thin/


