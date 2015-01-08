---
layout: post
title: "Handling failed builds on GitHub Pages"
categories: note
---
Last month I created this site with [Jekyll 2.0] and took advantage of the free hosting on [GitHub Pages]. The deployment process is effortless: `git push origin master`. If you've used Heroku this looks familiar, but on GitHub Pages you won't see any details of the deployment. So what happens if the build fails?

As I walked through the set up I realised that GitHub Pages does more than host my site, it builds it too. Everytime I push a new commit to `master`, GitHub builds my static site and serves it to the world via their CDN. Nice!

Unlike other hosts you can't control the production environment on GitHub Pages. Their generosity has some sensible limits. Thankfully GitHub won't deploy a failed build, but unless you check your site everytime you push you won't know if your changes have been deployed.

Here's how I avoid builds failing when GitHub Pages is updated and get a notification when a build fails.

## Use the same versions

Instead GitHub publishs the [dependencies and versions] and provide a handy JSON endpoint. In the Jekyll tutorial it shows how to call the endpoint provided in your `Gemfile` to specify the version of the `github-pages` gem running in production:

{% highlight ruby %}
source "https://rubygems.org"

require "json"
require "open-uri"
versions = JSON.parse(open("https://pages.github.com/versions.json").read)

gem "github-pages", versions["github-pages"]
{% endhighlight %}

This means that with every `bundle` the production version of the gem will be used. To keep track of updates I commit my `Gemfile.lock` to record the last version. The `github-pages` gem has been updated twice in the month or so since I created this site.

Ok, so I'm keeping up with changes to the `github-pages` gem. But what about the Ruby version? The endpoint gives several other details about the GitHub Pages production environment, here's the full response:

{% highlight ruby %}
{
  "jekyll"=>"2.4.0",
  "jekyll-coffeescript"=>"1.0.1",
  "jyll-sass-converter"=>"1.2.0",
  "kramdown"=>"1.3.1",
  "maruku"=>"0.7.0",
  "rdiscount"=>"2.1.7",
  "redcarpet"=>"3.1.2",
  "RedCloth"=>"4.2.9",
  "liquid"=>"2.6.1",
  "pygments.rb"=>"0.6.0",
  "jemoji"=>"0.4.0",
  "jekyll-mentions"=>"0.2.1",
  "jekyll-redirect-from"=>"0.6.2",
  "jekyll-sitemap"=>"0.6.3",
  "github-pages"=>"31",
  "ruby"=>"2.1.1"
}
{% endhighlight %}

Aha, there's the Ruby! So I can specify the production Ruby in my `Gemfile` as well:

{% highlight ruby %}
ruby versions["ruby"]
{% endhighlight %}

The Ruby version isn't recorded in `Gemfile.lock` so I track changes manually in `.ruby-version`, because I use [rbenv] to manage my Rubies locally. So when the Ruby version changes in production I see a warning when I `bundle`:

{% highlight bash %}
Your Ruby version is 2.1.0, but your Gemfile specified 2.1.1
{% endhighlight %}

Now I know that I'm using the same versions of Ruby and `github-pages` when I test my site locally and there's less to go wrong when I deploy to production. And if something fails after a version upgrade I'll be able to compare the last working versions recorded in `Gemfile.lock` and `.ruby-version` and narrow down the cause.

## Get notifications from Travis CI

Checking your site after every push is a chore. And to make things worse, I'm guilty of pushing minor changes without testing. I guess we've all done it. I have thrown caution to the wind and broken the build several times, but I get an email shortly afterwards reporting my foolishness. Continuous integration is my friend.

Setting up Travis CI for a GitHub Pages site is straight-forward. Check out the [continuous integration tutorial] and never miss a failed build again. I highly recommend using `html-proofer` to check all your links and images are working too.

Take a look at the [full source code] of this site and good luck with your deployments.

[Jekyll 2.0]: http://jekyllrb.com
[GitHub Pages]: https://pages.github.com
[dependencies and versions]: https://pages.github.com/versions/
[rbenv]: http://rbenv.org
[continuous integration tutorial]: http://jekyllrb.com/docs/continuous-integration/
[full source code]: https://github.com/jamesjoshuahill/jamesjoshuahill.github.io