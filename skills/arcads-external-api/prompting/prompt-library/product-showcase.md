# Product Showcase — AI person with product workflow

**Use when:** The user wants to generate a video of an AI person (not a real influencer) interacting with or showcasing a product. Bridges still image generation (Nano Banana 2) to video generation (Veo 3.1, Sora 2, or Kling 3.0).

## Overview

The workflow has 5 stages:

1. Collect product imagery and context
2. Generate a still of an AI person with the product (Nano Banana 2)
3. QA the still internally
4. User approves the still
5. Animate the still into video

---

## Stage 1 — Collect inputs

Ask the user for:

1. **Product photo** — file on disk (`references/products/`). NOT chat-pasted.
2. **Product details** — name, key features, target audience, pain point it solves. Pull from `MASTER_CONTEXT.md` product section if available, or from Arcads product fields.
3. **Person description** — age range, gender, ethnicity/build, vibe. Or ask "does a specific character exist in `references/influencers/`?"
4. **Intended use** — UGC-style social ad, premium brand content, product demo? This determines prompt framing.
5. **Video model preference** — Veo 3.1 (best UGC/start-frame fidelity), Sora 2 (longer duration), or Kling 3.0.

---

## Stage 2 — Generate the still (Nano Banana 2)

### Upload the product photo

Upload via presigned URL:

```bash
# Get presigned URL
curl -sS -X POST \
  -H "Authorization: $ARCADS_BASIC_AUTH" \
  -H "Content-Type: application/json" \
  -d '{"fileType":"image/jpeg"}' \
  "https://external-api.arcads.ai/v1/file-upload/get-presigned-url"

# PUT the file to the presigned URL
curl -sS -X PUT \
  -H "Content-Type: image/jpeg" \
  --data-binary "@references/products/your-product.jpg" \
  "$PRESIGNED_URL"
```

Save the returned `filePath` — this is the product reference.

### Compose the still prompt

```
[Aspect ratio: 9:16 vertical for social / 16:9 landscape for YouTube].
[Person description: age, gender, ethnicity/build, hair, key distinguishing features.]
[Skin realism: visible pores, slight unevenness in skin tone, minor undereye shadows — pick 2-3.]
They are [interaction: holding the product at arm's length toward camera / using the product / looking at the product with a reaction].
[Product description: color, shape, size, label text — describe verbally even though it's also a reference image.]
[Grip: naturally gripping the [product type] with relaxed fingertips, anatomically correct hand with five fingers.]
[Expression: candid, mid-speech / genuine excitement / natural relaxed look — NOT a posed smile.]
[Outfit: appropriate to the scene and brand vibe.]
[Setting: 1-2 sentences describing the environment.]
[Lighting: natural / indoor warm / outdoor bright.]
[Style notes: raw and authentic / polished and aspirational.]
Avoid: distorted face, extra fingers, anatomically incorrect hands, airbrushed skin, studio backdrop unless specified.
```

### API call

```json
POST /V2/images/generate
{
  "productId": "YOUR_PRODUCT_ID",
  "model": "nano-banana-2",
  "aspectRatio": "9:16",
  "prompt": "<composed prompt>",
  "referenceImages": ["<product filePath>"]
}
```

Note: `referenceImages` is an array of plain strings (filePath values), not objects.

### Poll for result

```bash
GET /v1/assets/{assetId}
```

Poll every 5 seconds until `status === "generated"`. Typical time: 30–60 seconds.

---

## Stage 3 — Internal QA (before showing user)

Check the generated still for:

- [ ] **Face** — no distortion, proportions look human
- [ ] **Hands** — correct number of fingers (5), natural grip on product
- [ ] **Product** — recognizable, not warped or garbled text
- [ ] **Skin** — not airbrushed/plastic-looking
- [ ] **Framing** — product visible and prominent

If any critical issue found, retry up to **2 times** before showing the user. On the 3rd attempt or after 2 retries, show the best result with a note about what's off.

