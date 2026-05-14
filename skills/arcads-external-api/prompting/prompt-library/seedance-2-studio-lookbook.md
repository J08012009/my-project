# Seedance 2.0 Studio Lookbook — style guide

**Arcads route:** `POST /v2/videos/generate` with `"model": "seedance-2.0"`
**Use for:** Polished product showcase videos with voiceover, multiple outfit/styling variations

Read [seedance-2.md](seedance-2.md) for base platform rules (forbidden words, prompt length, timestamps, etc.) before composing prompts here.

## Core concept

Middle ground between raw UGC and high-end commercial. **The visuals lead and the voice follows.**

The person does not talk to camera. They pose, turn, inspect, move — and a voiceover narrates what you're seeing. No lip-sync required. This frees the visual from dialogue pacing and lets each shot linger.

Key differentiator from UGC:
- **UGC:** Person speaks to camera, imperfect, raw
- **Lookbook:** Person moves and poses, voiceover narrates, polished but not sterile

---

## 7-layer structure

### Layer 1 — Format header

```
15-second vertical studio lookbook video. [Camera system: cinema camera / DSLR / high-end mirrorless.] [Lighting approach: softbox diffused light / natural window light / ring light + fill.] [Mood: aspirational and elevated / warm and approachable / cool and editorial.]
```

### Layer 2 — Person and styling

Model description with 2-3 outfit variations using the same product.

```
[Age]-year-old [description] model. [Hair, build, key traits — 2-3 details.] Throughout the video they wear the product styled [3 ways: way 1 / way 2 / way 3].
```

Show the product's versatility. Outfit variation proves the product works across contexts.

Examples:
- Jacket: `casual with jeans / layered over hoodie / dressed up with trousers`
- Bag: `crossbody / shoulder / hand-carried`
- Sneaker: `with athletic wear / with chinos / with casual dress`

### Layer 3 — Studio setting

Backdrop and any behind-the-scenes elements that signal authenticity.

```
[Backdrop: seamless white / neutral grey / light sand / blush pink] backdrop. [Optional: light stand visible at edge of frame / clothing rack with more product visible in background / natural window light from one side.] The setting feels like a brand shoot, not a staged ad.
```

Behind-the-scenes elements (visible light stand, extra pieces on a rack) signal "this is real brand photography" and create authenticity without going full UGC-rough.

### Layer 4 — Shot sequence

3-4 shots per 15 seconds. Each shot lingers 3-4 seconds — no quick cuts.

```
[00:00–00:04] [Shot 1: Opening — [full body or 3/4 shot]. [Action: model enters frame and turns to face camera / model stands still, camera slowly pushes in.] [Styling: outfit variation 1.]]
[00:04–00:08] [Shot 2: [Medium shot]. [Action: model adjusts/touches product, inspects it, turns to show side profile.] [Close-up detail beat: extreme close-up of [construction detail — stitching, zipper, hardware, fabric texture].]]
[00:08–00:12] [Shot 3: [Second styling]. [Action: model walks across frame / poses at camera.] [Voiceover continues.]]
[00:12–00:15] [Shot 4: [Final styling or hero shot]. [Action: model poses confidently, camera holds. Product clearly visible.] [Brand or CTA text appears.]]
```

**At least one extreme close-up of a construction detail is required** — stitching, zipper, fabric weave, hardware. This proves quality and signals craftsmanship.

### Layer 5 — Voiceover script

2-3 sentences maximum. Conversational but measured. Not a salesperson — more like a knowledgeable friend.

```
Voiceover (begins at ~[2]s, runs under visuals):
"[Sentence 1: context or discovery — how you found it or what makes it different.]
[Sentence 2: key claim — what it does or how it performs.]
[Sentence 3: verdict or invitation — who it's for or CTA.]"
```

Voiceover rules:
- Conversational but confident — not breathless or over-excited
- Measured pace — each sentence lands cleanly before the next starts
- The person does NOT mouth the words on camera
- Max 35 words total (fits 15s at a measured pace)

### Layer 6 — Tone and pacing

```
Tone: [aspirational but approachable / cool and editorial / warm and confident]. Shot pacing: slow and deliberate — each cut lets the previous image breathe. No jump cuts. The product is the star; the model is the context.
```

### Layer 7 — Technical quality

```
[Camera quality: DSLR sharpness with shallow depth of field / mirrorless detail.] Soft, flattering light — [source: diffused softbox / natural window] — [direction: front-fill / side-lit for dimension.] [Color grade: clean and natural / slightly warm / slightly desaturated for editorial feel.] Audio: [voiceover clean and close-mic'd / slight warmth, no reverb.] No handheld shake. No grain. No imperfections.
```

---

## Complete example prompt (15s apparel)

```
15-second vertical studio lookbook. Cinema camera with shallow depth of field. Diffused softbox lighting from front-left. Aspirational, warm, approachable mood.

27-year-old athletic woman, natural brown waves past shoulders, confident posture. She wears a matte black packable jacket throughout — styled three ways: 1) casual with high-waisted jeans 2) layered over an oversized cream hoodie 3) dressed up with fitted trousers.

Seamless light grey backdrop. Portable clothing rack visible at right edge of frame with more product. Light stand partially visible — signals a real brand shoot.

[00:00–00:04] Full-body shot: model walks into frame from left wearing style 1 (casual jeans). Faces camera, turns slowly to show the side profile. Voiceover begins.
[00:04–00:07] Extreme close-up: hands unzipping and re-zipping the front closure — stitching and hardware detail sharp and clear.
[00:07–00:11] Medium shot: model wearing style 2 (hoodie layer), adjusts the collar and tucks hands in pockets. Camera slowly pushes in to 3/4 shot.
[00:11–00:15] Final hero: model wearing style 3 (trousers), poses confidently toward camera. Camera holds. Brand text fades in: "Arcads Outerwear."

Voiceover (starts at 2s, measured pace):
"I've tested a lot of packable jackets and this is the first one that actually looks good. Warm down to 40, packs into its own pocket in under ten seconds. Honestly — wear it everywhere."

Tone: warm and confident. Shot pacing slow and deliberate — each cut lets the frame breathe. No jump cuts.

DSLR sharpness, shallow depth of field. Diffused softbox from front-left. Slightly warm color grade. Voiceover clean and close-mic'd with slight warmth, no reverb. No handheld shake, no grain.
```

---

## Voiceover pace calibration

Read the voiceover aloud at a measured, unhurried pace. Count seconds. It should feel like a calm, knowledgeable recommendation — not a product pitch.

| Word count | Fits in |
|------------|---------|
| 1–10 words | 4–5s |
| 11–20 words | 6–9s |
| 21–30 words | 10–13s |
| 31–35 words | 14–15s |
| 36+ words | Too long — cut |

---

## Common issues

| Issue | Fix |
|-------|-----|
| Looks like a commercial, not a lookbook | Add behind-the-scenes elements: "clothing rack visible, light stand partially in frame" |
| Person is talking to camera | Explicitly say "the person does NOT address camera — they pose, turn, and inspect" |
| Shots cut too fast | Add "each shot lingers 3-4 seconds — slow, deliberate pacing" |
| No construction detail shot | Add an extreme close-up beat of stitching, zipper, or hardware |
| Voiceover too fast/salesy | Read aloud at measured pace; cut words until it breathes |

## See also

- [seedance-2.md](seedance-2.md) — base platform rules, forbidden words, prompt checklist
- [seedance-2-ugc.md](seedance-2-ugc.md) — raw UGC testimonial style (person speaks to camera)
- [seedance-2-feature-walkthrough.md](seedance-2-feature-walkthrough.md) — fast-paced feature demo style
