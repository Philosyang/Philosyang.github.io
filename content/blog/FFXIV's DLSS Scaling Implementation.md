---
title: "FFXIV's DLSS Scaling Implementation"
date: 2026-11-04
tags: ["slice-of-life"]
---

Evercold is on the clock, meanwhile I had an unrecoverable crash with FFXIV a while ago (probably because I updated ReShade to a version too new that gposingway isn't happy with). Thus might as well do a clean install.

I finished the install and tried to check on the visuals. Unsurprisingly it looked upscaled and I need to root cause it. I did ReShade + gposingway + DLSSTweaks (enforce DLAA) when Dawntrail was just launched. This time I want to check on whether the game actually needed either the DLSSTweaks or the nvidia app override method at all.

The first step is to find a concrete way to know the rendering resolution and the display resolution. There is a registry value change one can make to let the nvidia driver draw a text overlay (bottom left) on a DLSS game. You can search it online. There's also a script/exe on github that toggles it for you. One also needs to restart the game to see the overlay.

When I set it DLSS to always on, here's my overlay text:

```
Render Preset: C
DLSSv3 v3.5.10 D3D11 cubin: fatbin LDR NGX (1920,1080 -> 3840,2160)
```

It basically confirms that the game is rendering at a 50% scale. Fun fact, the game renders at 100% when you are in gpose, and goes back to what it was when you exit.

When I set it to only enable when below 30fps, the rendering scale gradually increases at a (+16,+9) per 0.5 second rate (it only steps when there are inputs, probably to avoid conflicts with the "auto limit fps when afk/unfocused" setting) until it hits (3840,2160 -> 3840,2160).

It's a clever implementation of a gradual ramp up/down on rendering scale, but it's too vague for end users to know when and how it kicks off.

It could probably be a nice feature to have to auto lower the rendering scale when in battle and ramp back up when out of one.