---
layout: post
title: Ruby vocabulary
category: ruby
---
There are many ways to produce a result in Ruby. Most of the discussions I have read focus on the performance of alternatives, but what could your choice of method tell the next developer about your intention?

To illustrate this point I've chosen three methods from Enumerable: `map`, `inject` and `each_with_object`, and I'll start with a list of numbers:

{% highlight ruby %}
numbers = [1, 2, 3, 5, 7, 11, 13]
{% endhighlight %}

## Transpose

{% highlight ruby %}
numbers.map { |number| number * 10 }

numbers.inject([]) { |result, number| result << number * 10 }

numbers.each_with_object([]) { |number, result| result << number * 10 }

# => [10, 20, 30, 50, 70, 110, 130]
{% endhighlight %}

## Sum

{% highlight ruby %}
sum = 0
numbers.map { |number| sum += number }
sum

numbers.inject(0, :+)
# => 42

numbers.each_with_object(0) { |number, sum| sum += number }
# => 0  Huh?
{% endhighlight %}

## Transform

{% highlight ruby %}
table = {}
numbers.map do |number|
  group = number / 10
  table[group] = [] unless table.key?(group)
  table[group] << number
end
table

numbers.inject({}) do |table, number|
  group = number / 10
  table[group] = [] unless table.key?(group)
  table[group] << number
  table
end

numbers.each_with_object({}) do |number, table|
  group = number / 10
  table[group] = [] unless table.key?(group)
  table[group] << number
end

# => { 0 => [1, 2, 3, 5, 7], 1 => [11, 13] }
{% endhighlight %}
