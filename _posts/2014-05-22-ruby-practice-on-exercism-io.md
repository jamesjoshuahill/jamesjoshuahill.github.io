---
layout: post
title: Ruby practice on exercism.io
---
Last week I joined [exercism.io] to practise Ruby. I'm looking forward to
iterating on the problems set out by [@kytrinyx] and co. I think the
open-ended nature will encourage me to iterate and practise lots of small decisions.

<blockquote class="twitter-tweet" lang="en"><p>Hey <a href="https://twitter.com/nodunayo">@nodunayo</a>, I just submitted my first exercism! Leave me a nitpick at <a href="http://t.co/Ctvmd5AFvH">http://t.co/Ctvmd5AFvH</a></p>&mdash; Josh Hill (@jamesjoshuahill) <a href="https://twitter.com/jamesjoshuahill/status/466967829032366080">May 15, 2014</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

## Free tests

Each exercise comes with some instructions and a test file. Yes, free tests! so you can concentrate on writing code to make them pass one by one. I start my getting all the tests passing with the minimum amount of code possible. Then once they're passing and my head has engaged with the problem, I look for opportunities to refactor.

## Iterate

Like many code practice sites, once you've submitted your solution you can see other people's solutions. This is a great resource for finding alternative ways to write a solution. As part of my practice I try to find at least one or two alternatives I can try out. I've discovered several standard library methods already. And I've found that being able to submit several iterations of each exercise has encouraged me to.

## Short feedback loop

I enjoy TDD with a short feedback loop. I use [Guard] to run the tests. Since they're written in MiniTest you'll need:

{% highlight bash %}
gem install guard-minitest
{% endhighlight %}

If you use Terminal.app on a Mac, you can get a notification each time Guard runs the tests by installing a handy gem:

{% highlight bash %}
gem install terminal-notifier-guard
{% endhighlight %}

I put a copy of the following `Guardfile` in each exercise folder, so that Guard knows to look in the same directory, fire up Sublime Text and run `guard`.

{% highlight ruby %}
# A sample Guardfile for Ruby exercises from exercism.io
# More info at https://github.com/guard/guard#readme

guard :minitest, test_folders: '.' do
  # with Minitest::Unit
  watch(%r{^(.+)_test\.rb}) { |m| "./#{m[1]}_test.rb" }
end
{% endhighlight %}

With this set up, every time I save the test file Guard runs the tests for me.

See you on [exercism.io]!

[exercism.io]: http://exercism.io
[@kytrinyx]: https://twitter.com/kytrinyx
[Guard]: http://guardgem.org
