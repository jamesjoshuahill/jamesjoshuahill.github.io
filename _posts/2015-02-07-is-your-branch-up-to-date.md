---
layout: post
title: "Is your branch up-to-date?"
categories: note
---
git can be confusing, especially for beginners. Even a common message: `Your branch is up-to-date with 'origin/master'.` might not mean what you think. Nowadays I'm comfortable with my git workflow and rarely see an error, but I can still remember feeling completely lost.

I started coaching at [Codebar](http://codebar.io) last year. It's a free workshop to get to grips with the basics of web development. I've found that sharing knowledge with a beginner is harder than understanding. Telling someone else shines a light into my blind spots. If you're near a Codebar meetup, sign up and come along! It's a friendly group and you're bound to learn something.

## Where is origin/master?

Recently I was asked 'How do I know if my branch is up-to-date?' This question led to a git fundamental: **nearly every git operation is local**. Maybe you've heard this before, but it's worth another look.

Nearly everything you do with git happens on your machine. Don't take my word for it. Turn off your wifi and see how many git commands you can run. You'll see `fetch`, `pull` and `push` fail without a connection to your remote, but try the other commands you can think of: `status`, `commit`, `checkout`, `cherry-pick`, `merge`, `rebase`, `diff`, `log` and see how many times git tells you that you're up-to-date. How can you be up-to-date if you're disconnected?

You may not have realised that git keeps a clone of your remote repositories on your machine. That's how you can do so much without a connection. If you're using a GitHub repository as your remote, then there's a clone of it in your local repository. `origin/master` is not on GitHub, it's the clone of the remote `master` branch on your machine.

Next time git tells you that you're up-to-date it might help you to think:

{% highlight bash %}
Your branch is up-to-date with your clone of 'master' from 'origin'.
{% endhighlight %}

## Fetch is manual

It's up to you to keep your local clone of the remote updated. git won't remind you to synchronise with your remotes; you have to remember. When you run `git fetch origin` the list of branches and commit history is downloaded from GitHub and synchronised into the clone on your machine. Doing a fetch won't affect your local branches, so it's one of the safest git commands you can run. You can fetch as much as you like.

Remembering to run `git fetch origin` does feel laborious. As I tap this article it's being saved to the cloud continuously in the background.  Sync has become an everyday part of so many apps, but everything in git is manual.

To check if you're up-to-date with GitHub run `git fetch origin` before `git status` and you'll know you're up-to-date. At least you were a few seconds ago! You're only as up-to-date as your last fetch.

## Checking out a branch from GitHub

One evening a student worked on a new feature at Codebar and wanted to continue working on another computer at home. She had started a new branch and pushed it to GitHub. I gave her a shortcut to try:

{% highlight bash %}
# Instead of repeating the branch name
git checkout -b new-feature origin/new-feature

# Use the same branch name and set up tracking
git checkout -t origin/new-feature
{% endhighlight %}

It's handy if you use the same name for your branches locally and on GitHub. Even better, it sets up tracking so you can `git push` straight away, without `-u origin new-feature` to set the upstream branch the first time. However, when she tried it at home, git threw an error:

{% highlight bash %}
$ git checkout -t origin/new-feature
fatal: Cannot update paths and switch to branch 'new-feature' at the same time.
Did you intend to checkout 'origin/new-feature' which can not be resolved as a commit?
{% endhighlight %}

She felt lost. git threw a fatal error and questioned her _intention_, how rude? I looked back at git askance and had a rubber duck moment. This is roughly how my one-sided conversation with git went:

> JOSH: Oh. I don't recognise that error. Hmmm.
> 
> Yes, I want to checkout 'origin/new-feature'.
> 
> That's the correct branch name, no typos.
> 
> I can see the branch on GitHub, it's definitely there...
>
> TOTORO: ...
> 
> (penny drops)
>
> JOSH: ...oooooh!


I realised that she hadn't run `git fetch origin` first, so git threw a fatal error because it didn't know the new branch existed. The clone on her home computer was not in sync with GitHub.

When she ran `git fetch origin` the new branch was downloaded and then she was able to checkout. Phew! I didn't see that error coming and caught out because I take fetching for granted. That's what happens when you step out of your routine.

You might think that when git throws this error it would be a perfect opportunity to remind you how long it has been since you fetched from GitHub, but no. Instead, I think git assumes you know how it works, so the error message politely suggests that you've made a typo.

## Get an overview

When I have two or more branches on the go I find it's useful to see an overview. Here's how to see a summary of all your local branches, which remote branch they are tracking and their status:

{% highlight bash %}
# A summary of all local branches with their tracking branch and status
$ git branch -vv
* git-up-to-date dafa4b4 [origin/git-up-to-date: ahead 1] Add git up-to-date post
  master         991f4cd [origin/master] Fix footer nav margin
{% endhighlight %}

For example, I have two branches locally. I am on `git-up-to-date` branch and it is ahead of `origin/git-up-to-date`. So I have one commit to push to GitHub.

## Can you be completely up-to-date?
 
Sure. If no one else has access to the GitHub repository then you can rest easy between each fetch. When you're the only one pushing changes then you're in control and you'll be up-to-date all the time. The only gotcha is when you use another computer, then you need to fetch each time you switch.

If you're collaborating with other people on GitHub, then hopefully the next time you see `Your branch is up-to-date with 'origin/master'` you'll wonder how long it's been since your last fetch. It's up to you to keep your local clone in sync and up-to-date with your team.

When you collaborate it's best to work in separate branches to avoid conflicts. Even so, in a shared repository I'm not sure you can ever be completely up-to-date with GitHub. Maybe just for a moment, when you push and take the lead.