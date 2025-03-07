---
layout: post
title: 'Building PopcornTime for tvOS'
excerpt: 'I explain in this post the steps I followed to bring the concept of PopcornTime to tvOS and offering torrent video streaming in the last Apple TV device.'
modified: 2015-01-03
tags: [tvos, popcorn time, torrent]
---

With the launch of the last Apple TV, Apple also released an SDK, `tvOS`, offering to the developers the tools to build apps for such device. I have to admit I didn't get any device because I have the previous model and I did not use it at all, but as a developer, I was kind of curious about the idea of porting PopcornTime to tvOS. _Was it possible? Was there any restriction?_.

The idea of PopcornTime was great, it was sad seeing them closing the service after everything they were able to do with a remote team, and building the app for multiple platforms. Desktop apps were actually web apps built on top of NodeJS and the Android app used a torrent client implemented in Javascript, that was executed on the Android device using a NodeJS instance, _quite interesting, isn't it?_

## Torrent Client

My first concern when I started coding the project _(which is available on [this][1])_ was which torrent client I was going to use. I first took a look if there was any Swift client already implemented but there wasn't so I jumped to Objectve-C and C++. I found one, very popular in the community, [libtorrent][2] which is implemented in C++. As you can add C++ in a Xcode project I added de dependency to my project and used an Objetive-C torrent client implemented using libtorrent from this [project].

In order to use it from Swift I just add the import to the bridging header and could access the client from my Swift code. The exposed interface of that client exposes three callbacks:

- The **ready to play** callback notifies when the resource is ready to start playing it. The input parameter of this callback if the URL where the resource is located.
- The **progress** callback that provides information about the already downloaded data and about the buffer state. This callback is very useful in terms of adjusting the player status to the buffer. Synchronizing them to offer the best playing experience.
- The **error** callback, that is called if the download fails for any reason.

When I first tried the torrent client I added some console logs in these callbacks and sent a torrent to be downloaded. I didn't get any log printed and I then decided to go to sleep because I was a bit tired. 30 min later, I woke up and saw the log full of printed messages, I shout out, yay! it works!. I then added a `VideoPlayerViewController` and tried to reproduce the provided `NSURL` where the resource was located.

Guess what? It worked!

```swift
PTTorrentStreamer.sharedStreamer().startStreamingFromFileOrMagnetLink("magnet-link", progress: { (status) -\> Void in
   print("Status: \(status)")
}, readyToPlay: { (url) -\> Void in
   print("Ready to play \(url)")
}) { (error) -\> Void in
   print("Error: \(error)")
}
```

## Torrents API, YTS

For the previous example I hardcoded the magnet-link but I wanted the real app to get the data from an API and present the list of movies using a `tvOS` user-friendly layout, with covers, movies information, ... After some research I found out, [YTS API][3], tried its multiple endpoints and they worked, they offered, list of movies, filtering, and also recommendations. It was perfect!

I decided then to architecture the core of the app in a framework, `PopcornTimeKit` dependency of the main app target. I implemented the `Movie` and `Torrent` models that were going to be the mapping result of API responses and also the HTTP requests and repositories to access these resources from the API. I used for that purpose, a library, I implemented called [HTTPCommander][4] that implements base HTTP Commands that expose its execution using reactive observables _(I didn't mention but decided that the public interface of PopcornTimeKit was going to be reactive with [RxSwift][5])_.

With the requests ready for accessing the API and getting the data and errors mapped, the `PopcornTimeKit` was ready to be used from the app. The app was not going to have any kind of persistence, data would be fetched and presented as the user navigated through the interface as the desktop client did.

## 200 Mb Storage Limit

When finding developers that helped me to test the app //[TODO][6]// reported that there was a limit of 200 Mb when persisting data in the Apple TV. :shit: I thought. How could I solve it? Multiple ideas came to my mind and I am still trying to figure out which one is the best:

- **Client is on iOS/OSX and tvOS is an AirPlay client**: Move the PopcornTime torrent client to another platform that doesn’t have the storage restriction and use a protocol like AirPlay to share the content with the AppleTV. I am not sure at all with this solution since it means we’re practically moving all the responsibility to the iOS/OSX app and have the tvOS app as an idle app.
- **Control the persisted data beca** Someone with more experience in video files might think I’m a lot crazy but I’ve to still check it. My original idea was implementing a controller that knows about the _download status_, _reproduction status_, and _file size_. And with all these information trim unneeded bytes at the beginning of the file ensuring the file doesn’t go over 200 Mb ever.

Do you have any other idea, create an issue on the repository or write me an email, [pedropb@hey.com][7]

## Layout

//TODO

- List
- Detail View

## MobileVLCKit

The `AVFoundation` component `AVPlayer` works but it does not allow to embed subtitles or read formats like `.mkv`. I had a look at `MobileVLCKit` which recently gave support to _tvOS_ but I couldn’t get it compiling so I opened an issue explaining the problem I was having. I hope they can fix it soon.

## What’s next?

I’ve given the first steps, and seen that it’s possible to have PopcornTime working on our AppleTV and enjoy a better catalog than the one other companies offer. **I’m not going to try to find any distribution channel, even if there was one**. I like learning and creating, projects like PopcornTime are perfect to experiment with new protocols formats, platforms… If you are a SWift/Objective-C developer and you would like to help with the project this project is also yours. I’ll be pleased to have you onboard and go with it together.

## TODO

- Add a reference to the user that reported the 200 Mb limit
- Add a link to MobileVLCKit
- Add a link to the MobileVLCKit issuef

[1]: https://github.com/pepicrft/popcorntimetv
[2]: link
[3]: link
[4]: https://github.com/swiftreactive/httpcommander
[5]: https://github.com/reactivex/rxswift
[6]: TODO
[7]: mailto://pedropb@hey.com
