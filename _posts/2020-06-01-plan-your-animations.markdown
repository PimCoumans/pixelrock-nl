---
layout: post
title: "Chain multiple UIView animations, the easy way"
date: 2022-06-07 00:00:00 +0200
summary: How to perform multiple UIView animations in sequence with AnimationPlanner
---

Superfluous animations, I love them.

For [OK Video](https://okvideo.app)’s latest update I wanted to create some pretty involved animations and when I starting building them out I had a thought -- a though that usually ends in a lot a frustration and cursing:

> This should be made easier..

Every time this thought pops into my head, I end up diving deep into a rabbit hole, getting lost in details about stuff I‘d never heard about before. This time I allowed myself to get distracted because the idea of making a little animation library sounded like too much fun to pass up on. Here‘s the animation I end up building and for which I definitely totally had to create a whole animation library _(hit the play button in the center)_:

{% include video.html url="/assets/ok-video/unlock-projects.mov" caption="Unlock animation of projects after completing in-app purchase" %}

## Enter: AnimationPlanner

After shipping the Projects update to OK Video I went back to revisit my library and give it some well-deserved attention. I was [gently nudged](https://twitter.com/harshil/status/1516421012367323140) to try an approach using Swift‘s result builders (like you‘d use for building views in SwiftUI) and I just went for it. Two excruciating but fun weeks layer, creating a basic sequence animation in code now looks as simple as:

```swift
AnimationPlanner.plan {
    Animate(duration: 0.32, timingFunction: .quintOut) {
        view.alpha = 1
        view.center.y = self.view.bounds.midY
    }
    Wait(0.2)
    Animate(duration: 0.32) {
        view.transform = CGAffineTransform(scaleX: 2, y: 2)
        view.layer.cornerRadius = 40
        view.backgroundColor = .systemRed
    }.timingFunction(.quintOut)
    Wait(0.2)
    AnimateSpring(duration: 0.25, dampingRatio: 0.52) {
        view.backgroundColor = .systemBlue
        view.layer.cornerRadius = 0
        view.transform = .identity
    }
    Wait(0.58)
    Animate(duration: 0.2) {
        view.alpha = 0
        view.transform = .identity
        view.frame.origin.y = self.view.bounds.maxY
    }.timingFunction(.circIn)
}.onComplete { finished in
    view.removeFromSuperview()
}
```

The nice-looking code above results in the following animation sequence. Yes, really.

![Animation planner sample animation](https://raw.githubusercontent.com/PimCoumans/AnimationPlanner/main/Assets/sample-app.gif){: style="width: 293px" }

## How to create your sequence animation

First of all, add `AnimationPlanner` to your project. With the Swift Package manager it's as easy as adding a package and searching for `https://github.com/PimCoumans/AnimationPlanner`. Or add the following to your package‘s dependencies:
`.package(name: "AnimationPlanner", url: "https://github.com/PimCoumans/AnimationPlanner.git", .branch("main"))`. Then add `@import AnimationPlanner` to the top of the file where you want to make glorious animations.

Wherever you want to start your animation sequence, start with calling the builder function:

```swift
AnimationPlanner.plan {
    // Your animations here
}
```

Then from within that block, simply start adding your animations. The simplest are `Animate()` and `Wait()`.

```swift
AnimationPlanner.plan {
    Animate(duration: 0.32, timingFunction: .quintOut) {
        view.alpha = 1
        view.center.y = self.view.bounds.midY
    }
    Wait(0.2)
}
```

This creates an animation that runs for 0.32 seconds using a custom timing function (more on that later). Within the animation‘s trailing closure the `view` object‘s `alpha` is set to `1` and its vertical position is centered in the screen. The changes applied in this closure will actually be performed from a `UIView.animate { }` call, so Core Animation will take care of all the necessary optimizations. After this animation. the sequence will paus for 0.2 seconds before completing the animation.

To get notified when the sequence finishes, append the following call to your animation plan:

```swift
.onComplete { finished in
    print("We‘re done here!")
}
```

## Fancy spring animations

To create an animation with spring paramaters (utilizing `UIView.animate(... usingSpringWithDamping: initialSpringVelocity:)`), you can replace your `Animate` struct with `AnimateSpring` and set its `dampingRatio` and the optionally an `initialVelocity`. You can also use an modifier function to add spring interpolating to an existing animation:

```swift
Animate(duration: 0.5) {
    view.transform = CGAffineTransform(scaleX: 2, y: 2)
}.spring(damping: 0.68)
```

## Running multiple animations at the same time

By adding a `Group { }` in your sequence or starting of with a group right away through `AnimationPlanner.group`, you can create a bunch of animations that should happen simultaneously. All animations added to a group will start at the same time, but grouped animations are also allowed to start after a specific delay:

```swift
AnimationPlanner.plan {
    Group {
        AnimateDelayed(delay: 0.1, duration: 0.5) {
            firstView.transform = .identity
        }.timingFunction(.quintOut)

        Animate(duration: 0.5) {
            secondView.transform = .identity
        }
        .timingFunction(.quintOut)
        .delayed(0.25)
    }
}
```

In the code shown above, two delayed animations are created, both resetting a transform on

## Stop running animations

`AnimationPlanner.plan` returns a `RunningSequence` object that primarily should be used for setting a completion handler. It also provides a way to cancel any running animations when necessary:

```swift
let sequence = AnimationPlanner.plan {
    for _ in 0...1000 {
        Animate(duration: 1) { view.alpha = 0 }
        Animate(duration: 1) { view.alpha = 1 }
    }
}

// Okay that's enough
sequence.stopAnimations()
```

## Can I use AnimationPlanner right now?

You‘re in luck, after much work v1.0 is out and working like a charm. I‘ve updated all parts in OK Video where I needed to animate more than one thing and it‘s been a very smooth transition

![Animation Planner logo](https://github.com/PimCoumans/AnimationPlanner/raw/main/Assets/AnimationPlanner.png)

[github.com/PimCoumans/AnimationPlanner](https://github.com/PimCoumans/AnimationPlanner)
