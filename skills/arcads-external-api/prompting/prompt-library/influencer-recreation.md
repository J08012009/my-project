# Influencer Recreation from Reference Image

**Use when:** The user shares a photo of a real person (influencer, themselves, a customer) and wants to recreate their appearance in AI-generated content — stills or video.

This workflow is different from [character-sheet.md](character-sheet.md), which creates a character from a text description. Here, the starting point is an existing photo.

## Workflow overview

1. Analyze the reference photo systematically
2. Compose a prompt from the analysis
3. User approves the prompt before generation
4. Generate the still (with QA)
5. User approves the still
6. Optionally animate to video

---

## Step 1 — Analyze the reference photo

When the user shares a photo, examine it systematically. Do not invent details not visible in the photo.

Analyze in this order:

**Face:**
- Face shape (oval, round, square, heart, etc.)
- Eye shape, color, and spacing
- Eyebrow shape and thickness
- Nose shape and size
- Lip shape, fullness, color
- Jawline and chin
- Cheekbones
- Skin tone (describe precisely: "warm golden-brown," "cool fair with pink undertones," not just "light" or "dark")
- Skin texture and any visible features (freckles, moles, dimples)

**Hair:**
- Color (primary + secondary if highlighted/ombré)
- Length (describe in terms of body: chin-length, shoulder-length, mid-back, etc.)
- Texture (straight, wavy, curly, coily)
- Style (parted how, up/down, specific style name if applicable)

**Body:**
- Build (petite, athletic, average, tall and lean, etc.)
- Approximate height impression if full-body shot

**Clothing and styling:**
- What they're wearing (describe color, type, style)
- Makeup if visible
- Jewelry or accessories

**Lighting and aesthetic:**
- Light source direction and quality (soft, harsh, warm, cool)
- Describe as physics: "diffused daylight from a window to the left" not "beautiful lighting"

**Overall vibe:**
- One sentence: how do they come across? (warm and approachable, cool and editorial, energetic and youthful, etc.)

---

## Step 2 — Compose the prompt

Combine the analysis into a single dense paragraph, 80–150 words. Use specific visual language, not vague adjectives.

**Prompt structure:**

```
[Age]-year-old [gender] with [precise face and hair description — dense, specific]. [Skin tone: specific description, not just "light" or "dark".] [Skin realism: 2-3 texture cues: visible pores, slight unevenness, minor undereye shadows.] [Distinguishing features if any.] [Build.] 

[What they're doing in the image you want to generate — this is where you adapt from the reference, not copy it.]

[Setting/background.]
[Lighting: describe as physics.]
[Style notes.]
Avoid: distorted face, airbrushed skin, generic approximation of features.
```

**Specific visual language vs vague adjectives:**

| Vague | Specific |
|-------|----------|
| "beautiful eyes" | "almond-shaped hazel eyes with visible lash line and slight epicanthal fold" |
| "nice skin" | "warm golden-brown skin with visible pores and slight unevenness in tone" |
| "wavy hair" | "medium-length loose waves, dark brown with subtle warm highlights, parted slightly left of center" |
| "good lighting" | "soft diffused daylight from a window to the left, slight warm cast, minimal shadow on the right side of face" |

**Describe lighting as physics:**
- NOT: "beautiful natural lighting"
- YES: "soft diffused daylight from a window to the subject's left, slight warm cast, minimal shadow falloff on the right"

---

## Step 3 — User approves the prompt

Present the prompt before generating:

> "Here's the visual prompt I'll use to recreate this person. Does this capture them accurately?
>
> [prompt]
>
> Once you confirm, I'll generate the still. You can adjust any description before I fire."

Wait for explicit confirmation.

---

## Step 4 — Generate the still

Upload the reference photo as base64 and pass it to Nano Banana 2.

**Upload the reference photo:**

