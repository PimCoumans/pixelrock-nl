---
layout: post
title:  "Chain multiple UIView animations, the easy way"
date:   2022-06-07 00:00:00 +0200
summary: How to perform multiple UIView animations in sequence with AnimationPlanner
---

Superfluous animations, I love them.

For [OK Video](https://okvideo.app)’s latest update I wanted to create some pretty involved animations any while starting on building them I had a thought -- a though that usually ends in a lot a cursing:

> This should be made easier...

Every time this thought pops into my head, I end up diving deep into a rabbit hole, getting lost in details about stuff I‘d never heard about before. This time I allowed myself to get distracted because the idea of making a little animation library sounded like too much fun to pass up on. Here‘s the end-result of what I had to create a whole animation libary for.

{% include video.html url="/assets/ok-video/unlock-projects.mov" caption="Unlock animation of projects after completing in-app purchase" %}

## Enter: AnimationPlanner

![Animation Planner logo](https://github.com/PimCoumans/AnimationPlanner/raw/main/Assets/AnimationPlanner.png)

- spoiler, you can find it over here: [AnimationPlanner](https://github.com/PimCoumans/AnimationPlanner)


After shipping the update to OK Video I went back to revisit my library and give it some well-deserved attention. I was [gently nudged](https://twitter.com/harshil/status/1516421012367323140) to try an approach using Swift‘s result builders and I just went for it. Two excrusiating but fun weeks layer, creating a little sequence animation in code now looks as simple as:

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
    AnimateSpring(duration: 0.25, damping: 0.52) {
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
} completion: { finished in
    view.removeFromSuperview()
}
```

The nice-looking code above results in the following animation sequence. Yes, really.

![Animation planner sample animation](https://raw.githubusercontent.com/PimCoumans/AnimationPlanner/main/Assets/sample-app.gif)
<!-- <p align="center">
    <img src="https://raw.githubusercontent.com/PimCoumans/AnimationPlanner/main/Assets/sample-app.gif" width="293" height="443" />
</p> -->