Retry prompt adjustments:
- Hand issues: add `"naturally gripping the [product] with relaxed fingers, anatomically correct, five fingers clearly visible, no extra digits"`
- Face issues: add more specific face description or reduce style guidance that may be competing
- Product issues: add more verbal description of the product (don't rely solely on the reference image)

---

## Stage 4 — User approval

Show the generated still alongside the product reference:

```
Here's the generated product showcase still.

[Display image]

QA notes:
- Face: ✓ natural proportions
- Hands: ✓ natural grip, 5 fingers visible
- Product: ✓ clearly recognizable

Ready to animate to video? Or would you like adjustments to the expression, framing, or setting first?
```

**Do NOT proceed to video generation without explicit user approval.**

---

## Stage 5 — Animate to video

Once approved, upload the still as a `startFrame` (for Veo 3.1 and Kling 3.0) or as a style reference (for Sora 2).

### Upload the approved still

```bash
# Upload the generated still image
curl -sS -X POST \
  -H "Authorization: $ARCADS_BASIC_AUTH" \
  -H "Content-Type: application/json" \
  -d '{"fileType":"image/jpeg"}' \
  "https://external-api.arcads.ai/v1/file-upload/get-presigned-url"
```

Save the `filePath` for use as `startFrame`.

### Model selection

| Model | Best for | startFrame support |
|-------|----------|-------------------|
| **Veo 3.1** | UGC, dialogue, authentic motion | Yes — literal frame-one fidelity |
| **Kling 3.0** | Longer clips, smooth movement | Yes — strong fidelity |
| **Sora 2** | Longer duration (up to 20s), style only | No — style/mood reference only |

**Default recommendation: Veo 3.1** for product showcase (best start-frame fidelity, face preserved from still).

### Veo 3.1 video prompt

```
POST /v1/veo31/generate/video
{
  "productId": "YOUR_PRODUCT_ID",
  "prompt": "<video prompt>",
  "startFrame": "<filePath of approved still>",
  "aspectRatio": "9:16",
  "resolution": "720p"
}
```

Video prompt template:
```
[Continuation of the still: the person continues to hold the product / begins speaking / takes a sip / reacts to the product.]
[Natural movement cues — pick 3-4:]
- "briefly glances down at the product then back at camera"
- "slight head tilts while talking, nods along with own words"
- "shifts weight slightly, adjusts grip on the product"
- "raises eyebrows for emphasis mid-sentence"
[Dialogue if any: "She says: '[script line]'"]
[Tone: casual and genuine / excited and warm / confident and direct.]
No subtitles, no captions, no text overlays.
```

Resolution: default `720p` — 4K and 1080p show no visible quality difference for UGC-style content.

---

## Credit cost reference

| Step | Credits | Notes |
|------|---------|-------|
| Still generation (Nano Banana 2) | 24 credits | Per generation |
| Still QA retry | 24 credits | Per retry, max 2 |
| Veo 3.1 video | ~varies | Per generation |
| Kling 3.0 video | ~varies | Per generation |

Always present as estimates. Confirm exact pricing in the Arcads platform.

---

## Common issues

| Issue | Fix |
|-------|-----|
| Hands look wrong | Add "naturally gripping, anatomically correct, five fingers clearly visible" |
| Product unrecognizable | Describe product verbally (color, shape, size) + pass as reference image |
| Person looks too polished / AI | Add skin texture cues: visible pores, undereye shadows, slight unevenness |
| Start frame not preserved in video | Use Veo 3.1 (not Sora 2) which has literal start-frame fidelity |
| Video person looks different from still | Ensure still was uploaded and passed as `startFrame`, not as style ref |

## See also

- [ugc-product-selfie.md](ugc-product-selfie.md) — UGC selfie with character sheet references (not a one-off AI person)
- [ugc-selfie-style.md](ugc-selfie-style.md) — cross-model UGC video prompting guide
- `skills/arcads-external-api/reference.md` — full API reference
