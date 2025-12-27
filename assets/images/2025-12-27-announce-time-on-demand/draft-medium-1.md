---
layout: post
title:  Announce the time on demand (eyes closed)
date:   2025-12-27
tags: ios applewatch shortcuts
---

## TL;DR
I wanted to know the time in the morning without opening my eyes. The simplest setup ended up being:
- iPhone: a Shortcuts automation that speaks the current time, bound to the Action Button.
- Apple Watch: the built-in two-finger gesture that speaks the time (no shortcut needed).

## Motivation
Some mornings I’m still in bed and I want a quick time check without the whole “open eyes → pick up phone → get blinded by a bright screen” routine.

I figured there had to be a way to make my devices just tell me the time, on demand. My first thought was “this smells like Shortcuts”, so I asked ChatGPT for the lowest-effort, no-code setup.

## 1) iPhone: a Shortcut that speaks the time
My first attempt was an iOS Shortcut. The goal was: press a button, hear “It’s 9:42 AM”.

In Shortcuts, create a new shortcut (I called it “Announce Time”) with these actions:
1. `Date` → “Current Date”
2. `Speak Text` → `It’s ` + `Current Date` (tap the date variable and set `Date Style: None`, `Time Style: Short`)

I initially tried to use a custom time format, but the UI on my phone didn’t expose it. Formatting the `Current Date` variable directly (date style none + short time style) gave clean output without any extra actions.

To bind it to the Action Button:
- Settings → Action Button → Shortcut → “Announce Time”

## 2) Apple Watch: I overcomplicated it (AssistiveTouch)
Once the phone worked, I tried to get the same “announce time on demand” behavior on my watch. I went down the AssistiveTouch route, mapping a gesture so I could trigger the action without fiddling with tiny buttons.

It worked, but it felt like a lot of setup for what should be a basic “tell me the time” feature.

## 3) The Apple Watch feature I should’ve used first
After the detour, I learned that Apple Watch already has this built in: a two-finger press on the watch face that speaks the time.

The relevant setting is:
- Watch app → Clock → `Speak Time` (turn it on)

Once enabled, a two-finger press on the watch face announces the time.

So that’s now my default in bed: no shortcut, no automation, just the watch telling me the time when I ask.

## Loose end: speaker volume
The one downside is the watch speaker volume. In a quiet room it’s fine, but in the exact scenario where I care most (half-awake, head on a pillow), it can be annoyingly hard to hear even after turning the volume up.

I tried the obvious knobs (watch volume and alert volume), but it still feels inconsistent. If you know a reliable way to make the watch speak time louder (or route it somewhere sensible by default), I’m all ears.
