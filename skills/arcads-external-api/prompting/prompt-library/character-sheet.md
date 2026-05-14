# Character Sheet Generation — 10-image AI influencer workflow

**Use when:** The user wants to create a new AI influencer character from scratch, or needs a consistent set of reference images across angles for an existing character concept.

A character sheet is 10 images of the same person from different angles and expressions. The hero front-view (image 01) anchors identity; all subsequent images use it as a reference to maintain consistency.

## Folder structure

Character sheets are saved to:
```
references/influencers/{name-hair-color-hair-style-feature-eye-color-skin-tone}/
  01-hero-front.jpg       ← primary reference, used in all future generations
  02-three-quarter.jpg
  03-profile-left.jpg
  04-profile-right.jpg
  05-close-up-face.jpg
  06-expression-smile.jpg
  07-expression-shocked.jpg
  08-expression-serious.jpg
  09-three-quarter-back.jpg
  10-full-body.jpg
```

Name convention combines 5 descriptors: `name-hair-color-hair-style-feature-eye-color-skin-tone`

Examples:
- `sofia-dark-curly-beauty-mark-green-tan`
- `marcus-black-fade-scar-brown-deep`
- `jade-blonde-straight-freckles-blue-fair`

---

## Workflow

### Step 1 — Get influencer description

Ask the user to describe the influencer in plain English:

> "Describe your ideal AI influencer. Include: age range, gender, ethnicity/build, hair (color + style), eye color, skin tone, and any distinguishing features (beauty mark, freckles, scar, glasses, etc.). Also: what vibe should they have? (approachable, edgy, aspirational, etc.)"

### Step 2 — Expand to visual prompt

Convert the user's description into a precise visual anchor prompt. Present it for review before generating.

**Visual anchor prompt template:**

```
[Age]-year-old [ethnicity/build] [gender] with [hair color] [hair style] hair, [eye color] eyes, [skin tone description] skin. [Distinguishing feature if any.] [Build: petite / athletic / average / tall and lean / etc.] [Overall vibe: warm and approachable / cool and editorial / energetic and athletic / etc.]

Skin realism (mandatory — always include 2-3):
- visible pores
- slight unevenness in skin tone
- minor undereye shadows
- [add 1 more appropriate for skin tone]

Style: clean portrait, [neutral background color], soft diffused light. Sharp focus on face.
```

Present the expanded prompt to the user:

> "Here's the visual prompt I'll use for the character. Does this match what you had in mind? [prompt]. Confirm and I'll generate the hero image first."

Wait for explicit confirmation before generating.

### Step 3 — Generate hero image (01-hero-front.jpg)

The hero image is the identity anchor. Generate it alone first.

```json
POST /V2/images/generate
{
  "productId": "YOUR_PRODUCT_ID",
  "model": "nano-banana-2",
  "aspectRatio": "9:16",
  "prompt": "[visual anchor prompt] Front-facing portrait, head and shoulders, looking directly at camera. Neutral expression — natural, relaxed, not posed. [Neutral background color] seamless background. Clean, sharp portrait lighting."
}
```

Poll `/v1/assets/{id}` until `status === "generated"`.

### Step 4 — User approves hero image

**Do NOT skip this step.**

Show the hero image to the user and wait for explicit approval:

> "Here's the hero front-view image (01). Does this match the character you had in mind? If yes, I'll generate the remaining 9 angles using this image as the identity anchor. If not, what should I change?"

Only proceed to the remaining 9 images after explicit approval. The hero is the reference for all subsequent generations — if it's wrong, all 9 will be wrong.

### Step 5 — Generate remaining 9 angles

Use the approved hero image as a `referenceImages` anchor for all remaining shots. Fire them **sequentially** (not in parallel) to avoid rate limits.

For each shot, upload a fresh copy of the hero image (re-using the same `filePath` causes 500 errors).

**Shot prompts (use with hero image as first `referenceImage`):**

```
02 — three-quarter:
"[Character description]. Three-quarter angle, face slightly turned to the right. Head and shoulders. Same neutral background. Soft diffused light."

03 — profile left:
"[Character description]. Side profile facing left. Head and shoulders. Same neutral background. Soft diffused light."

04 — profile right:
"[Character description]. Side profile facing right. Head and shoulders. Same neutral background. Soft diffused light."

05 — close-up face:
"[Character description]. Extreme close-up of face, from chin to just above hairline. Fills the frame. Same neutral background. Sharp focus on eyes and skin texture."

06 — expression smile:
"[Character description]. Front-facing. Warm genuine smile showing teeth, eyes crinkling — not a posed model smile. Same neutral background."

07 — expression shocked:
"[Character description]. Front-facing. Shocked/surprised expression — eyebrows raised high, mouth open, eyes wide. Genuine, not overdone. Same neutral background."

08 — expression serious:
"[Character description]. Front-facing. Focused serious expression — direct eye contact, slight jaw tension, no smile. Same neutral background."

09 — three-quarter back:
"[Character description]. Three-quarter view from behind and slightly to the side — back of head visible, face in partial profile. Same neutral background. Shows hair and build."

10 — full body:
"[Character description]. Full body shot, head to toe, front-facing. Neutral outfit — plain fitted [color] t-shirt and jeans. Same neutral background. Shows full build and proportions."
```

Poll each asset after firing. After all 10 are complete, download to the character folder.

### Step 6 — QA across all images

Check the full set for:

- [ ] **Face consistency** — same facial structure, eye shape, features across all 10
- [ ] **Hair consistency** — color and style match across angles
- [ ] **Skin tone consistency** — same tone in all lighting conditions
- [ ] **No anatomy issues** — no distorted ears, misaligned features, neck issues
- [ ] **Expression accuracy** — smile is genuine, shock reads clearly, serious is focused

If any image has a critical issue (wrong face shape, wrong hair), regenerate that angle only.

---

## API call structure

```json
POST /V2/images/generate
{
  "productId": "YOUR_PRODUCT_ID",
  "model": "nano-banana-2",
  "aspectRatio": "9:16",
  "prompt": "<shot-specific prompt>",
  "referenceImages": ["<fresh upload of 01-hero-front filePath>"]
}
```

**Critical:** Upload a fresh copy of `01-hero-front.jpg` for each angle generation. Reusing the same `filePath` causes `HTTP 500 UNKNOWN_ERROR`.

---

## Credit cost

| Operation | Credits |
|-----------|---------|
| Hero image | 24 |
| 9 angle images | 216 (9 × 24) |
| **Full 10-image sheet** | **~240 credits** |
| QA retry (per image) | 24 |

Present as estimate. Confirm exact pricing in Arcads platform.

---

## Common issues

| Issue | Fix |
|-------|-----|
| Face drifts across angles | Ensure hero image is passed as first `referenceImage`; describe face verbally in each prompt |
| Wrong expression on neutral shots | Add "neutral, natural, relaxed — NOT smiling, NOT posed" to prompts 01-05, 09-10 |
| Hair changes color between angles | Add `"[exact hair color and style] unchanged"` to each prompt |
| Skin tone inconsistent | Add skin tone to each prompt; add `"maintain exact skin tone across all lighting conditions"` |
| Hero looks right but angles drift | Add character description to every angle prompt — don't just rely on `referenceImages` |

## See also

- [ugc-product-selfie.md](ugc-product-selfie.md) — using character sheets for UGC product selfies
- [influencer-recreation.md](influencer-recreation.md) — creating a character from a real reference photo (different workflow)
- `skills/arcads-external-api/reference.md` — full API reference
