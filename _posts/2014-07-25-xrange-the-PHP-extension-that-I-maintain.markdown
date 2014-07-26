---
layout: post
title:  "xrange, the PHP extension that I \"maintain\""
date:   2014-07-25 22:19:00
categories: PHP PECL Opensource
---

A few years ago, after being bewildered by infinite loop problems and convoluted paging algorithms, I wondered why the PHP community hadn't adopted iterator based looping and sunset the three statement for loop like Python.

Some of the resistance I encountered were arguments regarding memory efficency & performance using the range() function. These were the days where PHP lacked generators and yield statements.

In [Python's image](https://docs.python.org/2/library/functions.html#xrange), I built xrange(). I wrote an article, [Killing The For Loop](http://www.phpdeveloper.org/news/9481), about it in [PHP\|Architect](http://www.phparch.com/) magazine (when still in print) and published my [extension](http://pecl.php.net/package/xrange) into the [PECL](http://pecl.php.net/) respository.

In combination with PHP's [SPL](http://php.net/manual/en/book.spl.php), you can do some quite amazing things. For those that don't know, SPL is the PHP "equivalent" of C++'s [Standard Template Library](http://en.wikipedia.org/wiki/Standard_Template_Library). It offers generic algorithmic data structures, iterators and such. Following is a contrived example, using one of my own package supplied filters.

{% highlight php %}
<?php
assert(extension_loaded("xrange"));

// display all odd numbers 1 .. 20
print_r(array_values(
	iterator_to_array(
		new OddFilterIterator(xrange(1, 20))
	)
));
{% endhighlight %}

The real power comes from chaining slicing, appending and filtering iterators together. Creating large batch sets of numbers together without any memory overhead.

Last I heard, it's still a standard package in the [SUSE Linux](https://www.suse.com/) repositories. You can still use it, include the source I published in the article, or adopt the modern generator syntax... which I'm unsure works with SPL natively.
