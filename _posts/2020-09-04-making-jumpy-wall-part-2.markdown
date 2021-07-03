---
layout: post
title:  "Verby Nouns: a Jumpy Wall Story - Part 2: Dynamics beats and synths"
summary: Where I go into detail about the dynamic music in the game with variable bpm and a real-time synth to boot.
date:   2020-09-04 10:00:00 +0200
---

>This the is second part in my series on making [Jumpy Wall](https://jumpywall.com){:target="_blank"}, an endless wall jumper for [iOS](https://itunes.apple.com/us/app/jumpy-wall-endless-wall-jumper/id986693325?l=en&mt=8){:target="_blank"} and [Android](https://play.google.com/store/apps/details?id=nl.pixelrock.jumpywall&utm_source=jumpywall.com&utm_campaign=website){:target="_blank"}. In this part I go into detail about the dynamic music in the game, where the tempo goes up as the characters goes higher in the game. Also you'll read about the basic real-time synth that creates the bass and melody.
>
>- [Part 1]({% post_url 2020-09-03-making-jumpy-wall-part-1 %}) How the game came to be

## The higher you get, the faster the music

As if the game's visuals aren't intense enough, or the fact that moving obstacles move faster the higher you get, I wanted to add even *more intensity*. So why not just make the bpm go quicker too?

Luckily, I don't like to make stuff the conventional way. In this case that would mean I didn't want to compose music and create a audio file to loop during the gameplay. If I wanted to do anything dynamic and tweak anything during development, I'd need to do more myself in code. Most games with dynamic music separate the music into different layers and decide when to play each layer, making sure all are aligned to the beat. But if it's the beat itself that should be dynamic too, the music would sound warped and stretched when the tempo changes. The only way forward for me was to create something called a *drum machine*.

## Drum sounds

My version of this drum machine would play back certain audio clips at predefined times, at a dynamic rate. So for instance I'd create a kick sound effect that should play on every first and third count, and a snare that should play every second and fourth count. For the sound effects I used the well known 8-bit sound generator [Bfxr](https://www.bfxr.net){:target="_blank"}.

{% include image.html url="/assets/jumpywall-bfxr.png" alt="Bfxr with sound effects used in music" caption="Bfxr showing sounds effects used for the drum machine" %}

- Maybe show GarageBand screenshot if still available
- Show how audio clips are added and indexed with script
- Explain OnAudioFilterRead for beat clips with exact timing
- Add pan values for left-right pan
- LFO with synth melody in the same way as beats
