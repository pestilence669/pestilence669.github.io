---
layout: post
title:  "Scala: Implicit Classes"
date:   2016-07-11 23:02:00
categories: Scala language OOP magic
---

[Implicit classes](http://docs.scala-lang.org/overviews/core/implicit-classes.html)
in [Scala](http://scala-lang.org/) are an underused and oft misused feature. I
don't feel that they are explained very well and have a bit too much mystery for
the beginner to grasp. I was playing around and thought it might help to show
the explicit syntax, to more easily explain the "magic" to someone.

In a nutshell:

{% highlight scala %}
import scala.language.postfixOps

object Factorial {

  implicit class IntDecorator(val n: Int) {
    def ! = 1 to n product
  }

  def factorial(n: Int) =  n!                 // implicit

  def factorial2(n: Int) = IntDecorator(n).!  // explicit

}
{% endhighlight %}

