---
layout: post
title: Announce time on demand (without opening your eyes)
date:   2025-12-27
tags: software
---

## TL;DR
In bed, I wanted to know the time without opening my eyes.

- **iPhone:** a one-action Shortcut (`Speak Text`) bound to the Action Button.
- **Apple Watch:** skip the “announce it” Shortcut and use Apple’s built-in **Taptic Time** (no speaker volume surprises).

Full transcript of my back-and-forth with ChatGPT is in [transcript.md](/transcript.md){:target="_blank"}.

## How we got here
Some mornings, before I’ve fully booted up as a human, I want to know the time without the bright screen + eye-opening ceremony. I basically wanted “tell me the time” on demand, hands-free-ish, and ideally without thinking.

My first thought was: “This feels like a Shortcuts thing.” So I asked ChatGPT, and it gave me a pretty reasonable recipe: grab current time → speak it → bind it to a button.

That’s what I did. And then I fell into a classic Apple platform progression:

1. It works great on iPhone.
2. It mostly works on Apple Watch.
3. It turns out Apple Watch already had a better built-in way.
4. Also the Watch speaker volume is… a journey.

## 1. iPhone: “Announce Time” in one Shortcut
Here’s the simplest version I ended up using (no code, just Shortcuts):

- Create a Shortcut named `Announce Time`
- Add `Speak Text`
- In the text field, type `It's ` and insert `Current Date`
- Tap the inserted `Current Date` variable and set:
  - `Format`: `Date`
  - `Date Style`: `None`
  - `Time Style`: `Short`

Now it speaks something like “It’s 9:42 PM” instead of reading the full date.

If you were trying to do this via a `Format Date` / custom format string and couldn’t find the “Custom” option (same), formatting the `Current Date` variable inline like this is the path of least resistance.

To bind it to the Action Button (if you have one):

- Settings → `Action Button` → `Shortcut` → pick `Announce Time`

## 2. Apple Watch: the Shortcut approach (AssistiveTouch)
I wanted the same “announce time” behavior on my Apple Watch, ideally behind a physical action.

There are a few ways to trigger something “hardware-ish” on watchOS (depending on model). The one I set up was **AssistiveTouch**, which can map a hand gesture to “Run Shortcut”.

At a high level:

1. Make sure your `Announce Time` Shortcut is available on the watch (Shortcuts app → the Shortcut → enable “Show on Apple Watch”).
2. Watch app on iPhone → Accessibility → `AssistiveTouch` → enable it.
3. Configure a gesture (e.g. double-clench) to `Run Shortcut` → `Announce Time`.

This works, and it’s kind of magical the first time.

## 3. Plot twist: Apple Watch already had “time on demand”
After I got the Shortcut + AssistiveTouch setup working, I found out the Apple Watch already has a built-in feature for exactly this use case: **Taptic Time**.

On my watch, the setup is:

- Apple Watch Settings → `Clock` → enable `Taptic Time` (I like `Terse`)

And the “on demand” gesture is:

- On the watch face, touch and hold two fingers on the display

It vibrates the time. No screen, no Shortcut, no speaker.

## Loose end: the Apple Watch speaker volume
The whole reason I went looking for a non-speaker option is that the “announce it out loud” version on my Apple Watch was unreasonably loud in a quiet bedroom, and the obvious volume sliders didn’t consistently affect it.

Maybe this is model / watchOS specific, but the short version of my experience was: **Shortcuts → `Speak Text` did not reliably respect the volume controls I expected**.

Taptic Time completely sidesteps this. (Phew.)

## Discussion
I went in thinking I’d be gluing together a clever Shortcut, and came out appreciating that Apple already built a more ergonomic solution.

If you’ve found a reliable way to control the Apple Watch `Speak Text` volume (especially on older models), I’d love to hear it.
