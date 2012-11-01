---
layout: post
title: "Micro Ruby notes"
date: 2011-11-03 09:58
comments: true
categories: [Ruby]
tags: Ruby
published: false
---

For my personal cosulting...    
No guarantees XD

``` ruby
puts('huang')
```

<!--more-->

**Constructor:**

``` ruby
    instance = Class.new
``` 

**instance variable:**

``` ruby    
	@var
```

**Ruby naming convention:**

**methods, variables**

> using line_item instead of lineItem

**Ruby's symbol**

	":" + var

> e.g., :name, :action, :id...etc.

**Define a method:**

``` ruby
	def methodName
    	# your code goes here
	end
```

**Expression Interpolation:**
``` ruby
	def say(name)
	  puts "hi, #{name.capitalize}"
	end
```

``` ruby
$ puts say(juan)    
>> "hi, Juan"
```

**Ruby Class:**

``` ruby
	Class order < ActiveRecord::Base
		
		has_many :line_items
		
		def self.find_all_unpaid 
			find(:all, 'paid=0')
		end
	
		def total
			sum=0
			line_items.each {|li| sum += li.total}
		end
	end
```

> A method with "self." is a class-level method 

**Quick access to Instance variable:**

``` ruby
    Class Car
        attr_accessor :name # Read & Write
        attr_reader :color # read only
        attr_writer :weight # write only
```

**Public / Private / Protected :**

> Public for everyone, protected for instances with same class, private instance only.

**Modules:**

> You can define it but cannot create it. For sharing methods and naming spaces issue.

**Array:**

``` ruby
	a = [ '1', 23, 7.6, 'ppl' ]
	age = [ ]
```

**\'<<\' operator (Appending at the end)**

``` ruby
	for person in @people
	  age << person.age
	end
```

**Quickly for declaring char array:**

	a [ 'a', 'b', 'c', 'd'] is equivalent to a %w{a b c d}

**Hash:**

``` ruby
	sample_hash = {
	    :a => 'a'
	    :b => 'b'
	}
```

**To get value of symbol a:**

``` ruby
	sample_hash[:a]
```

**Hashes and Parameter List:**

``` ruby
	redirecto_to :action => 'show' , :id => product.id
```

**Control Structures:**

``` ruby
	if a > 10
	  puts 'a>10'
	elsif a == 3
	  puts 'a=3'
	else
	  puts 'a<10&a!=3'
	end

	while a<100
	  a += 1
	end
```

**with only 1 expression**

``` ruby
	puts 'a>10' if a > 10
	distance *= 1.2 while distance < 100
```
**Blocks and Iterators:**

Single Line Block 
	{ ... }
	
Multi-line Block
``` ruby
    do
      club.enroll(person)
      person.socialize
    end
```
> The block can only invoke right after method call.

``` ruby
	greet ("Huang", "Ni-hao") { puts "Hi" } # greet is a method
```

> method_call (parm1, ...) { block }


**Example usage:**

``` ruby
	animals.each { |animal| puts animal}
	3.times { print 'I love you' }
```

**Exceptions:**

``` ruby
	begin
	  	#your code here
	  rescue BlogDataNotFound
	    #do something
	  ...
	end
```

**Require:**

> loading resources outside    

``` ruby
	require File.dirname(___FILE___) + '/.../test_helper'
```

**Ruby api cosult:**

`$ gem_server`

Go to <http://localhost:8808> for consulting.
