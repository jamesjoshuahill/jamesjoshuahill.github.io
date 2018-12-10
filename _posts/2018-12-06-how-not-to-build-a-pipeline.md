---
layout: post
title: "How NOT to build a pipeline"
categories: talk
---
Mirah and I delivered this talk at the [Concourse London User Group](https://www.meetup.com/Concourse-London-User-Group/events/256171643/) at Pivotal London's office. We shared the mistakes and anti-patterns we discovered in our team's [Concourse CI](https://concourse-ci.org/) pipelines over the last six months.
<div class="embed-container ratio16x9 slideshare">
  <iframe src="//www.slideshare.net/slideshow/embed_code/key/n5IaarJx7xsImQ" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe>
</div>

Pipelines are the infrastructure we use to test and deliver our code. We work with them every day, but sometimes they behave in unexpected ways. We will go over common failure modes and issues we have encountered in our Concourse pipelines, and understand what we can do to prevent and solve these pain points.

Being able to build pipelines that work for you is critical for effective dev/ops. By sharing our own mistakes, we hope that you will be able to recognize them when they happen and know what to do to fix the problems.
