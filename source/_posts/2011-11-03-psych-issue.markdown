---
layout: post
title: "couldn't parse YAML, psych.rb:148"
date: 2011-11-03 10:02
comments: true
categories: [octopress, yaml, psych.rb]
tags: octopress
published: true
---
I'm blogging with `octopress` and my ruby version is `ruby 1.9.2p290`

While running:

`$ rake generate`

You see this error:

``/Users/Mac/.rvm/rubies/ruby-1.9.2-p290/lib/ruby/1.9.1/psych.rb:148:in `parse': couldn't parse YAML at line 5 column 0 (Psych::SyntaxError)
``

<!--more-->

This error you see is probably **you have some invalid yaml somewhere around your code**.

> psych.rb is a new ruby YAML parser.

You may find solutions from Stack Overflow and octopress support forum below.

[Rails error, couldn't parse YAML] [1]    
[error with rake generate] [2]

[1]: http://stackoverflow.com/questions/4980877/rails-error-couldnt-parse-yaml
[2]: https://github.com/imathis/octopress/issues/57


My case I found it is a simple yaml error when creating new post.
Every new post begins with yaml stuff:

<p>
&#45;&#45;&#45; <br>
layout: post    <br>
title: \"some title\" <br>   
date: 2011-11-03 10:00 <br>   
comments: true <br>   
&#45;&#45;&#45; <br>
</p>

If you accidentally write:

<p>
&#45;&#45;&#45; <br>
<strong>layout:post</strong> <br>
title: \"some title\" <br>   
date: 2011-11-03 10:00 <br>   
comments: true <br>   
&#45;&#45;&#45; <br>
</p>

You'll see this error because you do NOT have space between `':'` and the following value.
**Make sure you save a space after `':'`**

Hope it helps!
