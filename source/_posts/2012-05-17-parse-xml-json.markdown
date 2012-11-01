---
layout: post
title: "Python 简易解析 XML JSON"
date: 2012-05-17 22:06
comments: true
categories: xml json
tags: xml json
---

### XML

#### 使用轻量快速的 minidom 函式库

引用 minidom:

	from xml.dom import minidom

> DOM -- Document Object Model

minidom 有一个 parseString 函数可以解析 XML 字串。

<!--more-->

解析一个随意取名的 XML 字串，存入 x：

	x = minidom.parseString("<foo>Lorem ipsum<children><item>1</item><item>2</item><item>3</item></children></foo>")

x 现在是一个 xml.dom.minidom.Document instance 实例。

**注意** XML 不像 HTML，严格要求每个 open 标签要有一个相应的 close 标签！

看看 x 有什么可以调用的属性、方法：

	dir(x)

	['ATTRIBUTE_NODE', 'CDATA_SECTION_NODE', 'COMMENT_NODE', 'DOCUMENT_FRAGMENT_NODE', 'DOCUMENT_NODE', 'DOCUMENT_TYPE_NODE', 'ELEMENT_NODE', 'ENTITY_NODE', 'ENTITY_REFERENCE_NODE', 'NOTATION_NODE', 'PROCESSING_INSTRUCTION_NODE', 'TEXT_NODE', '__doc__', '__init__', '__module__', '__nonzero__', '_call_user_data_handler', '_child_node_types' ... 'standalone', 'strictErrorChecking', 'toprettyxml', 'toxml', 'unlink', 'version', 'writexml']

转回 xml:

	x.toprettyxml()

印出来看看：

	print x.toprettyxml()

输出：

	<foo>
		Lorem ipsum
		<children>
			<item>
				1
			</item>
			<item>
				2
			</item>
			<item>
				3
			</item>
		</children>
	</foo>

取得第二个 item 标签内的值 2：

	x.getElementsByTagName('item')[1].childNodes[0].nodeValue

你可以看看 dir 里面有什么函数可以用，在 python 的直译器里面玩玩看。

### RSS

比如说想要知道 http://www.nytimes.com/services/xml/rss/nyt/Science.xml 有几个 item：

	from xml.dom import minidom

	import urllib2

	contents = urllib2.urlopen("http://www.nytimes.com/services/xml/rss/nyt/Science.xml").read()

	d = minidom.parseString(contents)

	len(d.getElementsByTagName("item")) # => 38 on 2012.05.17

### JSON

Javascript Object Notation

在 Python 用 dictionary 混 List 的形式储存 `{ foo: [{"a": 1}, ... {"c": 3}] }`

使用 JSON 库：

	import json

假设今天我们有一个 json 格式的字串 j，具有两个键 `mon` 与 `numbers`：

	j = '{"mon": 1, "numbers": [1,2,9.9]}'

载入这个 json ，存到 d 里：

	d = json.loads(j)

载入后我们得到一个 python 字典（无序）：

	{u'mon': 1, u'numbers': [1, 2, 9.9]}

取出 `mon` 的值：

	d['mon'] # => 1
	d['numbers'][2] # => 9.9

你也可以 `eval` 这个 json 格式的字串：

	eval(j)
	# => {'mon': 1, 'numbers': [1, 2, 9.9]}

**永远别用 eval 来解析 json** 。

Q: 加总 www.reddit.com 帖子的 up votes。

A:

```python
r = urllib2.urlopen("http://www.reddit.com/.json")
j = json.loads(r)

j.keys() # => [u'kind', u'data']
j['data'].keys() # => [u'modhash', u'children', u'after', u'before']
j['data']['children'][0].keys() # => [u'kind', u'data']
j['data']['children'][0]['data'].keys() # => [..., u'ups']
j['data']['children'][0]['data']['ups'] # => 7902

sum(c['data']['ups'] for c in j['data']['children']) # => 84500
```

DONE.
