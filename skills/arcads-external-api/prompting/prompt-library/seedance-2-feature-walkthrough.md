# Seedance 2.0 Feature Walkthrough — style guide

**Arcads route:** `POST /v2/videos/generate` with `"model": "seedance-2.0"`
**Use for:** Fast-paced product feature demonstrations with physical proof of claims

Read [seedance-2.md](seedance-2.md) for base platform rules (forbidden words, prompt length, timestamps, etc.) before composing prompts here.

## Core principle

**Show over tell. Every feature claim is backed by a physical action.**

Don't say "it has a hidden pocket" — show the person reaching into it on camera. Don't say "it's lightweight" — show them tossing it with one hand. Density with clarity: 3 features in 15 seconds via jump cuts that isolate each demonstration.

---

## 7-layer structure

### Layer 1 — Format header

```
15-second vertical feature demo video. Handheld smartphone camera, [lighting: bright natural light / warm indoor light / clean overhead]. [Angle: eye-level medium shot / slightly above looking down.] Fast-paced, energetic.
```

Always `9:16` vertical. 15 seconds is the standard — enough room for 3 features.

### Layer 2 — Person + product

Person and product are inseparable from frame one.

```
[Age]-year-old [description] [gender] already wearing / holding / using the product from the very first frame. [Key physical traits: 2-3 details.] [Outfit: functional, appropriate for product context.]
```

The product should be in frame before the first word is spoken. No "reaching for it" openers.

### Layer 3 — Setting

Simple residential space that doesn't compete for attention.

```
[Room type: living room / bedroom / kitchen / backyard]. Clean enough to not distract, but residential — not staged. [1-2 background objects for context.]
```

Avoid: offices, gyms, coffee shops (too much visual noise). Home settings keep attention on the product.

### Layer 4 — Feature beats

The core of the format. Each beat = one feature, demonstrated physically.

**Beat architecture:**
- **Hook** — bold opening claim
- **Demo beat** — physical proof of the claim
- **Kicker** — urgency, verdict, or CTA

**3-beat structure (15s):**

```
[00:00] Hook: [Bold opening claim — one sentence. Person speaks directly to camera.]
[00:05] Demo 1: [Physical demonstration of feature 1. Silent or with short caption text. "She reaches into the hidden side pocket and pulls out her AirPods."]
[00:10] Demo 2 + Kicker: [Feature 2 demonstrated, followed by a verdict. "Throws it over one shoulder. 'I've worn this every day for a month.' Gives a thumbs up."]
```

One beat can be silent — physical action with graphic overlay, no dialogue.

**Hook formulas that work:**
- Challenge: `"Okay so I need everyone to see this."`
- Result-first: `"This thing solved the problem I've had for three years."`
- Relatable pain: `"If you're tired of [problem], watch this."`

### Layer 5 — Graphic overlays

On-screen text reinforces the feature being shown.

```
Graphic overlays: [When and what text.] Example: "At [00:05] a white caption appears: '[Feature name]'" / "At [00:08] an arrow callout points to the hidden pocket."
```

Overlay types:
- Caption bar: lower-third white text on semi-transparent background
- Callout arrow: animated arrow pointing to the product feature
- Feature title: large centered bold text that snaps in and fades
- None: let the action speak (works for obvious demos)

Limit to 2-3 overlays max — more than that competes with the physical demo.

### Layer 6 — Tone

```
Tone: [confident and fast-paced / excited and punchy / relatable and casual]. She speaks quickly — almost interrupting herself — like she can't wait to show you the next thing. Energy is high throughout.
```

This style is faster and more energetic than standard UGC. Pacing drives it.

### Layer 7 — Technical specs

Phone-quality aesthetic, but not as imperfect as pure UGC.

```
Handheld but relatively steady — minimal shake. Natural phone quality, not color graded. Sharp enough to read text on the product. No slow-motion. Audio: clear phone mic, slight ambient room noise. No studio mic quality.
```

---

## Complete example prompt (15s apparel)

```
15-second vertical feature demo. Handheld smartphone, bright natural light, eye-level medium shot. Fast-paced, energetic.

A 27-year-old athletic woman with a short brown ponytail and confident posture. Wearing the product — a matte black packable jacket — from frame one. Casual fitted outfit underneath.

Living room. Clean but residential — couch and plant in background.

[00:00] She looks straight at camera: "Okay I need you to see how many pockets this has."
[00:05] She reaches into a hidden interior chest pocket and holds up her phone toward camera. Caption appears: "Hidden phone pocket." Then zips it shut in one motion.
[00:09] She grabs the bottom of the jacket, stuffs the entire jacket into its own chest pocket — it compresses into a compact square she holds in her palm. Says: "Packs into itself. I'm not joking."
[00:13] She gives a thumbs up. "This is my airport jacket now." Caption: "Links in bio."

Graphic overlays: white caption bar at [00:05] for "Hidden phone pocket." No other overlays — let the demos speak.

Tone: confident and fast-paced. She almost interrupts herself. High energy throughout.

Handheld but relatively steady. Natural phone quality, not color graded. Sharp enough to read text. No slow-motion. Clear phone mic audio with slight ambient room noise.
```

---

## Multi-clip strategy for 4+ features

Products with 4+ features should split across 2-3 separate prompts.

| Clip | Features | Hook |
|------|----------|------|
| Clip 1 | Features 1-3 | Strongest feature as hook |
| Clip 2 | Features 4-6 | Second strongest as hook |
| Clip 3 | Features 7+ or combo | "More things they didn't show you" |

Keep tone and person consistent across clips for a cohesive series.

---

## Feature demo verbs

Replace abstract claims with concrete actions:

| Claim | Physical demo |
|-------|--------------|
| "Lightweight" | Toss it with one finger / hold it on one fingertip |
| "Hidden pocket" | Reach in and retrieve an object on camera |
| "Packs small" | Compress into internal pouch, hold in palm |
| "Waterproof" | Pour water directly on it, wipe away with one motion |
| "Strong" / "durable" | Twist, bend, pull — demonstrate stress |
| "Easy to open" | One-hand operation, filmed in close-up |

---

## Common issues

| Issue | Fix |
|-------|-----|
| Features described, not shown | Rewrite as physical actions — see demo verbs table |
| Too much dialogue, not enough action | Replace one dialogue beat with a silent demo beat |
| Setting too distracting | Use blank wall or simplified background |
| Too slow / low energy | Shorten each beat by 1s; add "fast-paced, almost interrupting herself" to tone |
| 4+ features in one 15s clip | Split across 2-3 clips; 3 features max per clip |

## See also

- [seedance-2.md](seedance-2.md) — base platform rules, forbidden words, timestamps, prompt checklist
- [seedance-2-ugc.md](seedance-2-ugc.md) — softer UGC testimonial style (less demo-focused)
