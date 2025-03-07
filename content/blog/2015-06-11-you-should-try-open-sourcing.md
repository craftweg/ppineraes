---
layout: post
title: Why Open Source helps you to become a better developer
excerpt: "Most of developers haven't tried creating an Open Source component before. Since I apply it to every of my projects I feel the results and development process has improved a lot. In this article I will describe why it's so important"
modified: 2014-10-13
tags: [opensource, carthage, cocoapods]
---

For those who are not conscious about that, Open Source is the reason of the existence of many development communities. Would you imagine nowadays the iOS/OSX development without CocoaPods? And what about Ruby without its Gems? A lot of developers around the world put their efforts to simplify your daily stuff publishing their work in an Open Source way through these dependency managers (for them because otherwise it would be impossible to resolve many dependencies conflicts of our projects). Open Source a project doesn't mean just `git push origin` of your projects and making them public. It has some extra implications that will help you as a developer and with your future projects. Have you ever done it before? Would you like to know how it helped to me? Let's see.

### Why I started Open Sourcing some libraries?

When I started developing app some years ago I didn't know about what the term Open Source meant. I started with iOS, by that time there wasn't a dependency manager like CocoaPods and I integrated the libraries manually. There was though, reference websites like [Cocoa Controls](https://www.cocoacontrols.com/) where I could check the last libraries that other developers had published and were offering to the community.

I've always been a curious person and I wonder every day how the things work. I like to say that I can't be happy without knowing what there's inside the magic boxes around us. I wanted to know how these libraries worked, and why developers were spending their time developing libraries instead of working on their projects.

I found the answer, and liked the philosophy behind that. What makes a language very important is not only how good it is and what it offers that others don’t but the community that there’s supporting the language with new tools/libraries/tutorials, …. And Objective-C was building a great community thanks to the mobile apps development and tools like CocoaPods, or libraries like AFNetworking that you sure know about. **People, packaging, code logic, to simplify others stuff and support the community with great tools**. I liked it! I wanted to support the community as well and started giving my first steps sharing some code.

I remember having some friends who started developing apps for iOS as well and that saw (and still see) dependency managers as “tools for those developers that don’t know how to integrate libraries manually” or that think that “those who use libraries are not good developers, they have to use code from others”. **Sorry, but I totally disagree with that**. The point is that you have bundled something you have to code and that would make you save a lot of time. _Why not using it and extending in case you need extra features not supported?_. Those developers tend to see their code as Gollum saw the ring:

- This code is mine and only mine.
- Sharing means, others get advantage of the time I spent coding.
- But yes… I take code from others. And take part passively in the community. Resources rain over me.

> It’s something really worth to try if you’re a Developer and you haven’t done it before.

### Why contributing with Open Source projects helps you as a developer?

I said that it helps to developers but some of you might be thinking why?. These are some points I figured out after creating some Open Source libraries:

- **Think about code structure**: Most of the times we’re constrained by defined patterns that come from the project itself, or maybe the language. **We code for a product** and forget about the code structure. The important fact there is coding a feature, or add a fix there that helps to solve this other bug. If you work in a team this might be a little bit different but if you work as a Freelance it’s something common. When you work on a library others developer are going to use it. The interface has to be clear, the code has to be well structured, otherwise they won’t be able to use “your product”. Before starting coding you’ll analyze your library requirements, how you would use that library if you were a developer and then design the core structure. I feel tempted to not follow these steps when I work for a project which is not a library. **In my last project I’ve bundled the core business logic in modules, for example for 8fit, I called it EFKit, or EFWatchKit for the Apple Watch code** It helps me to think on these code as a module that my main project depends on.
- **Tests are important**: When you have an open source library published on Git developers will start contributing with it. They might not know about all the library and they want to just add an extra functionality. Do you know how easy it’s to introduce a regression there? Having everything tested ensures that nothing is broken and the project keeps stable.
- **Versioning is also very important**: When you’ve other developers depending on your library you have to reflect the library changes through the versioning. I **recommend you to follow the [Semantic versioning 2.0](http://semver.org/)**. That way you can reflect big important changes in the library interface through major updates and use minor updates with small fixes.

> **Open Source opens your mind, and contributes to design cleaner and better code**

### Things you have to keep in mind

When you work an Open Source project that you are going to open to more people there’re some points that you don’t usually take care of but that you should if that project’s going to be opened to more people. These points help to get closer to the project and understand how it works. **You know how it works, or it components** because you have worked on that, but, what about the rest? Developers are your users and if you forget about these points, developers might end up not using your library. What are these points?:

- **Documentation**: Code documentation is very important to understand the behaviour of classes/methods or other library components without digging into its implementation. Think about a method with multiple parameters, and a language not too stricter with types. How does the user know about the parameters you can pass to that method? If you’re using an strongly typed language, great! but otherwise not documented code might lead to big headaches working with the library.
- **Tests**: Do you love testing? You’ll end up doing. Testing is very important on Open Source projects because the more developers you have developing for the library the easier it’s to introduce a regression and that nobody detects it. It’s very important to have your project integrated with any **continuous integration** solution _(Travis, Jenkins, …)_ Most of them are free for Open Source projects.
- **Wiki page**: I hadn’t used Wiki pages until I created my first project on Github. There were a lot of things I had to explain and the README file was getting larger and larger. My recommendation is that if your project size is small enough just to explain it in one page of README, do it there. If the README becomes larger, move it to the Wiki, organize the Wiki in different pages and add a home reference page that links to them.
- **Issues**: Enable your repo issues. Some developers disable them because they don’t want to hear developers complaining about things working or because they don’t know how to use the library. After some libraries you’ll figure out that **issues is the communication channel between developers and you**. And something also important to keep in mind… Not all issues are valuable, don’t stress yourself trying to give a valid answer to all of them. You might find people asking for features that are impossible to support for the library that you designed. Think if it makes sense to add that feature, if it fits into the core code. After that design the feature and implement it. Always **reference the issues** in your Pull Requests because it’s a good way to let the user know that you’re working on that.
- **Contribution guidelines**: Luckily your library will become popular and more developers will contribute with the project. In that case having contribution guidelines will be helpful to avoid messy code in the future. Explain there the code style you’re using, how the project is structured and how you can contribute with that structure, what new proposals must include, for example, new PR must include _documented code_, _tests for that new feature_, _wiki page update_, …. It’ll save you time explaining developers the things they must fix in every PR.
- **Code structure**: Design first and then code. Think about how you would use that library, the public API you’ll like to find in that library, and then start designing the core components behind that API. Your code must be scalable and reusable, think where the project might have new features in the future, and design it to support them. When we develop for a product we tend to not thing about code reusability and scalability (and we shouldn’t). If we don’t think that way the library will be usable now but it probably won’t after some months _(and you won’t be willing to keep supporting it, you’ll be conscious about not having done the things properly before)_

Lastly and not less important, every Open Source project requires one thing, **compromise**. You’re building a product, you’re building a piece of code other projects depend on. I don’t know about any project that is self maintained. The project will have dependencies with system frameworks, or even with other libraries. Having dependencies mean that if these change the project will need some changes as well. If there’s no compromise with the project it’ll be unusable some months later _(unless you have a community that maintains it)_. An Open Source project **requires invested time**. The most common Open Source reference projects were built with a big community behind them. They started with a person having an idea, that was later supported by more and more developers that spent time to make it better and bigger.

> If you’re thinking about building something Open Source, let me give a recommendation. Try to build something that **your project depends on**. It’s a good way to committed to the library.

#### Recent Open Source project

- **GDAnalytics**: I started that library for a side project I'm working on [Gitdo](http://gitdo.io). The purpose of that library is centralize analytics _(Flurry, Google Analytics, Fabric,..)_ in a single API. It's highly inspired by [**SegmentIO**](https://segment.com/) and [**ARAnalytics**](https://github.com/orta/ARAnalytics)

Hope you have enjoyed the article. If you’re another Open Source geek and you would like to comment any other point you consider is important also when working for these projects, feel free to add a comment or contact me, [pedropb@hey.com][2].

[1]: http://semver.org/ 'Semanting Versioning'
[2]: mailto://pedropb@hey.com