```bash
# Prepare image (upscale to ≥1080px if needed, convert to JPEG)
python3 - "$REF_PHOTO" "$TMP_PREPARED.jpg" <<'PY'
import sys
from PIL import Image
inp, out = sys.argv[1], sys.argv[2]
img = Image.open(inp).convert("RGB")
w, h = img.size
if max(w, h) < 1080:
    scale = 1080 / max(w, h)
    img = img.resize((int(w*scale), int(h*scale)), Image.LANCZOS)
img.save(out, "JPEG", quality=92)
PY

# Get presigned URL
PRESIGN=$(curl -sS -X POST \
  -H "Authorization: $ARCADS_BASIC_AUTH" \
  -H "Content-Type: application/json" \
  -d '{"fileType":"image/jpeg"}' \
  "https://external-api.arcads.ai/v1/file-upload/get-presigned-url")

PRESIGNED_URL=$(echo "$PRESIGN" | python3 -c "import json,sys; print(json.load(sys.stdin)['presignedUrl'])")
FILE_PATH=$(echo "$PRESIGN" | python3 -c "import json,sys; print(json.load(sys.stdin)['filePath'])")

# PUT to S3
curl -sS -X PUT \
  -H "Content-Type: image/jpeg" \
  --data-binary "@$TMP_PREPARED.jpg" \
  "$PRESIGNED_URL"
```

**Generate:**

```json
POST /V2/images/generate
{
  "productId": "YOUR_PRODUCT_ID",
  "model": "nano-banana-2",
  "aspectRatio": "9:16",
  "prompt": "<composed prompt>",
  "referenceImages": ["<filePath of uploaded reference>"]
}
```

Poll `/v1/assets/{id}` until `status === "generated"`.

---

## Step 5 — Internal QA (before showing user)

Check for:

- [ ] **Face similarity** — does it look like the reference person? Key features preserved?
- [ ] **Skin tone match** — consistent with reference?
- [ ] **Hair match** — color, length, and style correct?
- [ ] **No distortion** — face anatomy looks human
- [ ] **Skin realism** — not airbrushed/plastic

If significant drift: retry up to **2 times** with adjusted prompt. Common fixes:
- More specific face description (add exact feature descriptions you may have left vague)
- Mention distinguishing features more prominently in the prompt
- Adjust or remove competing style cues

---

## Step 6 — User approval

Show generated still alongside the original reference:

> "Here's the AI recreation next to the original reference.
>
> [Side by side or sequential display]
>
> How does the likeness feel? Would you like to refine anything (expression, framing, setting)? Or ready to animate to video?"

**Do NOT proceed to video without explicit approval.**

---

## Step 7 — Save the prompt for future reuse

After approval, note the approved prompt in `MASTER_CONTEXT.md` under the influencer entry. Keep the core description "frozen" — vary only pose, expression, setting, or outfit for future uses.

Example `MASTER_CONTEXT.md` entry:

```markdown
### [Person name / handle]
**Approved still prompt (core — frozen):**
"27-year-old woman with medium-length loose dark brown waves with warm highlights, parted left of center. Almond-shaped hazel eyes. Warm golden-brown skin with visible pores, slight unevenness in skin tone, minor undereye shadows. Small mole above the right lip. Athletic build, average height. [Continue with whatever settings/lighting were in approved prompt...]"

**Approved still asset ID:** [id]
**Date generated:** [date]
```

---

## Step 8 — Animate to video (optional)

Upload the approved still and use it as `startFrame` for Veo 3.1:

```json
POST /v1/veo31/generate/video
{
  "productId": "YOUR_PRODUCT_ID",
  "prompt": "<video prompt with movement cues>",
  "startFrame": "<filePath of approved still>",
  "aspectRatio": "9:16",
  "resolution": "720p"
}
```

Include 3-4 natural movement cues (see [ugc-selfie-style.md](ugc-selfie-style.md) for the full cue library). End every video prompt with: `"No subtitles, no captions, no text overlays."`

---

## Credit cost

| Step | Credits |
|------|---------|
| Still generation | 24 |
| QA retry (up to 2) | 24 each |
| Veo 3.1 video | varies |

Present as estimates. Confirm exact pricing in Arcads platform.

---

## Common issues

| Issue | Fix |
|-------|-----|
| Face doesn't match reference | More specific feature descriptions; mention distinguishing features (mole, scar, freckles) prominently |
| Skin tone drifts | Add precise skin tone language: "warm golden-brown" not just "tan" |
| Hair wrong color | Add exact color: "dark brown with subtle warm caramel highlights" |
| Looks generic | The prompt may be too vague — add 2-3 specific distinguishing features from the reference |
| Video face drifts from still | Use `startFrame` with Veo 3.1 (not Sora 2 which treats image as style ref only) |

## See also

- [character-sheet.md](character-sheet.md) — creating a character from text description (no reference photo)
- [ugc-product-selfie.md](ugc-product-selfie.md) — UGC selfie with character sheet
- [ugc-selfie-style.md](ugc-selfie-style.md) — cross-model UGC video prompting
