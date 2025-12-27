---
layout: post
title:  Announce time on demand (without opening your eyes)
date:   2025-12-27
tags: ios apple-watch shortcuts software
---

## TL;DR
- iPhone: a 3-action Shortcut + Action Button = "It’s 7:42 AM" on demand.
- Apple Watch: I tried to recreate this with Shortcuts + AssistiveTouch… and then learned watchOS already has it: **Taptic Time** (hold two fingers on the watch face).
- Loose end: Apple Watch speaker volume for `Speak Text` was way harder than it should be (at least on my Series 6).

## The problem
In the morning, lying in bed, I’m often awake enough to wonder what time it is, but not awake enough to want light in my face.

I wanted a way to get the time **on demand**, ideally without opening my eyes:
- press a button
- hear the time
- go back to sleep (or finally get up)

My first thought was: this sounds like an iOS Shortcuts thing. So I asked ChatGPT.

Full transcript: [transcript]({{ site.baseurl }}{% link transcript.md %})

## iPhone: announce time with the Action Button
The Shortcut itself is straightforward (no code required):

1. Open **Shortcuts** → create a new shortcut called `Announce Time`.
2. Add **Speak Text**.
3. In the Speak Text content, type `It's `, then insert `Current Date`.
4. Tap the inserted `Current Date` variable and set:
   - Format → `Date`
   - Date Style → `None`
   - Time Style → `Short`

Then bind it to the Action Button:
- **Settings** → **Action Button** → **Shortcut** → pick `Announce Time`

That’s it. Press button, phone speaks the time.

One small snag: a bunch of older guides talk about a custom time format (like `h:mm a`). On my phone, the “Custom Format” option simply wasn’t there. Formatting the `Current Date` variable inside `Speak Text` worked fine and kept the shortcut simple.

## Apple Watch: I rebuilt it... and then learned it already existed
Next I wanted it on my Apple Watch too, ideally triggered without hunting for a tiny on-screen button.

I got it working by running the same Shortcut on the watch and triggering it via **AssistiveTouch** (accessibility gestures mapped to “Run Shortcut”). Two notes that helped:
- In the shortcut details, enable **Show on Apple Watch**.
- Prefer actions that run fully on watchOS (for this one, `Speak Text` is fine).

And then I learned watchOS already has a purpose-built feature: **Taptic Time**.

Enable it:
- Watch → **Settings** → **Clock** → **Taptic Time** → choose a mode (I like `Terse`)

Use it:
- on your watch face, **touch and hold two fingers** on the display

That’s the “double finger press” I was looking for. No shortcut. No speaker. No fiddling.

## Loose end: the Apple Watch speaker was… loud
The original plan was “hear the time”, but on my Apple Watch Series 6, `Speak Text` volume ended up being surprisingly stubborn. Sliders didn’t seem to affect it, and even adjusting volume mid-speech was inconsistent (it felt like a separate “Siri voice” volume I couldn’t reliably control).

In the end, this pushed me further toward Taptic Time (or speech via AirPods when I actually want audio).

## Discussion
If you have a reliable way to control `Speak Text` volume on older Apple Watches, I’d love to hear it.
