---
layout: post
title:  "Almost two years later, the Boost C++ Library project finally merges my patch"
date:   2014-07-05 14:57:00
categories: C++ Boost Opensource KIXEYE "War Commander"
---

Almost two years ago, I was using [Boost's PropertyTree](http://www.boost.org/doc/libs/1_55_0/doc/html/property_tree.html) library as a JSON serializer. It had a bug that included extra whitespace in the output, when disabling the "pretty" option. I submitted a [patch](https://svn.boost.org/trac/boost/ticket/7180).

I implemented it locally, to reduce bandwidth for a [game title](https://www.kixeye.com/game/warcommander/home/) I was working on. The bandwidth savings add up, given the frequency of data refresh. It's a simple fix.

{% highlight diff %}
diff -dur boost.old/property_tree/detail/json_parser_write.hpp boost.new/property_tree/detail/json_parser_write.hpp
--- boost.old/property_tree/detail/json_parser_write.hpp	2012-07-26 19:42:10.000000000 -0700
+++ boost.new/property_tree/detail/json_parser_write.hpp	2012-07-26 19:43:34.000000000 -0700
@@ -93,7 +93,8 @@
                     stream << Ch(',');
                 if (pretty) stream << Ch('\n');
             }
-            stream << Str(4 * indent, Ch(' ')) << Ch(']');
+            if (pretty) stream << Str(4 * indent, Ch(' '));
+            stream << Ch(']');
 
         }
         else
{% endhighlight %}

It was finally merged to master five months ago.

I you work in C++ and haven't tasted the Boost libraries, I'd highly encourage you to do so. Modern C++ doesn't resemble old school C in the slightest. Some of my most favorite libraries in the world have been included in the [C++11 standard](http://en.wikipedia.org/wiki/C%2B%2B11).

This was done, and made possible, by Adobe's [FlasCC](http://www.adobe.com/devnet-docs/flascc/docs/Reference.html) initiative. [KIXEYE](http://kixeye.com/) ported all of their [ActionScript](http://en.wikipedia.org/wiki/ActionScript) to C++ to run both on the client and server with a shared code base, during my multiplayer implementation project, that I lead. The game still runs in the [Flash Player](http://get.adobe.com/flashplayer/)... with more explosions.
