---
layout: post
title: "Tailor your monkeys with refinements"
categories: note
---
One of the most powerful features of Ruby is open classes. You can reopen any class and change, or extend it. Unfortunately these _monkey patches_ have global scope, so their convenience comes with possible side effects. In Ruby 2.1+ refinements allow you to limit the scope of _monkey patches_, so you can enjoy their convenience again.

## blank?

Ruby on Rails brought many monkey patches into mainstream use and they've become second nature. For example, ActiveSupport provides a `#blank?` method on almost every object by monkey patching several standard library classes:

{% highlight bash %}
Object#blank? #=> [true, false]
Array#blank? #=> [true, false] alias of Array#empty?
Hash#blank? #=> [true, false] alias of Hash#empty?
String#blank? #=> [true, false] using a regular expression to detect empty and whitespace only strings

NilClass#blank? #=> true
FalseClass#blank? #=> true

TrueClass#blank? #=> false
Numeric#blank? #=> false
{% endhighlight %}

[Read the source code](https://github.com/rails/rails/blob/7847a19f476fb9bee287681586d872ea43785e53/activesupport/lib/active_support/core_ext/object/blank.rb) in ActiveSupport 4.2.0.

What's your favourite monkey patch in Rails? Maybe it's `"octopus".pluralize`, or `3.months.ago`?

## Rolling your own

`#blank?` is so handy that we missed it when we started writing a new Ruby app at [globaldev](http://www.globaldev.co.uk). Because we want to avoid dependencies whenever possible, we turned to refinements to roll our own version, tailored to our needs.

In this case, we wanted a convenient syntax for checking parameters in a Rack app. To handle missing or empty parameters we had vanilla Ruby code like:

{% highlight ruby %}
member_id = String(request.params["member_id"])
if member_id.empty?
  # return 400 Bad Request
end
{% endhighlight %}

For our use case we only needed to handle `nil` and `""`, so we extended `NilClass` and `String` using refinements:

{% highlight ruby %}
module Blank
  refine String do
    alias_method :blank?, :empty?
  end

  refine NilClass do
    def blank?
      true
    end
  end
end
{% endhighlight %}

You can group several refinements in a single module and activate them together in your code. With this refinement we could reduce the boilerplate code for handling parameters to:

{% highlight ruby %}
using Blank

if request.params["member_id"].blank?
  # return 400 Bad Request
end
{% endhighlight %}

## Scope

The purpose of refinements is to limit the scope of monkey patches, which should make them easier to reason about and avoid unintended consequences. In addition, refinements must be activated explicitly, which makes it clear when they are active.

The scope of refinements is per file and lexical. You can activate them at the top-level of a file and they will be activated until the end of the file. Or you can activate them inside a class or module and they will be activated until the end of the class or module definition.

Here is an example file showing how our `#blank?` refinements can be scoped to a single class definition.

{% highlight ruby %}
require_relative "blank"

class App
  using Blank
  # activated here
  def call(env)
    # here
  end
  # and here
end

# but not here
{% endhighlight %}

[Read the documentation](http://ruby-doc.org/core-2.1.1/doc/syntax/refinements_rdoc.html) on ruby-doc.org.

With refinements we can enjoy the wonderful convenience of monkey patching Ruby with less potential for bugs. Enjoy!

---

P.S. If you'd like to see another example in action. Check out my latest implementation of [FizzBuzz](https://github.com/jamesjoshuahill/fizzbuzz-enumerator) using Enumerator and a refinement of Integer.
