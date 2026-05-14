# Seedance 2.0 Premium Product Reveal — style guide

**Arcads route:** `POST /v2/videos/generate` with `"model": "seedance-2.0"`
**Use for:** Dark-background premium product launches, no person in frame

Read [seedance-2.md](seedance-2.md) for base platform rules (forbidden words, prompt length, timestamps, etc.) before composing prompts here.

## Core philosophy

**Restraint and revelation.** Each beat reveals slightly more — a new angle, a new detail, a new text line. The power comes from what you withhold, not what you show.

- Pure black void. No environment, no lifestyle context.
- Slow, deliberate camera movements — 3–5 seconds minimum per move.
- Every movement is smooth. No quick cuts, no handheld shake.
- The feel is premium, authoritative, restrained.

This is the opposite of UGC. Where UGC is imperfect and casual, premium reveal is flawless and controlled.

---

## 6-layer structure

### Layer 1 — Void stage setup

```
15-second dark product reveal video. Pure black background — deep void, no texture, no environment. Shot on a cinema camera with a macro lens. [Overall mood: cold and sleek / warm and luxurious / electric and futuristic.]
```

### Layer 2 — Product hero description

Describe the product precisely: shape, material, finish, color, text on label.

```
The product: [product name] — [shape description], [material/finish: matte black aluminum / frosted glass / glossy white plastic], [key design detail]. [Surface condition: dry and pristine / covered in condensation droplets / backlit so the liquid glows.]
```

Never use just `@(img1)` without verbal description — describe the product in full so the model understands what it's rendering.

### Layer 3 — Text narrative

Maximum 3 lines of text in 15 seconds. Each line under 8 words. Centered positioning in upper frame area.

Plan text reveals before writing the full prompt:

```
Text line 1 (appears ~2s): "[Short claim — 4-6 words]"
Text line 2 (appears ~7s): "[Secondary claim or stat — under 8 words]"
Text line 3 (appears ~12s): "[Brand name or CTA — 2-4 words]"
```

Text reveal styles: `fades in smoothly`, `snaps in sharply`, `types character by character`, `slides up from below`.

### Layer 4 — Reveal choreography

Describe the camera and product movement beat by beat. Slow is premium.

```
[00:00–00:04] [Tease: partial view, extreme close-up, or silhouette. First text line appears.]
[00:04–00:10] [Full reveal: camera pulls back to show complete product. Slow dolly or rotation. Second text line appears mid-move.]
[00:10–00:15] [Hero moment: ideal angle, dramatic light. Third text line appears. Camera settles.]
```

### Layer 5 — Lighting description

Rim lighting is mandatory. Never describe "studio lighting" (forbidden). Light sources are invisible — you only see what they illuminate.

```
Rim lighting from [left/right/both sides]: [color of light: cool blue / warm amber / neutral white / electric purple]. [Secondary fill if any: subtle warm glow from below / no fill, pure contrast.] [Specular highlights on product surface.] Light sources invisible — only the effect is visible.
```

### Layer 6 — Technical specs

```
Ultra-clean, sharp focus — opposite of UGC. Slow, smooth camera movement only. [Color grade: desaturated and cold / rich and warm / high contrast monochrome.] [Sound: deep bass hum / glass ping resonance / pure silence.] No handheld shake, no grain, no imperfections. No dialogue, no voiceover.
```

---

## Complete example prompt (15s)

```
15-second dark product reveal video. Pure black background — deep void, no texture. Cinema camera with macro lens. Cold, sleek, futuristic mood.

The product: Arcads Artificial Cola — tall slim aluminum can, matte black with gold and purple lettering, sharp edge design. Surface covered in fine condensation droplets, backlit so the liquid glows faintly through the top.

[00:00–00:04] Extreme close-up of the can's top edge, condensation catching the light. Camera holds still. White text fades in centered above: "Zero sugar. Maximum edge."
[00:04–00:10] Camera slowly dollies back and rotates left — full can comes into frame, rotating 90 degrees on an invisible turntable. Rim lighting catches the gold lettering. Text fades. New text snaps in: "24 credits a sip."
[00:10–00:15] Camera settles at hero angle — slight low shot looking up at the can. Dramatic rim light from both sides, cool blue on left, warm amber on right. Final text fades in slowly: "Arcads Cola."

Lighting: cool blue rim from left, warm amber from right. No fill — pure contrast. Specular highlights on condensation droplets. Light sources invisible.

Ultra-clean, sharp focus. Slow, smooth dolly and rotation only. Desaturated cold color grade. Deep bass hum under the reveal. No handheld shake, no grain, no imperfections.
```

---

## Beat timing reference

| Time | Content |
|------|---------|
| 0–4s | Tease: partial view or extreme close-up + text line 1 |
| 4–10s | Full reveal + camera movement + text line 2 |
| 10–15s | Hero angle + text line 3 + brand close |

---

## Text reveal timing

Pick one style per text line and specify it in the prompt:

| Style | Prompt phrase |
|-------|--------------|
| Smooth fade | `fades in gently over 1 second` |
| Sharp snap | `snaps in instantly — no fade` |
| Typewriter | `types in character by character` |
| Slide up | `slides up from just below center` |

---

## Common issues

| Issue | Fix |
|-------|-----|
| Background has texture/environment | Explicitly state "pure black void, no texture, no surface, no environment" |
| Camera moves too fast | Add "slow, deliberate — 3-5 seconds per movement" |
| Too many text lines | Max 3 lines in 15s — cut or consolidate |
| Looks like a product photo, not video | Add specific camera movement cues (dolly, rotation) |
| Lighting looks studio-lit | Replace "studio lighting" with specific rim lighting description |

## See also

- [seedance-2.md](seedance-2.md) — base platform rules, forbidden words, prompt checklist
- [seedance-2-product-hero.md](seedance-2-product-hero.md) — elemental product with water/mist/splash effects
