# chromatic-drift-background-waves-screensaver.html
Summary 1. Third wave across the bottom half A dedicated front wave now sits in front of all the layered bands — a broad, slow wave with its crest around 56% of screen height, filled solid to the bottom edge. It has its own color and its own independent re-roll timer (5–20s), so it drifts and changes color on its own schedule..
Summary
1. Third wave across the bottom half
A dedicated front wave now sits in front of all the layered bands — a broad, slow wave with its crest around 56% of screen height, filled solid to the bottom edge. It has its own colour and its own independent re-roll timer (5–20s), so it drifts and changes colour on its own schedule. When it's on, the layered bands respace themselves into the upper portion so nothing gets swallowed. Toggle: Front wave.

2. Auto-start after idle + fullscreen
Start after idle slider: off → 60 minutes, default 3 min.
Idle is measured from real input events — pointer move, click, key, wheel, touch — tracked via lastInput.
When the timer expires, the page enters screensaver mode: the panel hides, the clock fades in, pointer influence is dropped, and fullscreen is requested.
One honest limitation: browsers require a user gesture for requestFullscreen(). A timer-driven request is normally rejected. So if it is, a small "Click to go fullscreen" pill appears at the bottom centre — one click completes it. Any click, key press, or Esc exits screensaver mode and restores your controls.
A web page also cannot read OS-wide idle time (browsers don't expose it), so this tracks page inactivity, which behaves the same way in practice: you're away, it takes over.
3. Deep space mode
One toggle swaps the entire scene profile:

CLASSIC
DEEP SPACE
Bands
5
14 (thin ridge stack)
Wave frequency
×1.0
×0.40 — much wider, slower swells
Amplitude
×1.0
×1.30
Stars
standard
3.4× more
Sun
striped disc
small distant planet (no stripes)
Palette
9 families
restricted dark set (Space / Nebula / Cobalt / Solaris)
Speed
0.5×
0.32×


The scene rebuilds instantly when you toggle, and the band slider now runs 3–20 so you can push it to 20 bands in either mode.

4. Speed and colour-change controls
Four separate sliders, because "how fast" and "how often" are different things:

CONTROL
RANGE
WHAT IT DOES
Wave speed
0.1–2×
how fast the waves physically roll
Change rate
0.2–3×
how often a new colour is picked (divides every timer)
Blend time
1–20s
how long the fade to the new colour takes — the "slow, smooth" knob
Variety
60–220
minimum RGB distance between new colours (low = wildly different, high = harmonious)


The colour pool is now 80 distinct colours across 10 families (Nebula, Ember, Tide, Vapor, Verdant, Cobalt, Solaris, Ink, Space, Aurora), so even at a high change rate you're never seeing the same colours twice.

5. Music-reactive colour
Two ways to connect audio:

Share audio → getDisplayMedia({audio:true}). A picker opens; choose a tab, window, or entire screen and tick "share audio". This is the one that reacts to whatever's playing in another app — Spotify, a video, a browser tab.
Microphone → getUserMedia. Reacts to music playing out loud in the room.
An AnalyserNode splits the signal into three bands and drives the visuals:

Bass → wave amplitude swells (up to +85%) and the sun/planet pulses in size.
Overall level → the whole scene drifts slightly faster.
Mids → hue rotation applied to every colour. The fills stay perfectly solid — it's the hue that rotates, so the palette swims through colour without any banding or transparency.
Highs → stars brighten.
All energies are smoothed with an EMA so nothing strobes. If you disconnect audio, everything keeps running normally.

Post-summary — what matters most
The four asks are genuinely independent now. Speed, change rate, blend time and variety are separate parameters, so "lots of colours but slow and smooth" is literally Change rate 2.5× + Blend time 14s + Variety 160. That combination is the preset I would ship.
The hue-rotation trick is the key to music reactivity. Mapping bass to amplitude and mids to hue keeps the solid-colour aesthetic intact — a brightness-flashing equaliser would have destroyed the look you asked for.
The idle→fullscreen gesture limitation is a browser rule, not a bug in the page. The pill fallback means it still works with one click, and Esc/click always restores your controls, so it can never trap you.
Deep space is a profile, not a separate file. Because it's one PROFILES object, you get the same sliders, the same music reactivity, the same idle behaviour — just different numbers.
Both files are still in the skill (index.html with the six patterns, waves-screensaver.html with this), so nothing was lost and I can extend either one later.
Epilogue — the real point
The page has crossed over from "an animated background" into "a screensaver you actually leave running." Open it, press F, walk away — after three minutes of your not touching anything it takes the screen over, hides itself completely, and drifts. Come back and one click hands the screen straight back to you.

The best configuration for pure atmosphere, and the one I'd suggest: Deep space on, wave speed 0.35, change rate 1.5, blend time 16s, variety 150, front wave on. Fourteen thin ridges in the dark, colours drifting through purple and blue at the pace of a slow exhale, and the whole palette rotating gently whenever music is playing.

If you want to go one step further, the next obvious build is a true OS screensaver — a .scr file or a small Electron wrapper that runs this in a borderless always-on-top window and launches it from Windows' Screen Saver settings, so it activates when Windows itself thinks you're idle. That's the one piece that needs a real application rather than a browser page, and I can write it for you on request.
