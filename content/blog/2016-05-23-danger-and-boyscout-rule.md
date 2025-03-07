---
layout: post
title: 'Boy Scouts rule with Danger'
excerpt: 'Post where I explain how Danger helped us at SoundCloud to apply the programming Boy Scouts rule to our workflow'
modified: 2016-05-23
tags: [danger, github, soundcloud]
---

![Boy Scouts](/images/posts/boyscouts.jpg)

Some months ago I did introduce [Danger](https://github.com/danger/danger) in the SoundCloud project. When I first read about it was in Artsy Engineering Blog where Orta explained how they used at Artsy. For those who don't know what Danger is, it's a Ruby tool designed to be run on CI and allows you to execute some checks on your PRs and report the results back to the PR adding a comment. It's like a linting step but that have access to the PR information and send the report back to the PR.

When we started using it, there was no support for plugins _(now it has)_ and we came up with a solution for creating our reusable checks as explained on this post. With the time we've been adding new checks to Danger and so far we have around 12 Danger checks that run every time someone commits something to GitHub. What initially turned out to be a tool for ensuring good code quality and prevent some mistakes to be merged into master has turned into a tool that enforces the famous [**Boy Scouts Rule for programmers**](http://programmer.97things.oreilly.com/wiki/index.php/The_Boy_Scout_Rule).

If you don't know what the Boy Scouts Rule is about I'll copy & paste it here:

> The Boy Scouts have a rule: "Always leave the campground cleaner than you found it." If you find a mess on the ground, you clean it up regardless of who might have made the mess. You intentionally improve the environment for the next group of campers. Actually the original form of that rule, written by Robert Stephenson Smyth Baden-Powell, the father of scouting, was "Try and leave this world a little better than you found it."
> What if we followed a similar rule in our code: "Always check a module in cleaner than when you checked it out." No matter who the original author was, what if we always made some effort, no matter how small, to improve the module. What would be the result?
> I think if we all followed that simple rule, we'd see the end of the relentless deterioration of our software systems. Instead, our systems would gradually get better and better as they evolved. We'd also see teams caring for the system as a whole, rather than just individuals caring for their own small little part.
> I don't think this rule is too much to ask. You don't have to make every module perfect before you check it in. You simply have to make it a little bit better than when you checked it out. Of course, this means that any code you add to a module must be clean. It also means that you clean up at least one other thing before you check the module back in. You might simply improve the name of one variable, or split one long function into two smaller functions. You might break a circular dependency, or add an interface to decouple policy from detail.
> Frankly, this just sounds like common decency to me — like washing your hands after you use the restroom, or putting your trash in the bin instead of dropping it on the floor. Indeed the act of leaving a mess in the code should be as socially unacceptable as littering. It should be something that just isn't done.
> But it's more than that. Caring for our own code is one thing. Caring for the team's code is quite another. Teams help each other, and clean up after each other. They follow the Boy Scout rule because it's good for everyone, not just good for themselves.
> by Uncle Bob.

That summarizes with this statement `Always leave the campground cleaner than you found it`. The problem is that if you don't commit none of the developers in the team would apply it unless there was something that would force them to do it. There is where Danger played an important role for us.

### Danger enforcing _Boy Scouts rule_

Danger provides you with the list of files that have been modified in the PR. We started running the checks against these files and reporting warnings in the project. Some of these checks that we run against new PRs are:

- Check that there are no `TODO` comments.
- Check if there are header comments.
- Check if there are implemented tests.
- Check if there are Nullability macros.

All these tests are run against **modified files**, and as a result, it warns you to improve these files _(even if you are not the original author)_. For example:

1. I modify a class method because I have to pass an extra parameter.
2. The file doesn't include Nullability Objective-C macros, `NS_ASSUME_NONNULL_BEGIN` _(worse compatibility with Swift)_.
3. I create a PR and Danger will warn me about that modified file not including the macros.
4. I'll take advantage of my changes to add the macros to that file.
5. Voila :tada:, thanks to Danger I improved the project a little bit.

Since we started using it at SoundCloud the project has been improving progressively and we're enforcing new good practices every day with new rules. Whenever we feel something can be _"Danger Checkable"_ we implement the check and add it to the list of existing check.

> How do you ensure good practices in your projects?
