---
layout: post
title: "測試！測試！ - 002"
date: 2012-04-25 10:51
comments: true
categories: Rails
tags: Rails
---

**1000 个小时学会 Rails 系列**

> The general idea behind unit testing is that you write a test method that makes certain assertions about your code, working against a test fixture. A bunch of these test methods are bundled up into a test suite and can be run any time the developer wants. The results of a run are gathered in a test result and displayed to the user through some UI.
-- Nathaniel Talbott

好了，Rails 真的很牛。Ruby 是如此优雅精妙，那么程序员真的性福美满了吗？那究竟要如何写出可维护的代码呢？拜读松本行弘的程序世界？不是！连读七遍 Programming Ruby 1.9？有可能！每天上 Ruby-china 学习？这就对了！好了那到底是什么？答案是写测试！

<!--more-->

为什么要写测试呢？恩，先谈谈两种程序员吧。一种是自负的程序员，他们觉得：“日出东方，唯我代码不坏”，这种思想其实很好，是社会进步的动力之一。这种人要嘛特别牛，要嘛特别。。。0010，但我们要看清一个事实，是人都会犯错。另一种程序员，怎么著都怕出错，在论坛四处发问，哪本书最好，哪个教程最猛，写程序战战兢兢，就跟相亲挑老婆，结果如墨菲先生预言：只要有可能出错，那就一定会出错。第一种程序员，根本不屑写测试，第二种程序员，拼命学写测试，学的连代码都不会写了。该怎么办？

还是写测试！在编码前先写测试，这有什么好处？预测程序的行为、确保程序如你想的那般工作、有写测试让你更有自信，更容易重构代码，理清你的思路，等等好处。那为什么大家都不写测试呢？呃。。。很多原因是老板太凶、日期太紧，但我相信测试可以救你于水火之中。而 Rails 也替你打点了许多的测试工具，让你不用在「编码->储存->刷新->编码->储存->刷新...」、要是一个个视图、一个个模型、一个个控制器都是如此手工测试，搞得你晚上八点还在公司，一出错又不知从何查起，真是一场永远不会醒的恶梦。测试可以使我们确保程序正常运作，将用户行为转为测试，让我们有一个开发的方向。未来出错时，可以改动现有的测试来适应新的情况，让你可以早日回家陪老婆孩子（家庭第一），正所谓，测试写得好，挣钱挣到老，测试写的巧，上班没烦恼。

月有阴晴圆缺，而生命会自己找到出口，就这样，有了[测试驱动开发][TDD]（Test-Driven Development, TDD）以及[行为驱动开发][BDD]（Behavior-Driven Development, BDD）。TDD 又有一个名字叫做 Red-Green-Refactor。先写好测试，运行，错误一堆（满江红），撰写可以通过测试的代码（绿油油），测试通过后再重构，确保代码仍然工作。这样子的好处是？一来先写测试可以先让你想想程序的思路，与下棋有异曲同功之妙，只不过下棋咱是在脑里演练；二来写测试可以确保你的程序正常工作，预期未来可能发生的错误。然而我们从小的教育不是这样，导致我们害怕犯错，以前可以考试先考差了，再让你重写一次考卷嘛？现在机会来了。写测试吧！

恩，至于这 BDD 与 TDD 精确的定义呢，危机、摆渡百科都有，谷歌百度一下吧，就不赘述了，用了就知道！BDD 是基于 TDD 所造出来的，旨在测试整个程序中，各个“正常工作代码”之间的互动。也就是说呢，TDD 搭配 BDD 使用。TDD 的工具我们将粗浅介绍 Test::Unit，BDD 我们将介绍的是 RSpec 搭配 海豚 (Capybara)，小黄瓜 (Cucumber)就别用了，太坑爹了，还是留著配炸酱面吧！

