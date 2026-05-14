# Seedance 2.0 UGC — 9-layer formula

**Arcads route:** `POST /v2/videos/generate` with `"model": "seedance-2.0"`
**Use for:** Authentic smartphone-style UGC product reviews and testimonials

Read [seedance-2.md](seedance-2.md) for base platform rules (forbidden words, prompt length, @(img1) mapping, etc.) before composing prompts here.

## The 9-layer formula

Stack all 9 layers in order. Missing layers produce polished, fake-looking output.

### Layer 1 — Format header

Technical specs that set the camera "contract" for the model.

```
[Duration]-second vertical iPhone selfie video, handheld front camera, soft natural indoor light, slightly low angle looking up at subject.
```

- Duration: 10s for tight hook-and-punchline; 15s for fuller story (3-4 beats)
- Always specify `vertical` (maps to `aspectRatio: "9:16"`)
- Always say `iPhone` or `smartphone front camera` — sets the quality floor

### Layer 2 — Person

Realistic human with 2-3 skin texture details. No AI-smooth skin.

```
[Age]-year-old [ethnicity/build] [gender] with [hair description]. [Skin realism: visible pores, slight unevenness in skin tone, minor undereye shadows — pick 2-3.] [Distinguishing feature if any.]
```

**Skin realism cues (pick 2-3):**
- `visible pores`
- `slight unevenness in skin tone`
- `minor undereye shadows`
- `a hint of shine on the nose and forehead from natural oils`
- `slight pinkness on cheeks` (fair/medium skin)
- `minor skin texture variation`

Do NOT use: acne, pimples, blemishes, redness, skin conditions. Goal is "unretouched real person," not "person with problems."

### Layer 3 — Setting

Lived-in space. Name 3-4 specific clutter objects.

```
[Room type] — [object 1], [object 2], [object 3], [optional object 4] visible in background. [Ambient light source.]
```

Examples:
- `Bedroom — unmade bed, phone charger on nightstand, half-empty water bottle, hoodie on chair. Warm lamp glow.`
- `Living room — throw pillows in a pile, houseplants, TV remote, open snack bag on coffee table. Afternoon window light.`
- `Kitchen — dirty dishes in sink, coffee maker, takeout containers, reusable grocery bag on counter. Overhead fluorescent.`

Avoid: clean, organized, minimal, staged, neutral.

### Layer 4 — Product introduction

How the item physically enters the frame.

```
She holds up [product description] toward camera with one hand — [how it's held: label facing forward, bottom gripped loosely, held at arm's length, etc.].
```

Include product color, shape, size, and any text on it. Do NOT rely solely on `@(img1)` — describe the product verbally too for consistency.

### Layer 5 — Script beats

Jump-cut scenes mixing dialogue and silent action. Read these aloud at a natural, unhurried pace with pauses between sentences to verify they fit the runtime.

**10-second structure (2-3 tight cuts):**
```
[00:00] [Hook line — bold claim or question. One sentence.]
[00:04] [Silent beat — physical action: holds up product, takes a sip, inspects it.]
[00:07] [Punchline — verdict or CTA. One sentence.]
```

**15-second structure (3-4 beats):**
```
[00:00] [Hook — bold opening line.]
[00:04] [Beat 2 — expands claim or shows product in use.]
[00:08] [Silent beat or secondary dialogue.]
[00:12] [Kicker — verdict, urgency, or CTA.]
```

Silent beats are NOT optional — they prevent cramming too much dialogue into the runtime and create pacing rhythm.

**Dialogue embedding format:**
```
She says: "I've been using this for two weeks and I'm obsessed."
```
or inline: `mid-sentence she says "okay wait—"`

### Layer 6 — Tone direction

Emotional texture plus explicit pacing cues.

```
Tone: [adjective] and [adjective]. [One-sentence pacing direction: "She speaks at a natural casual pace, pausing slightly between sentences like she's gathering her thoughts." or "Fast-paced and punchy — she barely finishes one sentence before jumping to the next."]
```

Good tone combos for UGC:
- `Warm and conversational`
- `Excited and disbelieving`
- `Relatable and low-key`
- `Confident and direct`

