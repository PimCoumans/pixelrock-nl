---
layout: post
title: Hello Again, OK Video
# date: 2024-07-25 00:00:24 +0200
summary: OK Video has been rewritten and stuff
---

{% include image.html url="/assets/ok-video/okvideo-header.png" %}

Some exciting news: OK Video — my video app you should definitely try — has received a huge update with a bunch of new features! It’s literally a completely new app and I couldn’t be more proud of the result.

Read on if you want to hear more about all this, but of course you can [check it out yourself](https://okvideo.app/download) right now!

# A Little Backstory

OK Video [started out]({% post_url 2019-03-27-making-ok-video %}) as a fun hobby project that got more serious along the way. The initial goal was — and still is — to make an easy hold-to-record camera app that just allows you to create unlimited video sequences and getting out of your face as soon as possible.

Starting with a very, VERY basic app I slowly added more features in my spare time. As with most side projects that get worked on intermittently, along the way the project gained significant technical debt and its foundation ended up being held together by ever increasing layers of duct tape. I wanted to add new features, but working on this project no longer sparked joy.

The sensible solution would be to take some time and address the main pain points in the app’s codebase — slowly restructuring and modernizing the app in the process — but that didn’t sound like fun at all. I just wanted to start over and build the _whole app_ again, from scratch. That won’t take too long, right?

_Narrater: it did_

{% include image.html url="/assets/ok-video/rewriting-okvideo.jpg" alt="iMessage conversation from February 2023, stating I'm rewriting OK Video" %}

# Introducing: The New OK Video

Almost a year-and-a-half later, it’s done. OK Video version 10.0. Painstakingly rebuilt, piece by piece, adding and improving many features in the process. Just this update alone is officially my biggest solo project to date. I’m extremely happy with result and I sincerely hope you will like it too.

Please allow me to take you through all the new features.

## Cleaner UI, Chunky Buttons, Colorful Menus

{% include image.html url="/assets/ok-video/okvideo-delete-panel.png" alt="Screenshot of OK Video showing the confirmation panel to delete all clips" caption="Colorful, chuncky, just the right amount of whimsy" %}

I've come to really enjoy whimsical, playful interfaces. App designers can learn a lot from the playfulness of UIs shown in most Nintendo games. Considering OK Video isn’t a very serious app, why should its dialogs be? There’s also a few easter eggs hidden in the app, have you found any yet?

## Improved Editor

{% include image.html url="/assets/ok-video/okvideo-editor.png" alt="Screenshot of OK Video showing the improved editor and all its new features" caption="The editor received some much requested editing features" %}

It’s hard to imagine OK Video existed for over three years without any editing functionality besides deleting the last clip. The dedicated editor that was released in December 2020 started with just reordering and deleting clips.

Luckily editing in OK Video is now much more full-featured. Firstly, when opening the editor the video player subtly scales down to make room for the timeline that pops in from the bottom. Each clip in the timeline shows multiple thumbnails — unbelievable, I know.

All the actions you can do with a selected clip are neatly displayed at the bottom, with the most requested feature sitting proudly in the center: trimming!

{% include image.html url="/assets/ok-video/okvideo-trimming.jpg" alt="Cropped screenshot of the editor’s timeline showing a clip in the trimming state" caption="Trimming happens right in the timeline with an expanded view of the selected clip" %}

Yes you read that right, you can now change the timing of your clips. Just drag the left or right handle while in the trimming mode to change the start and end times respectively. Combined with the duplicate action it kinda, sorta, gives you the option to split clips.

## Zoom Control

{% include image.html url="/assets/ok-video/okvideo-zoom.png" alt="Screenshot of OK Video showing refreshed camera interface with the new zoom control" caption="That large zoom control at the bottom lets you quickly change zoom levels" %}

With this update it’s finally possible to zoom in before starting a recording. The zoom levels are neatly displayed in the new Zoom Control, allowing you to quickly toggle between lenses. You can swipe horizontally to gradually step between each zoom level, and even drag past the highest level to zoom in even further.

{% include video.html url="/assets/ok-video/okvideo-zoom-control.mp4" caption="Cropped screen recording of the new Zoom Control in action (click to play)" %}

## Self Timer

The Self Timer feature lets you record a clip without having to keep hold of the screen, giving you a hands-free mode of sorts. Just — safely — put your phone down somewhere, make sure its pointed in the right direction and focused on the right point and select the cute little timer icon in the main menu. It’ll keep recording until you tap the screen so make sure you don’t leave it going for too long!

## Onboarding Tutorial

{% include image.html url="/assets/ok-video/okvideo-tutorial.png" alt="Screenshot of the first step in the new tutorial" %}

When launching OK Video for the very first time, new users are greeted with a friendly step-by-step tutorial. This tutorial should help them quickly get the hang of the main features: recording, previewing, deleting the last clip and sharing a project.

If you already had the app installed, you can see it in action by selecting ‘Show Tutorial Again’ in Settings.

## Widgets

{% include image.html url="/assets/ok-video/okvideo-widgets.png" alt="Screenshot of an iPhone’s homescreen featuring multiple OK Video widgets providing quick access to its projects" caption="Widgets! Fill your screen with all of them!" %}

Now you can go straight to one of your OK Video projects right from your homescreen. This is a great way to always see which projects you’re still working on and making sure you never record to the wrong one. There’s multiple sizes available, where the smallest gives you access to your first four projects.

{% include image.html url="/assets/ok-video/okvideo-lockscreen.jpg" alt="Screenshot of an iPhone’s locks screen with a small OK Video icon that opens the app" caption="You can even open OK Video from your lock screen!" %}

An even smallest widget can be added your lock screen. It’s just the app’s logo and tapping it allows you to immediately opens the app from wherever you are.

## Anything Else?

Here’s a list of all the other new stuff worth mentioning:

- **Improved export flow:** Featuring options to share or save to photos after exporting.
- **Pro Settings:** More fine-grained settings for folks with specific wants and needs.
- **Unlimited Undo and Redo:** Better support for system gestures — deleted files are removed when closing the project.
- **Ghost Mode with First Frame:** Most convenient while making a timelapse, align your shots with the very first frame — instead of the last — so subsequent shots never drift.
- **Focus Mode** allows you to keep tapping to find the right focus instead of dismissing after a single tap
- **Share Single Clip:** Long-press on a clip in the Editor and tap ‘Share’ to manually share just that clip.
- **Per-Project Settings** are remembered, like camera orientation, Flash, and Ghost mode
- **Gratuitous Purchase Animations** added for the ‘Remove Watermark’ and ‘Unlock Editor’ in-app purchase (will write about these in the near future!)

# Closing Thoughts

That was quite the update! Thanks for reading all this! If you want to see more, make sure to check out the official website, [okvideo.app](https://okvideo.app), and feel free to share it with anyone! The update is available right now and anybody with an iPhone can download it using [this link](https://okvideo.app/download).

Some of you iOS developers probably are wondering if this brand-new app is written in SwiftUI and I’m proud to announce: No! It’s all still 100% pure, old-fashioned, homegrown UIKit.

I’ve taken some cues from SwiftUI though and came up with an MVVM-type architecture built upon a reactive framework. What framework? My own of course: [DidUpdate](https://github.com/PimCoumans/DidUpdate).

All non-trivial animations are driven my animation framework [AnimationPlanner](https://github.com/PimCoumans/AnimationPlanner) which I initially created to [animate the Projects unlock animation]({% post_url 2022-06-07-plan-your-animations %}).