还是不怎么信么？那我再好好讲一次测试的好处，你想想，如果你要测试某个页面的表单，填了某个值会发生什么事，要是这个表单一共有九种变化，共有九种不同表单，九九八十一个变化，还不算你手滑按错的错误，这测起来真是想死的心都有了（爱惜生命！）。让计算机自动帮我们测试，比起手工测试好、省时又省心。另一个好处是，测试可以预防你犯傻。当你犯了一个再明显不过的错误时，测试可以替你找出来，替你的程序做一个健康检查，让你获得更多信息，由测试通知你，总比暴跳如雷的老板来得好。用户永远都有无止尽的好奇心，会在你想都想不到的地方，把东西弄坏！有了之前的测试，你可以轻松的改写之前的测试，来满足这个你未预期的情况，这又叫作[回归测试][RT] (Regression Test)

现在我们来看怎么用 Test::Unit 写测试吧！

### 撰写第一个测试

Ruby 的 `Test::Unit` 写了一堆的函式库，就在哪里，等著、盼著、寂寞地等你调用它们。接下来我来讲一个简单的 `Test::Unit` 例子。首先建立一个目录，叫作 `example` ，在这个目录里你创一个文件：`example_test.rb` 。记得把测试加上 `_test` 的字尾，这样子一看就知道这是一个测试文件。打开这个 `example_test.rb` ，敲入以下代码：

	require 'test/unit'

	class ExampleTest < Test::Unit::TestCase
	  def test_truth
	    assert true
	  end
	end

`Test::Unit` 测试呢，首先引入 Ruby 标准函式库的 `'test/unit'` 。这让你可以从 `Test::Unit::TestCase` 继承它所有的东西（要是可以 `require '李嘉诚'` 就好了，我也不用。。。）。那究竟继承了什么？继承了让你可以在类里面，将名字取为 `test_` 打头的方法来写测试的功能，`test_xxxx` 会被识别成是测试。

第一个测试写好了！！！！！！！（咆哮体），让我们来运行看看： 

`ruby example_test.rb` 

你会看到像是这样的输出：

	.

	Finished tests in 0.000866s, 1154.7344 tests/s, 1154.7344 assertions/s.

	1 tests, 1 assertions, 0 failures, 0 errors, 0 skips

那个奇怪的点是什么呢？这是 `Test::Unit` 告诉你一个测试成功通过的方式， `F` 代表不通过的测试, `E` 代表有错误的测试，那 `(.)(.)` 呢？哈哈开个玩笑，确保你有认真看。跟著点之后是一些统计数据，告诉你一个测试、一个断言 (assertion)、零个失败、零个错误、零个跳过。

在你的测试中你用了一个 `assert` 方法，你断言传入的参数为真。然而我们传入的是真（非 `nil` 与 `false` 亦为真），假如不知为何的这个方法失败了，会引起一个 exception 告诉你。 

如果你的方法名不是 `test_` 打头：

	test "truth" do
		assert true
	end

你再运行看看 (`ruby example_test.rb`)，会发现

	No tests were specified.
	1 tests, 1 assertions, 1 failures, 0 errors

这是因为 `Test::Unit` 调用了缺省的 `default_test` 缘故，若你使用的是 1.9.3+ 的 Ruby 只会显示没有测试。

所以记得把测试方法名用 `test_` 开头！

接下来让我们考虑一个更复杂的方法，建立一个 `love_test.rb` ：

	require 'test/unit'
	class LoveTest < Test::Unit::TestCase
	  def test_saved
	    assert Love.saved?
	  end
	end

当然了，你想确保你的愛情有保存，但是当你运行时 `ruby love_test.rb` ，哎呀：

	NameError: uninitialized constant LoveTest::Love

哪知道你根本还没有愛情，让我们来定义爱情：

	class Love

	end

那这个愛情要放在测试之前呢，还是测试之后呢？在 `Test::Unit` 里是都可以，在 Ruby 里面东西都是得先定义才能使用，但是 `Test::Unit` 会先把所有的代码求值，再来运行测试，所以现在 `love_test.rb` ：

	require 'test/unit'

	class Love

	end

	class LoveTest < Test::Unit::TestCase
	  def test_saved
	    assert Love.saved?
	  end
	end