Avoid: `professional`, `polished`, `formal`, `cinematic` — these are forbidden words in Seedance.

### Layer 7 — Edit style

How the cuts relate to each other.

```
Jump cuts between each beat. No cross-fades or wipes. Each cut is abrupt and purposeful — feels like clips stitched together in a phone editor.
```

Options:
- `Jump cuts` — UGC standard, most authentic
- `Single continuous shot` — works for 10s with one clear arc
- `Match cuts on action` — cuts mid-motion (e.g., hand reaches → new angle mid-reach)

### Layer 8 — Technical flaws

Lighting, camera, and audio imperfections. Include at least 4.

```
CRITICAL STYLE: Must look like an unedited phone video, NOT a produced commercial. Include: [pick 4-5]:
- slight motion blur on hair strands
- slightly overexposed highlights on forehead and nose
- visible image grain and noise
- iPhone front camera wide-angle lens distortion
- slightly off-center framing, tilted a few degrees
- natural phone quality, not color graded
- soft focus — nothing is tack sharp
- uneven ambient lighting, one side slightly in shadow
- audio that sounds like a phone mic in a room, not a studio mic
```

### Layer 9 — Vibe statement

One sentence emotional anchor that captures the feeling the video should leave.

```
This feels like a real person genuinely excited to share something they found — not an ad, not a spokesperson, just a person talking to their phone.
```

Write this in plain English as a feeling description, not a technical instruction.

---

## Complete example prompt (15s)

```
15-second vertical iPhone selfie video, handheld front camera, soft natural indoor light, slightly low angle.

A 28-year-old Latina woman with voluminous dark wavy hair, visible pores, slight unevenness in skin tone, minor undereye shadows. Casual oversized cream sweatshirt.

Living room — throw pillows in a pile, houseplants, TV remote visible. Warm lamp glow.

She holds up a tall purple and gold energy drink can (@(img1)) toward camera with one hand, label facing forward.

[00:00] She says: "Okay I don't usually post about drinks but this one actually got me."
[00:05] Silent beat — she cracks the can open and takes a slow sip, eyes closed, genuine reaction.
[00:09] She says: "Like I finished the whole thing before I even realized. Zero crash. Zero gross aftertaste."
[00:13] She grins at camera: "I'll link it."

Tone: warm and genuinely surprised. She speaks at a natural pace with a small pause after the sip.

Jump cuts between each beat. Abrupt, purposeful — feels like clips from a phone editor.

CRITICAL STYLE: This must look like an unedited phone video. Include: slight motion blur on hair strands, slightly overexposed highlights on forehead and nose, visible grain and noise, iPhone wide-angle lens distortion, natural phone quality not color graded, soft focus — nothing tack sharp. Audio sounds like a phone mic in a room. No retouching, no beauty filter, no studio lighting.

This feels like a real person genuinely excited to share something they found — not an ad.
```

---

## Duration and dialogue calibration

Say every dialogue line out loud at natural pace with pauses. If it doesn't fit in the runtime, cut lines — not pauses.

| Script word count | Duration |
|-------------------|----------|
| 1–8 words | 4–5s |
| 9–15 words | 6–8s |
| 16–25 words | 9–12s |
| 26–35 words | 13–15s |
| 36+ words | Split into multiple clips |

---

## Common issues

| Issue | Fix |
|-------|-----|
| Looks too polished | Add ALL technical flaw cues — don't skip any |
| Too much dialogue crammed in | Read aloud at natural pace; cut until it fits |
| Person looks fake/airbrushed | Add 2-3 skin texture cues from Layer 2 |
| Background looks staged | Add 3-4 specific clutter objects by name |
| Product unrecognizable | Describe color, shape, size verbally + use @(img1) |

## See also

- [seedance-2.md](seedance-2.md) — base platform rules, forbidden words, timestamps
- [ugc-selfie-style.md](ugc-selfie-style.md) — cross-model UGC guide (Sora 2 / Veo 3.1)
- [ugc-product-selfie.md](ugc-product-selfie.md) — still image → UGC selfie with Nano Banana 2
