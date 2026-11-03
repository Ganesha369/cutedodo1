# CuteDoDo hero video: design package (Tier 1, "Royal Arrival")

Chosen concept: **Royal Arrival**. Service: **Kling** (account connected, credits to be topped up).
This folder stays outside `site/` so none of it ships.

## 1. Brand premise

**"The goodest boy."** Every meme coin lives in the sky as a chart. $DODO comes down to earth as a real dog with a real family and a real cause. The scroll is the descent: from cold sky to one warm, real Shih Tzu. Every section below the hero keeps proving the same thing: he is real, and so is the help.

## 2. Palette (direction now, exact values sampled from the approved footage)

The page palette already in `site/index.html` is the target world, so the footage is prompted into it:

```css
:root{
  --canvas:#F2F0FF;       /* lilac-tinted page */
  --panel:#FFFDF9;        /* sticker cards */
  --accent:#FF3B3B;       /* bow-tie red: Buy buttons only */
  --accent-hover:#E62E2E;
  --accent-muted:#FFC83D; /* gold glow, sparkles */
  --text-secondary:#3B4274;
  --text-primary:#0E1446; /* deep night navy */
}
```
Footage world: deep cobalt night sky, bubblegum-pink cloud edges, warm gold sparkle light, royal-blue velvet, red bow tie.

## 3. Type trio (unchanged)

Bricolage Grotesque 600/800 (display), DM Sans 400/500/700 (body), JetBrains Mono 500/700 (labels).

## 4. Storyboard (one continuous shot, about 8 seconds)

| Time | What the camera sees | Where text lives |
|---|---|---|
| 0.0 to 2.5s | High in a deep cobalt night sky. Soft pink-edged clouds drift below, tiny gold sparkles float like fireflies. Camera starts a slow, steady descent straight down. | Left half |
| 2.5 to 5.0s | Camera sinks through a layer of cloud. A wisp brushes the lens with a soft blur beat (the boundary moment). Warm gold light glows up from below. | Left half |
| 5.0 to 8.0s | Cloud clears. Camera eases to rest at eye level with Dodo sitting proudly on a royal-blue velvet cushion, red bow tie, plaid vest, tongue out, ears moving slightly, breathing. Gold rim light. | Left 45% (Dodo sits in the right third) |

**Ending frame (law 4):** Dodo in the right third, whole body in frame with generous room above his ears (the nav sits there) and below the cushion. The left side of the frame is the same velvet room fading into soft cobalt bokeh with gold sparkles: calm, one continuous world, ready for the headline.

## 5. Generation steps and prompts

Every image and video prompt carries the guard: no text, no logos, no lettering anywhere.

**Step 1: Ending frame** (image-to-image, 16:9, 2k, Dodo photo as reference). Made first so his look is locked before anything else.

> The same dog from image 1, a small Shih Tzu with a white face, a chocolate-brown patch over his right eye and ear, a brown left ear, black nose and pink tongue out, wearing his grey plaid vest and red velvet bow tie. He sits proudly on a plump royal-blue velvet cushion with gold piping, placed in the right third of the frame, whole body visible with generous space above his ears and below the cushion. The rest of the frame is the same cosy velvet room receding into soft deep-cobalt bokeh with tiny warm gold sparkles floating, edge to edge, calm and even on the left side. Warm gold rim light from behind, soft pink fill light. Cinematic, photorealistic, 16:9. No text, no logos, no lettering anywhere. No tags on the vest.

Inspect for: likeness (eye patch side, ear colours, bow tie red, vest plaid), no fake tags or lettering, paws and anatomy, left side calm.

**Step 2: Starting frame** (image-to-image, 16:9, 2k, the approved ending frame as palette reference)

> A view from high in a deep cobalt night sky, looking gently downward, composed as the first moment of a slow descent. Below, soft clouds with bubblegum-pink edges drift in layers, lit from beneath by a warm gold glow. Tiny gold sparkles float through the air like fireflies across the whole frame. Same colour world and light as image 1. No dog visible, no ground visible. Cinematic, photorealistic, 16:9. No text, no logos, no lettering anywhere.

**Step 3: Video** (Kling 4.0 image-to-video, first frame = Step 2, last frame = Step 1, 8 seconds, 720p)

> One continuous shot, no cuts. The camera descends slowly and steadily straight down from the night sky, through the layer of pink-edged clouds, and comes to rest at eye level with the small Shih Tzu sitting on his royal-blue velvet cushion. The scene stays alive the whole time: clouds drift, gold sparkles float and twinkle. Halfway down, a wisp of cloud brushes across the lens with a brief soft blur, then clears to warm gold light. The dog stays alive at the end: he breathes, his ears move slightly, his tongue is out, he blinks. The shot ends at rest on the composed final frame: the dog in the right third, calm velvet and cobalt bokeh on the left. No text or lettering anywhere.

Because Kling locks the last frame to the Step 1 image, Dodo's face cannot drift during the video.

## 6. Band map (starting points, checked later with the flick test)

| Band | Scroll range | Footage moment | Copy (ships as written) | Entrance |
|---|---|---|---|---|
| 1 | 0.00 to 0.22 | high sky, sparkles | "Most coins live up here. Charts, hype, thin air." | words drift up like sparkles |
| 2 | 0.26 to 0.50 | sinking into cloud | "This one comes down to earth." | slides down with the camera |
| 3 | 0.54 to 0.74 | cloud wisp, gold glow | "A real dog. A real family. A real cause." | three beats pop in one by one |
| 4 | 0.80 to 1.00 | Dodo at rest | Settle: the current hero block. "The goodest boy on Solana. Meet Dodo." plus subline, contract address, Buy $DODO, Whitepaper v2.3, Join the pack | sticker slap: scales in with a small tilt |

Every band gets a soft local scrim and a text shadow, checked against its busiest frame.

## 7. Static hero (phones, reduced motion, or if the video fails to load)

The ending frame as a still background with the settle block over it. This is the same copy as today's hero: "The goodest boy on Solana. Meet Dodo." / "A real Shih Tzu from Chennai. A meme with a mission. Big memes, bigger heart, and every paw counts." / Buy $DODO.

## 8. What changes on the page

- The hero becomes a tall sticky scroll section (about 4 screens) with the video behind the bands. The live price stats and everything below stay as they are.
- The scrub engineering standard from `scrub-pipeline.md` applies in full: Blob fetch with a loading ring, eased playback in a rAF loop, gated seeks, change-only DOM writes, static fallback gates, and a complete page without the video.
- The current sticker-photo hero is kept as the static fallback layout.

## 9. Gates

1. Ending frame: I inspect it, then you approve it.
2. Starting frame: I inspect it, then you approve it.
3. ⛔ Video gate: you watch the video before anything gets built around it.
4. Copy gate: zero em dashes and zero stock words before you see the page.
