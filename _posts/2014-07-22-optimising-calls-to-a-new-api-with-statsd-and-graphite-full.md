---
layout: post
title: "Optimising calls to a new API with StatsD and Graphite"
source: globaldev.co.uk
source_url: https://globaldev.co.uk/2014/07/optimising-calls-to-a-new-api-with-statsd-and-graphite/
published: false
---

Monitoring calls to third-party APIs can reveal interesting trends and alert
you to problems. Following
[my last post]({{ site.baseurl }}/2014/07/15/back-off-and-retry-with-rabbitmq/), I describe how we
used StatsD and Graphite to monitor calls to a new API and optimise an
exponential back-off and retry mechanism.

-----

## Monitoring a new API

This story began with a graph. When we started using the new
[Akamai CCU REST API](https://api.ccu.akamai.com/ccu/v2/docs/index.html) we
wanted to get a feel for it. So we hooked up a graph of the status codes we
received from the API. Our tools of choice to gather and graph real-time stats
are:

  - [StatsD](https://github.com/etsy/statsd) to collect and aggregate stats,
  - [Graphite](https://graphite.wikidot.com) to generate real-time graphs, and
  - [Graphiti](https://github.com/paperlesspost/graphiti) as an alternative
    front-end for Graphite.

We have been running with this powerful monitoring stack for a while. So,
standing on the shoulders of the globaldev team who set it up, I could add
tracking of the new API's status codes to a [Node.js](https://nodejs.org)
application with one line of code:

```javascript
statsd.increment("akamai.response." + response.statusCode);
```

This creates and increments a counter for each status code, e.g.
`akamai.response.201` for successful calls. Very quickly, a graph of the API
response status codes visualised the number one issue: `akamai.response.507`.
During peak hours the API was rejecting a large number of calls when its
internal queue for processing calls was full. Here is the pattern of
API responses we saw over one week:

![API response pattern over one week]({{ site.baseurl }}/assets/week-of-api-responses.png)

This graph kicked off the development of the exponential back-off and retry
mechanism I described in
[my last post]({{ site.baseurl }}/2014/07/15/back-off-and-retry-with-rabbitmq/).

## Backing off just enough

When we put our exponential back-off and retry mechanism in place, the graph of
API status codes was very useful. More useful than our log files because it laid
bare the pattern of failed API calls during peak hours. Not only could we see
the proportion of failure vs success, but also the extent of peak hours from
8pm—2am.

Visualising the data allowed us to tailor the exponential back-off and retry
mechanism to the new API from the start. Our goal was to minimise the number of
retry attempts and achieve success for all our API calls before the start of
the next day.

We used three settings to tweak how long each API call waited before trying
again:

  - `initialTTL`, how long to wait before the first retry;
  - `multiplier`, to increase the wait each time a call fails; and
  - `randomiseBy`, how much to randomise the wait time to spread out retry
    attempts.

However, it's not enough to pick values in the right ballpark. In order to test
their performance we needed additional monitoring to see how these settings
interact. We settled on:

  - `retry attempt`, to track how many times we retry an API call; and
  - `estimated minutes`, a useful metric provided by the API that indicates the
    length of the API's internal queue for processing calls.

With these in place we were ready to test the settings overnight.

## Night 1

Monitoring `estimated minutes` was very useful, because it showed how long
the API took to recover from peak traffic. We added this to our graphs on a
second y-axis.

The API's queue grew during the afternoon, reached its limit at 22:20 and
started rejecting calls. This is a good example of useful data that APIs can
provide to users. Note that the number of calls we sent was not much greater in
the evening, so the API was probably pushed to its limit by Akamai's many other
users.

![Night 1 API responses]({{ site.baseurl }}/assets/night-1-responses.png)

Whilst the graph of status codes gave us context, a graph of retry attempts let
us evaluate our exponential back-off and retry mechanism and the values we chose
for its three settings.

![Night 1 API retry attempts]({{ site.baseurl }}/assets/night-1-retries.png)

### `initialTTL`
On night one the 1st and 2nd retry attempts were too soon. The API was still
under heavy load, so we saw 3rd and even a handful of 4th retry attempts after
07:00. (The small line of brown 4th retries almost went unnoticed under the peak
of red 1st retries!) This indicated that making the `initialTTL` much longer
could increase the chance of success on the 1st or 2nd retry.

### `multiplier`
The 3rd and 4th retry attempts we saw would have been successful if they were
made sooner after the previous attempt. There were almost no retries after 01:30
until 07:20! This indicated that reducing the `multiplier` could reduce the
total time to achieve a successful API call.

### `randomiseBy`
We also noticed that the retry attempts were too close to one another. Shortly
after 01:00 a number of 3rd retries refilled the API queue causing a spike of
failed calls. This indicated that increasing `randomiseBy` could spread out the
retry attempts and reduce clumps that might refill the API queue.

After reflecting on the data we tweaked the settings—a longer `initialTTL`,
smaller `multiplier` and greater `randomiseBy`—and tested them overnight.

## Night 2

We saw a similar level of peak traffic and noticed that failed calls started
earlier that the night before.

![Night 2 API responses]({{ site.baseurl }}/assets/night-2-responses.png)

Nevertheless, with the new settings the majority of API calls were successful on
the 1st retry attempt. And the rest were successful on the 2nd. We also met our
goal of completing all retries before the start of the next day. Hurrah!

![Night 2 API retry attempts]({{ site.baseurl }}/assets/night-2-retries.png)

This was a great result; the kind of _before and after_ that rarely appears.
It's a joy when a graph clearly demonstrates a positive result :o)

-----

## That's all folks!

Of course, the task of monitoring a third-party API is never done and we
continue to watch our stats. Hopefully, this will give you ideas for how to
monitor and collect real-time data on your API calls and optimise them.
