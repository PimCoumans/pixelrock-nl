---
layout: post
title: 'The New OK Video — More Editing Features'
date: 2024-07-01 00:00:24 +0200
summary: OK Video has been completely rewritten and gotten so much more capable
---

{% include image.html url="/assets/ok-video/okvideo-header.png" %}

Just a few months after celebrating its 7th birthday, [OK Video](https://okvideo.app) — the free little video app you should definitely try — has received the biggest update yet. Not only introducing a whole heap of new editing features, overall the app should now work much smoother and feel more complete.

Everything you know and love is still there, recording your videos just by holding the screen is just as easy as it ever was. But now, you know, better!

Read on if you want to hear more about all this, but of course you can [check it out yourself](https://okvideo.app/download) right now!

### Overview

- [Backstory](#backstory)
- [What’s New](#whatsnew)
- [UI Update](#cleaner-ui)
- [Evolved Editor](#evolved-editor)
- [Better Playback](#playback-control)
- [Zoom Control](#zoom-control)
- [Self Timer](#self-timer)
- [Widgets](#widgets)
- [Onboarding Tutorial](#tutorial)
- [More Changes](#more)
- [Closing Thoughts](#closing-thoughts)

# A Little Backstory {#backstory}

OK Video [started out]({% post_url 2019-03-27-making-ok-video %}) as a fun hobby project that got more serious along the way. The initial goal was — and still is — to make an easy hold-to-record camera app that just allows you to create unlimited video sequences and never nagging the user with ads, popups, subscriptions or other predatory practices.

Starting with a very, VERY basic app in 2017 I slowly added more features in my spare time. Along the way the project got a dated and its foundation was held together by ever increasing layers of duct tape — metaphorically speaking of course. I wanted to improve the app and build new features, but working on this project became cumbersome and no longer sparked joy.

The sensible solution would be to take some time to slowly and gradually restructure and modernizing the app component by component — but that didn’t sound like fun at all. I just wanted to start over and build the _whole app_ again, from scratch. That won’t take too long, right?

_Narrater: it did_

{% include image.html url="/assets/ok-video/rewriting-okvideo.jpg" alt="iMessage conversation from February 2023, stating I'm rewriting OK Video" %}

# What’s New? _(everything)_ {#whatsnew}

A year-and-a-half later the full rewrite of OK Video was done. Coincidentally this update has a nice round version number: OK Video version 10. Painstakingly rebuilt, piece by piece, adding and improving many features in the process. I couldn’t be happier with the end result and I sincerely hope you’ll like it too.

Allow me to take you through all the important new stuff.

## Cleaner UI, Chunky Buttons, Colorful Menus {#cleaner-ui}

{% include image.html url="/assets/ok-video/okvideo-delete-panel.png" alt="Screenshot of OK Video showing the confirmation panel to delete all clips" caption="Colorful, chuncky, just the right amount of whimsy" %}

The default, generic iOS controls and alerts are out, they no longer felt right for this app. I’ve come to really enjoy whimsical, playful interfaces like the UIs shown in most Nintendo games. Considering OK Video isn’t a very serious app, why should its dialogs be?

_There’s also a few easter eggs hidden in the app, have you found any yet?_

## Evolved Editor {#evolved-editor}

{% include image.html url="/assets/ok-video/okvideo-editor.png" alt="Screenshot of OK Video showing the improved editor and all its new features" caption="The editor received some much requested editing features" %}

It’s hard to imagine OK Video existed for over three years without any editing functionality besides deleting the last clip. The dedicated editor that was released back in December of 2020 featured just reordering and deleting clips.

Luckily editing in OK Video is now much more full-featured. Firstly, the video player subtly scales down when opening the editor to make room for the timeline. Each clip in the timeline now shows multiple thumbnails — unbelievable, I know.

All the actions you can do with a selected clip are neatly displayed at the bottom, with the most requested feature sitting proudly in the middle: trimming!

{% include image.html url="/assets/ok-video/okvideo-trimming.jpg" alt="Cropped screenshot of the editor’s timeline showing a clip in the trimming state" caption="Trimming happens right in the timeline with an expanded view of the selected clip" %}

Yes you read that right: you can now change the timing of your clips. Just drag the left or right handle while in the trimming mode to change the start and end times respectively. Combined with the duplicate action it kinda, sorta, gives you the option to split clips.

## Better Playback {#playback-control}

Previewing your project in OK Video has been pretty bare bones, just allowing you to start or stop playback of the whole video or just the last two clips. With this update, playback has been improved with these new features:

- **Auto-resuming playback:** After interruptions — e.g. app backgrounded, getting an important notification — your preview picks up where it left off instead of stopping the preview altogether.
- **Swipe-to-Seek:** Horizontally swipe the screen during playback to quickly seek through your project.
- **Play next/previous clip:** Tap the left or right edge of the screen to immediately seek to the previous or next clip.

## Zoom Control {#zoom-control}

{% include image.html url="/assets/ok-video/okvideo-zoom.png" alt="Screenshot of OK Video showing refreshed camera interface with the new zoom control" caption="That large zoom control at the bottom lets you quickly change zoom levels" %}

Before this update zooming was only possible while recording. While your finger was pressed on the screen, dragging up or down zooms in or out respectively. Then you had to delete the unwanted clip directly after.

With this update it’s finally possible to zoom in without recording. The new Zoom Control neatly displays the expected zoom levels, allowing you to quickly toggle between these positions. You can swipe horizontally to gradually step between each zoom level, and even drag past the highest level to zoom in even further.

{% include video.html url="/assets/ok-video/okvideo-zoom-control.mp4" caption="Cropped screen recording of the new Zoom Control in action (click to play)" %}

## Self Timer {#self-timer}

The Self Timer feature is probably also pretty self-explanatory: it lets you record a clip after some delay without having to hold the screen, giving you a hands-free mode of sorts. Just — safely — put your phone down somewhere, make sure it’s oriented and focused right, and select the cute little timer icon in the main menu. It’ll keep recording until you tap the screen so make sure you don’t leave it going for too long!

## Widgets! {#widgets}

{% include image.html url="/assets/ok-video/okvideo-widgets.png" alt="Screenshot of an iPhone’s homescreen featuring multiple OK Video widgets providing quick access to its projects" caption="Widgets! Fill your screen with all of them!" %}

Now you can go straight to one of your OK Video projects right from your homescreen. This is a great way to always see which projects you’re still working on and making sure you never record to the wrong one. There’s multiple sizes available, where the smallest gives you access to your first four projects.

{% include image.html url="/assets/ok-video/okvideo-lockscreen.jpg" alt="Screenshot of an iPhone’s locks screen with a small OK Video icon that opens the app" caption="You can even open OK Video from your lock screen!" %}

An even smaller widget can be added your lock screen. It’s just the app’s logo and tapping it allows you to immediately opens the app from wherever you are.

## Onboarding Tutorial {#tutorial}

{% include image.html url="/assets/ok-video/okvideo-tutorial.png" alt="Screenshot of the first step in the new tutorial" %}

When launching OK Video for the very first time, new users are greeted with a friendly step-by-step tutorial. This tutorial should help them quickly get the hang of the main features: recording, previewing, deleting the last clip and sharing a project.

If you already had the app installed, you can see it in action by selecting ‘Show Tutorial Again’ in Settings.

## Anything Else? {#more}

Here’s a list of all the other new stuff worth mentioning:

- **Improved export flow:** Featuring options to share or save to photos after exporting.
- **Pro Settings:** More fine-grained settings for folks with specific wants and needs.
- **Unlimited Undo and Redo:** Now using the system undo gesture, this feature adds support for unlimited undos and redos, instead of just undoing the last deletion.
- **Ghost Mode with First Frame:** Most convenient while making a timelapse, align your shots with the very first frame of your project — instead of the last — so subsequent shots never drift.
- **Focus Mode:** Instead of being dismissed after a single tap, it now allows you to keep tapping to find the right focus and exposure point.
- **Share Single Clip:** Long-press on a clip in the Editor and tap ‘Share’ to manually share just that clip.
- **Per-Project Settings** are remembered, like camera orientation, Flash, and Ghost mode.
- **Gratuitous Purchase Animations:** Celebrations shown after purchasing the ‘Remove Watermark’ and ‘Unlock Editor’ in-app purchases (will write about these in the near future!)
- **Revamped Settings Screen** with a new About page and the option to contact me through an online feedback form.

# Closing Thoughts {#closing-thoughts}

That was quite the update! Thanks for reading all this! If you want to see more, make sure to check out the official website, [okvideo.app](https://okvideo.app), and feel free to share it with anyone! The update is available right now and anybody with an iPhone can download it using [this link](https://okvideo.app/download).

Some of you iOS developers probably are wondering if this brand-new app is written in SwiftUI and I’m proud to announce: No! It’s all still 100% pure, old-fashioned, homegrown UIKit.

I’ve taken some cues from SwiftUI though and came up with an MVVM-like architecture built upon a reactive framework. What framework? My own of course: [DidUpdate](https://github.com/PimCoumans/DidUpdate).

All non-trivial animations are driven my animation framework [AnimationPlanner](https://github.com/PimCoumans/AnimationPlanner) which I initially created to [animate the Projects unlock animation]({% post_url 2022-06-07-plan-your-animations %}).
