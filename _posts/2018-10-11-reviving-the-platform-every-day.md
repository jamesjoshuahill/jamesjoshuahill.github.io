---
layout: post
title: "Reviving the platform every day"
categories: talk
---
Emmanouil Kiagias and I talked at Cloud Foundry EU Summit 2018 about the disaster recovery acceptance tests for Cloud Foundry. This talk is about how we delivered this critical feature of the platform across many teams.
<div class="embed-container  ratio16x9  youtube">
  <iframe src="https://www.youtube.com/embed/8osX_c1XQyI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

Natural disaster hit your data centre? Don't worry. Cloud Foundry is prepared for disaster from day one thanks to built-in support for BOSH backup and restore (BBR). Nice. But how do we know the platform is ready for catastrophe? What if our worst fears come true?

The BBR framework laid the technical foundation for implementing disaster recovery. However, Cloud Foundry is a complex distributed system and contributors are spread across multiple teams and timezones. The challenge was to find a way to drive out this cross-cutting feature across all Cloud Foundry components.

Thus the Disaster Recovery Acceptance Tests (DRATs) were born. Josh and Emmanouil will show you the test framework that continuously tests a critical feature of the platform. DRATs ensures that all the Cloud Foundry components continue to work together, so we can all be confident that the platform can recover when mishaps occur.

After this talk attendees will:
* take away patterns for developing features with cross-cutting concerns.
* understand DRATs and how Cloud Foundry teams test their components.
* understand how to deliver CI tasks that can be shared by many teams in their own CI pipelines.

<div class="embed-container ratio16x9 slideshare">
  <iframe src="//www.slideshare.net/slideshow/embed_code/key/bOVYADQwwkds7Q" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe>
</div>
