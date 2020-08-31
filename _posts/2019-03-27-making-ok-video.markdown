---
layout: post
title:  "Making OK Video(s)"
date:   2019-03-27 16:41:24 +0200
summary: Where I go into the challenges of creating a snappy vine-style recording app
---
>**Disclaimer:** This article was written as a draft for a talk about some of the technology involved with making OK Video. It's far from complete and hopefully I will get around to finishing it at some point.

## How it began
Early 2017, I saw a tweet by Tom DesLongchamp that peaked my interest. You should look him up, he makes amazing stuff, [tomdeslongchamp.com](http://tomdeslongchamp.com) and I'm a fan of his since Vine (RIP).

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Is there an app that exists where you can record vertical video Vine-style (hold down to record). I want to make video sequences quickly.</p>&mdash; Tom DesLongchamp (@tomthinks) <a href="https://twitter.com/tomthinks/status/829102015628193792?ref_src=twsrc%5Etfw">February 7, 2017</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">If you make that app for me, I&#39;ll be really happy. And you&#39;ll be happy too.</p>&mdash; Tom DesLongchamp (@tomthinks) <a href="https://twitter.com/tomthinks/status/829102305676963840?ref_src=twsrc%5Etfw">February 7, 2017</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 

And I responsed with
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">if this app genuinely doesn&#39;t exist, would you want me (a genuine real life iOS developer) to prototype something for you?</p>&mdash; Pim (@pimcoumans) <a href="https://twitter.com/pimcoumans/status/829254099409440772?ref_src=twsrc%5Etfw">February 8, 2017</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 

### The idea

Vine-style video shooting with as little effort as possible. Then save to camera roll to send it to whatever your heart's desires. Hold the screen to start recording, release to stop. Repeat for each subsequent shot and finish your project with one button.

*How hard could it be?* `¯\_(ツ)_/¯`

## Challenge 1

The prototype was literally built in a day. Luckily the `AVFoundation` framework does most of the heavy lifting for you. In short, it comes down to two steps:

- Create an `AVCaptureMovieFileOutput` and tell it to start recording to a specific file
- When done, tell it to stop.

One downside: both these operations aren't happening instantly. The file output object will notify you it has started recording a little after you told it to start, and the same goes for stopping recording.

### Problem

What if the screen was already released before the recording actually has started? What if the videographer wants to rapidly create short clips and the capture mechanism can't keep up?

### Solution

Keep track whether the app should be recording with a `shouldRecord` variable (for when the finger is touching the screen) and whether the app is actually recording with `isRecording` variable. When the recording has actually began, `isRecording` is set to `true`. Then `shouldRecord` is checked to see if recording should stop again. The same happens when we get notified that the recording has stopped: `isRecording` is set to `false`.

``` md
Touch:       [down]             [up]            |   [down] [up]
Recorder:           [started]           [ended] |               [started]   [ended]
```

For a while I was messing with a 'command buffer' that stores each start- and stop command, but that was a terrible idea. 🚮

## Challenge 2

Using `AVCaptureMovieFileOutput` is far out the easiest way to record video, and the fist version of OK Video shipped using this magnificent tool. But it wasn't good enough. My goal was to have a recording experience on par with Vine, which was way more responsive and allowed users to capture short bursts in quick succession. Behind the scenes there was too much going on in `AVCaptureMovieFileOutput` I had no control over, so I had to dig a little bit deeper and go down one level of abstraction.

Enter: `AVCaptureDataOutput` and `AVAssetWriter`.

My guess is that `AVCaptureMovieFileOutput` handles this for you, but to get more control over the nitty details, you have to use these classes yourself.

To get this set up, you create two outputs -- one for video and one for audio -- and configure them with your ideal encoding configuration. Whenever you want to record, you create an instance of `AVAssetWritter`, and send the output of each `AVCaptureDataOutput` over to the writer. When you're done, you tell it to finish writing and you've created your video.

Each output is a never ending stream of buffer objects with video or audio samples which you tap into whenever you want to record. Like a faucets you hold a bucket under whenever you want to collect some water.

### Problem

Now, these streams aren't very predictable. Each sample has its own timestamp and you don't know when you're getting what. Ideally, the audio and video samples come in around the same time, so they're not out of sync, but this is not always the case. When you start writing to a video file and your audio samples arrive later then your video samples, you're missing audio in the beginning of your video. When your video samples are late, your video starts with black (empty) frames.

When writing your data to a video, you need to tell it at what timestamp you want to start.

### Solution

Decide on one stream (video or audio) as a base, keep track of when samples of other track are also available. I'm using the video track as my base, and decide when to start or stop recording on each video frame that comes in. The next audio sample that comes in after recording has started, you note the timestamp of that sample. The difference between the timestamp when recording has started and the timestamp of the audio sample is the amount of time audio is potentially missing in your video. Keeping track of the latest timestamp of each audio track after recording has started, allows you to know how many audio is potentially missing at the end of your video.

``` md
video:   [frame][frame][frame][frame][frame][frame][frame]
audio:         [sample][sample][sample][sample][sample]
```

The offsets I store in the project file for each clip so when placing the videos into one composition, I know when to start each clip.

## Challenge 3

We're not done yet! We now have a bunch of videos that need to be stitched together. An MVP approach would be to just place these clip with directly in sequence. Event this isn't as easy as it sounds:

- Create an `AVComposition`
- Create two tracks for video and audio respectively
- Loop through all the clips and get the tracks for both video and audio
- Place the clip's video data at the right point in the composition's video track, do the same for the audio
- Render out the composition using an `AVAssetExportSession`

Remember when creating the clips, I'm noting the relative start and end point of the clips audio data? When starting the recording session at the first video frame, actual video data when the clip starts is ensured. The audio data that comes in after could be from a different time, be it earlier or later than the first video frame. If you ignore these times, gaps can appear in audio, resulting in a subpar exported video.

``` md
    ----|-------- video data ----------- |
        |------------ audio data --------|----
        |                                |
        |         smallest range         |
```

A naive solution is to use the smallest range of both video and audio data. I've found that not cutting at frame boundaries -- the exact interval of frames in video, or frames per second -- will result in uneven videos with incorrectly reported fps. So it's better to round everything to whole frames, making sure all cuts happen exactly between frames.

``` md
    [video][video][video][video][video][video]
           [audio][audio][audio][audio][audio][audio]
           |                                 |
           |       smallest rounded range    |
```

### Problem

As any audio export would no, just slapping two set of audio data together can result in unwanted distortions. As the waveforms of audio suddenly get interrupted or changed, a click or pop can be heard.

``` swift
      ____    | __                 ___
    /      \  |    \             /
  /          \|      \         /
/             |        \ ___ /
```

To transition smoothly from one audio clip to the next, the audio data needs to be interpolated. Luckily this can be done with a crossfade: fading out on a clip while gradually fading in the next. To have a good enough transition between audio clips, you need at least 10 milliseconds of crossfade, to round that up to more workable number, that's half a frame with 30 frames per seconds.

Each clip needs to overlap a bit to allow for half a frame of crossfade on each sides, while having enough content to show an actual frame.

### Solution

Rounding up to have enough data to work with, and extra frame on each sides is needed. When the recorder keeps recording until at least three frames of usable content is recorded you can ensure that each clips can crossfade into each other.

For every other clip, a different audio track should be used so audio can actually overlap. For all even clips you use audio track A, for the odd clips you use audio track B.

For a crossfade for half a frame, the audio data needs to extend at least a quarter frame on each sides. To account for any misalignments the audio should extent for double that, so 1/2 frame. That means that audio overlaps for a full frame.

For every clip I add a `volume ramp` from `0` to `1` during the beginning audio overlap and a ramp from `1` to `0` for the ending audio overlap. If everything aligns well, a clip should ramp its audio down exactly when the next clip ramps its audio up.

``` md
[   frame   ][   frame   ][   frame   ][   frame   ]
[  video 1  ][  video 1  ][  video 2  ][  video 2  ]

[  audio 1 ------------------- ]
                       [ramp]

                   [  audio 2 -------------------- ]
                       [ramp]
```