接下来再运行看看 `ruby love_test.rb` ：

	NoMethodError: undefined method `saved?' for Love:Class

错误信息明确的告诉我们，愛情是不能保质的，看来 Ruby 也挺懂人情事理的，但我們可以自己定義一個保存的方法：

	class Love
		def self.saved?
		  true
		end
	end

接著运行你会如预期的发现测试通过，但是有一天，就是風雨交加的那天，不知为何某女把你的测试改成 `false` ：

	F

	Finished tests in 0.001137s, 879.5075 tests/s, 879.5075 assertions/s.

	  1) Failure:
	test_saved(LoveTest) [love_test.rb:14]:
	Failed assertion, no message given.

失败，最惨的是 `no message given` 。。。

居然什么信息也不给，唉，其实这是 `Test::Unit` 一贯回报测试失败的方式，

然而某女突然觉得过意不去，又回头给你加上一个更清楚的信息：

  	assert Love.saved?, "咱俩不合适！ ..." 

现在你再运行测试，你会得到一个清楚的错误信息

	  1) Failure:
	test_saved(LoveTest) [love_test.rb:16]:
	咱俩不合适！

嗯，你懂得，我的朋友。。。。。他说风雨中这点痛算什么，擦乾泪不要问，至少我们还有梦！

这就是使用 `Test::Unit` 非非非非非非常基本的 TDD 了， `Test::Unit` 是 Rails 缺省的测试框架，在我们漫长的学习 Rails 的旅途中，你将会常常看到它，并且克制不住的或是被逼迫的使用它。

记得哦，爱情是没有保质期的，亲。

距离学会 Rails 还有 965 个小时。。。

待续。。。

### 延伸阅读

[CodeSchool: Rails Testing for Zombies slides](http://courseware.codeschool.com.s3.amazonaws.com/rails_testing.pdf)

[A Guide to Testing Rails Applications](http://guides.rubyonrails.org/testing.html)

[测试 Testing](http://ihower.tw/rails3/testing.html)

[Ruby Koans](http://rubykoans.com/)

[Ruby-china上关于测试的帖子](http://ruby-china.org/search?q=Test%3A%3AUnit)

[Ruby Test::Unit 函式库](http://ruby-doc.org/stdlib-1.9.3/libdoc/test/unit/rdoc/Test/Unit.html)

[为什么女朋友不要我了](http://www.google.com.hk/webhp?hl=zh-CN&sourceid=cnhp#hl=zh-CN&safe=strict&site=webhp&source=hp&q=%E4%B8%BA%E4%BB%80%E4%B9%88%E5%A5%B3%E6%9C%8B%E5%8F%8B%E4%B8%8D%E8%A6%81%E6%88%91%E4%BA%86&oq=%E4%B8%BA%E4%BB%80%E4%B9%88%E5%A5%B3%E6%9C%8B%E5%8F%8B%E4%B8%8D%E8%A6%81%E6%88%91%E4%BA%86&aq=f&aqi=&aql=&gs_nf=1&gs_l=hp.3...1405.6419.0.6789.34.32.1.0.0.0.105.1818.30j1.31.0.uZEfYhm1ZUM&bav=on.2,or.r_gc.r_pw.,cf.osb&fp=4de69b13c14b576b)


[1000-000]: http://ruby-china.org/topics/2799
[1000-001]: http://ruby-china.org/topics/2814
[RT]: http://zh.wikipedia.org/wiki/%E5%9B%9E%E5%BD%92%E6%B5%8B%E8%AF%95
[TDD]: http://zh.wikipedia.org/wiki/%E6%B5%8B%E8%AF%95%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91
[BDD]: http://zh.wikipedia.org/wiki/%E8%A1%8C%E4%B8%BA%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91

