---
layout: post
title: "A welcome contribution"
categories: open-source
---
I have been working through the Ruby exercises on [exercism.io] from time to time for seven months. It provides a great resource to practise writing code in different ways. Yesterday I found a small wrinkle and had an opportunity to give something back.

## A very small bug

I was working through the `crypto-square` exercise and one of the tests didn't seem right. This was the first time I've ever questioned a test from exercism.io, so I wasn't sure what to do. Once I'd submitted my first iteration I looked through the other submissions and found the magic number `5` everywhere.

I decided it was probably a bug, so I went GitHubbing. It didn't take long to discover the **exercism/xruby** repository where all the Ruby exercises live and an [open issue] reporting the bug!

## Bonus round

With the bug confirmed, I fixed the broken test and opened a tiny [pull request]. To my delight, [@kytrinyx] merged my change the same day and hinted that there were a few more test cases in the C# version. I've never worked with C#, but the test cases were easy to read, so I ported several extra tests to Ruby and opened a [second pull request].

I was encouraged by this encounter and look forward to contributing to exercism.io again.

[exercism.io]: http://exercism.io
[open issue]: https://github.com/exercism/xruby/issues/37
[pull request]: https://github.com/exercism/xruby/pull/54
[@kytrinyx]: https://twitter.com/kytrinyx
[second pull request]: https://github.com/exercism/xruby/pull/55
