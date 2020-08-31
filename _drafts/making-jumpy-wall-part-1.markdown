---
layout: post
title:  "Verby Nouns: a Jumpy Wall Story - Part 1: A New Hope"
summary: Where I tell you about the story behind the game and how the project evolved over time.
date:   2020-08-30 10:00:00 +0200
---

>This is the first part of my series on making Jumpy Wall, an endless wall jumper for iOS and Android. In this part I share the story behind the game and how the project evolved over time.
>
>- [Part 2]({% post_url 2020-08-30-making-jumpy-wall-part-2 %}) Perfectly scaled pixel graphics
>- [Part 3]({% post_url 2020-08-30-making-jumpy-wall-part-3 %}) Dynamic drum computer with variable bpm and custom synth for the bass and melody

## The game

In September 2015 I released my first mobile game. Lifting on the already less popular 'verby noun' trend for simple and addictive mobiles games, inspired by Flappy Bird and Crossy Road. The game features one-touch controls to wall jump your way up, collection gems and avoiding obstacles. The scope of the games was deliberately left very small, with the simplest control scheme I could think of: tap to jump, hold down your finger to slowly slide down the wall.

The visuals of the game are the most notable. Every time the character on the screen hits a wall the colors for all the elements on screen are randomized. While this may sound disorienting, the simple pixel art style of the game makes all individual elements very recognizable.

![Pim Coumans behind his desk working on Jumpy Wall in 2015](/assets/jumpywall-pim-coumans.jpg){:.full-image}

Trying to emulate the success of Crossy Road I implemented unlockables but with color schemes instead of characters. Each of these color schemes could be bought with an in-app purchases or you could try to unlock one randomly by trading in a few collected gems. Every now and then (following the same pattern used in Crossy Road) you'd get a notification that you got free gems to try to unlock more color schemes, or you could watch an ad every now and then to get a little extra.

Jumpy Wall launched on September 3rd, 2015 with a very brief and small success.

## How it started

Early 2015 I quit my job to pursue a career in making games. While making games had always been something I hoped I would end up doing, I seemed more intrigued by tech in general and found myself learning iOS development out of sheer interest. The success of some indie games like Fez made me realize that making games could be a viable option. I had the privilege that I could save up enough money to sustain myself for at least 6 months, so I was all ready to dive headfirst into potentially a new career. My plan originally was to build and release one tiny game in one month and in the remaining five months I'd work on a bigger idea.

While thinking up simple game ideas, I wanted to limit myself with one-touch controls tap your finger anywhere on the screen) and ideally something that did not require making much content. As I've always been a fan of the concept of wall jumping (most likely fueled by TowerFall) the idea of an endless wall jumper quickly became a very viable option.

## Prototyping

To get somewhere quick, I started the first prototype with pixel art. I drew a generic block and stick figure character that would do the jumping. Of course this character had a sprite for jumping, falling, sliding from either side and standing still on the ground.

![Very first prototype with rectangles](/assets/jumpy-stick-figure.png)

From here I could play around with obstacles, controls and tweak the physics to get the gameplay to something enjoyable. With every new iteration I recorded a Vine ([RIP]({% post_url 2019-03-27-making-ok-video %})) which turned out the be a perfect way to showcase this game.

<video muted controls loop>
    <source src="/assets/jumpy-vine-1.mp4" type="video/mp4">
</video>
*Very basic wall jumping*

<video muted controls loop>
    <source src="/assets/jumpy-vine-2.mp4" type="video/mp4">
</video>
*Trying out some level design ideas*

By minimizing the complexity of the level design, I made it possible for the level to be endless. That would mean I could design a few chunks of level that would be randomly repeated as the character moved up. Now I have a game that has an endless level which greatly reduces the scope of the project. 

<video muted controls loop>
    <source src="/assets/jumpy-vine-3.mp4" type="video/mp4">
</video>
*Simplifying the level design

## The eye

The character needed to have the shape of a square to make platforming the most enjoyable. I wasn't happy with the generic stick figure so I set out to try something else. Also considering I'm not confident with character design, it needed to be as simple as possible. Eventually the simplest character I could come up with was a square with a huge eye inside. Because it would be just a square, making it squishy would be relatively straightforward, because only the square needed to be scaled in code without the need for any extra images.

<video muted controls loop>
    <source src="/assets/jumpy-vine-4.mp4" type="video/mp4">
</video>
*Introduction of a meaty square*

## Colors

Again being limited by my ability to design environments, I once more tried to simplify the aesthetics of the game by using a limited color palette. I found a free four-color palette online and applied it to the game. Now the eye and gems, the wall, the background, and spikes have their own bright color and suddenly the game looked really appealing.

<video muted controls loop>
    <source src="/assets/jumpy-vine-5.mp4" type="video/mp4">
</video>
*Introduction of a meaty square*

Jumpy Wall articles:

- Pixel camera and pixel alignment
- Drum computer (speed) and synthesizer
- Color schemes, in-game text and buttons?
- In-game trailer generation

Jumpy Wall takes pixel graphics seriously.
