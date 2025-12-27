---
layout: post
title:  Announce the time without opening my eyes
date:   2025-12-27
tags: ios apple-watch shortcuts software
---

In the morning, before getting up, I sometimes want to know the time *without* opening my eyes. Not “set an alarm” time — just “tell me the time, on demand”.

I assumed I’d need a Shortcut (and I did end up building one), but it turns out Apple Watch already has this baked in.

## TL;DR

- **Apple Watch (built-in):** enable `Speak Time`, then do a two-finger press on the watch face to have it speak the current time.
- **iPhone (Shortcut, no code):** create an “Announce Time” shortcut that uses `Speak Text` with a `Current Date` variable formatted as time-only, then bind it to the Action Button (or AssistiveTouch).
- **Caveat:** the Apple Watch speaker can be surprisingly quiet (more on that at the end).

## How we got here

My first thought was: “This has to be doable with Shortcuts.” I wanted a single physical gesture that would announce the current time, so I don’t have to look at a screen (or even open my eyes).

So I asked ChatGPT, and started building a shortcut on my phone. Then I tried to make it equally easy on my watch (via AssistiveTouch), before realizing I had reinvented something Apple already shipped.

## Option 1: iPhone Shortcut (“Announce Time”)

The shortcut is deliberately boring. The only tricky part is formatting: on my device, the Shortcuts UI no longer exposes “Custom Format” for dates, so the formatting has to happen on the `Current Date` variable inside `Speak Text`.

Here’s the minimal shortcut:

~~~
Shortcut name: Announce Time

1) Date
   - Current Date

2) Speak Text
   - Text: "It's " + Current Date
   - Tap the "Current Date" variable:
     - Format: Date
     - Date Style: None
     - Time Style: Short
~~~

And then bind it:
- `Settings` → `Action Button` → `Shortcut` → pick `Announce Time`

If you don’t have an Action Button, this is still workable with AssistiveTouch, Back Tap, a widget, etc. The main point is that the shortcut itself can stay tiny.

## Option 2: Apple Watch (“Speak Time”)

After I had the shortcut working on my phone and started experimenting on the watch, I found out that Apple Watch already has a dedicated “speak the time” feature.

To enable it:
- On Apple Watch: `Settings` → `Clock` → toggle `Speak Time`

Once that’s on, you can do a two-finger press on the watch face and it will speak the current time. No Shortcuts, no automation, no syncing, no fiddling.

## Loose ends: speaker volume

The only remaining problem for my use case: when I’m half-asleep in bed, the watch speaker can be too quiet. Even with the watch volume turned up, it’s easy to miss if your wrist is under a blanket (or your pillow is doing a great job at sound absorption).

I don’t have a perfect fix yet. Right now, my fallback is the iPhone shortcut, since the phone speaker is louder (and more consistently positioned).

## Discussion

If you have a better “announce time” setup (especially something that reliably solves the watch speaker volume issue), I’d love to hear it.

