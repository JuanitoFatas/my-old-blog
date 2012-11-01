---
layout: post
title: "Rails 3.2.3 使用 Spork + Guard + RSpec + Capybara"
date: 2012-04-30 13:46
comments: true
categories: Rails
tags: Rails
---

## 比较匆忙的同学请看

0) `rails new appname --skip-test-unit --skip-bundle`

1) 复制这个 Gemfile([OSX][MacOSX] / [Linux][Linux] / [Windows][Windows])，替换掉项目下的 Gemfile。

安装需要的 Gems，你有两个选择：

2-a) `bundle install` ，之后使用 `bundle exec xxx`  
2-b) `bundle install --binstubs`  ，之后使用 `bin/xxx`

3) `rails g rspec:install`

4) 运行 `bin/guard init rspec && bin/guard init spork`  
5) 复制这个 [Guardfile][gcomplete]，覆盖掉项目下的 Guardfile。  
6) 添加 `--drb` 至项目的根目录下的 `.rspec`。 
7) 复制这个 [spec/spec_helper.rb](https://gist.github.com/2555618)，覆盖 `spec/spec_helper.rb`  

8-a) `bundle exec spork --bootstrap`  
8-b) `bin/sprok --bootstrap`  

9-a) `bundle exec guard`  
9-b) `bin/guard`  

<!--more-->

## 有10分钟的同学请看

### 为什么使用 [Guard][guard]？

1. 要切回终端机敲 rspec 命令  
2. 启动速度太慢(使用 Spork 来加速)

Guard 人如其名，自动侦测改动并运行测试。

#### 配置 Guard

Gemfile:

在 `:development group` 加入：  

	gem 'guard-rspec', '0.5.5'

