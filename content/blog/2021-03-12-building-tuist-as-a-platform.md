---
layout: post
title: 'Building Tuist as a platform'
categories: ['platform', 'tuist', 'open source']
---

Having seen Shopify acting as an e-commerce platform that developers can extend made me think whether the same idea would be applicable to Tuist.
What if instead of us trying to codify all different workflows and configurations,
we gave developers an API to do it?
Damn, it's so good.
I started thinking about it thoroughly, and I think I have a good idea around how that could be.

First, I think **Tuist's focus should be on the project graph,
the generation of projects,
and the build and test commands**.
We've invested four years into building a solid graph that we can optimize and turn into Xcode projects.
Developers love that!
They no longer have to think about linking or embedding build phases.
Tuist makes them an implementation detail and knows what changes can be applied to the resulting Xcode project to be fast to index and compile.

**What APIs can we expose?** The two that I think would be very valuable are `Setup.swift` and `Tasks.swift`.
The first already exists.
Developers can define how to configure an environment before interacting with the project.
However,
I'd change the approach to be imperative instead of declarative.
Basically,
instead of Tuist parsing the file and then translating the steps into system commands,
we'd run the `Setup.swift` file directly as if it was a command line tool.
`Tasks.swift` is not yet implemented but it'd allow developers describe their workflows in the same way they currently do with Fastlane.
The difference is that Tuist'd provide them with information about their projects, like the dependency graph.
How cool is that?
Let me dump some pseudo-code below:

```swift
import TuistAutomation

let tasks = [
  .task(name: "swifltint") { tuist in
    let graph = tuist.graph()
    let sources = graph.sources()
    tuist.system("swiftlint", ....)
  }
]
```

And this would align with the work that we are doing with [plugins](https://tuist.io/docs/plugins/using-plugins/).
Developers would be able to extract their tasks and up commands and wrap them in a plugin that they share across projects and with the community.
Same as if they were sharing Fastlane lanes ❤️.

It's exciting seeing everything that project generation enables.
As I've said a few times,
project generation is a means in Tuist to help developers with the challenges at scale.
Using project generation for only getting rid of git conflicts will not help you with a plenty of problems that you'll see down the road.