在 `:test group` 加入一些相依的 Gems，OSX 可能还需要安装 [growl-notify](http://growl.info/downloads#generaldownloads)：

**MacOSX**

	gem 'rb-fsevent', '0.4.3.1', :require => false
	gem 'growl', '1.0.3'

**Linux**

	gem 'rb-inotify', '0.8.8'
	gem 'libnotify', '0.5.9'

**Windows**

	gem 'rb-fchange', '0.0.5'
	gem 'rb-notifu', '0.0.4'
	gem 'win32console', '1.3.0'


范例 Gemfile，放在 Gist:

[MacOSX](https://gist.github.com/2555278)  
[Linux](https://gist.github.com/2555344)  
[Windows](https://gist.github.com/2555343)  

Gemfile 配置好运行 `bundle install` ，初始化 Guard：

	bundle exec guard init rspec

或是运行 `bundle install --binstubs`，初始化 Guard：

	bin/guard init rspec

会产生一个 Guardfile，最上方加入此行：

	require 'active_support/core_ext'

并改动此行 `guard 'rspec', :version => 2 do` ：

	guard 'rspec', :version => 2, :all_after_pass => false do

确保 Guard 不再一个失败测试通过后继续运行（加快**红绿重构**周期）

再添加：

	guard 'rspec', :version => 2, :all_after_pass => false do
		.
		.
		.
		watch(%r{^app/controllers/(.+)_(controller)\.rb$})  do |m|
		  ["spec/routing/#{m[1]}_routing_spec.rb",
		   "spec/#{m[2]}s/#{m[1]}_#{m[2]}_spec.rb",
		   "spec/acceptance/#{m[1]}_spec.rb",
		   (m[1][/_pages/] ? "spec/requests/#{m[1]}_spec.rb" : 
		                     "spec/requests/#{m[1].singularize}_pages_spec.rb")]
		end
		watch(%r{^app/views/(.+)/}) do |m|
		  "spec/requests/#{m[1].singularize}_pages_spec.rb"
		end
		.
		.
		.
	end

当 integration tests 及 views 有变动时，会自动运行测试。

这些都设置好了，启动 guard 

	bundle exec guard

或

	bin/guard

更多信息请参考：[Guard Github 页面](https://github.com/guard/guard)

### 使用 Spork 来加速测试

运行 rspec 很慢的原因是每次都得重加载整个 Rails 环境。Spork 测试服务器透过加载 Rails 环境，并维护一个进程池(pool of processes)给之后的测试使用。跟 Guard 搭配使用顺风顺水。

配置 Gemfile，将此行加入 `:test group`：

	gem 'guard-spork', '0.3.2'
	gem 'spork', '0.9.0'

范例 Gemfile，放在 Gist:

[MacOSX][MacOSX]  
[Linux][Linux]  
[Windows][Windows]  

运行 `bundle install` 并运行 spork ：

	bundle exec spork --bootstrap

运行 `bundle install --binstubs` 并运行 spork：

	spork --bootstrap # or bin/spork --bootstrap

添加需加载的环境信息至 `spec/spec_helper.rb` 里的 `Spork.prefork`：

	require 'rubygems'
	require 'spork'

	Spork.prefork do
	  # Loading more in this block will cause your tests to run faster. However, 
	  # if you change any configuration or code from libraries loaded here, you'll
	  # need to restart spork for it take effect.
	  # This file is copied to spec/ when you run 'rails generate rspec:install'
	  ENV["RAILS_ENV"] ||= 'test'
	  require File.expand_path("../../config/environment", __FILE__)
	  require 'rspec/rails'
	  require 'rspec/autorun'

	  # Requires supporting ruby files with custom matchers and macros, etc,
	  # in spec/support/ and its subdirectories.
	  Dir[Rails.root.join("spec/support/**/*.rb")].each {|f| require f}

	  RSpec.configure do |config|
	    # == Mock Framework
	    #
	    # If you prefer to use mocha, flexmock or RR, uncomment the appropriate line:
	    #
	    # config.mock_with :mocha
	    # config.mock_with :flexmock
	    # config.mock_with :rr
	    config.mock_with :rspec

	    # Remove this line if you're not using ActiveRecord or ActiveRecord fixtures
	    config.fixture_path = "#{::Rails.root}/spec/fixtures"

	    # If you're not using ActiveRecord, or you'd prefer not to run each of your
	    # examples within a transaction, remove the following line or assign false
	    # instead of true.
	    config.use_transactional_fixtures = true

	    # If true, the base class of anonymous controllers will be inferred
	    # automatically. This will be the default behavior in future versions of
	    # rspec-rails.
	    config.infer_base_class_for_anonymous_controllers = false
	  end
	end

	Spork.each_run do
	  # This code will be run each time you run your specs.

	end

启动 Spork 服务器：

之前使用 `bundle install`：

`bundle exec spork` 

之前使用 `bundle install --binstubs`

`bin/spork`

加入此行至 `.rspec` ，让 RSpec 缺省使用 spork：

	--drb

**提示** ：

如果改动了 `routes.rb` 需重启 Spork 服务器，如果你觉得测试是对的，但是失败了，也可以重启 Spork 服务器试试看。

更多信息请参考 [Spork Github 页面](https://github.com/sporkrb/spork)

### Guard 搭配 Spork

有了 Guard 与 Spork 以后，让它们合体：

	bundle exec guard init spork
	bin/guard init spork

加入此行至 Guardfile：

	guard 'spork', :rspec_env => { 'RAILS_ENV' => 'test' } do
	  watch('config/application.rb')
	  watch('config/environment.rb')
	  watch(%r{^config/environments/.+\.rb$})
	  watch(%r{^config/initializers/.+\.rb$})
	  watch('Gemfile')
	  watch('Gemfile.lock')
	  watch('spec/spec_helper.rb')
	  watch('test/test_helper.rb')
	  watch('spec/support/')
	end

	guard 'rspec', :version => 2, :all_after_pass => false, :cli => '--drb' do
	  .
	  .
	  .
	end

现在全都设定好了，以后只要

`bundle exec guard` 或 `bin/guard` 

Guard 就会自动启动 Spork 服务器并侦测你的改动！

打完收工。。。

[gcomplete]: https://gist.github.com/2555614
[MacOSX]:https://gist.github.com/2555402  
[Linux]:https://gist.github.com/2555397 
[Windows]:https://gist.github.com/2555403
[guard]: http://rubygems.org/gems/guard
