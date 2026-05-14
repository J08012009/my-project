# Seedance 2.0 Product Hero — elemental style guide

**Arcads route:** `POST /v2/videos/generate` with `"model": "seedance-2.0"`
**Use for:** Product-only videos with elemental effects (water, ice, mist, smoke) — no people

Read [seedance-2.md](seedance-2.md) for base platform rules (forbidden words, prompt length, timestamps, etc.) before composing prompts here.

## Core principles

Four pillars define this style:

1. **Product as sole subject** — every shot frames the product. No lifestyle context, no person (except minimal hand-only shots if the prompt explicitly calls for one).
2. **Elemental motion** — water, ice, mist, steam, powder, smoke, light trails. The elements interact with the product.
3. **High-contrast lighting** — dramatic highlights, deep shadows, no flat diffuse light.
4. **Escalating shot sequence** — macro → interaction → dramatic angle → hero composition. Each shot more epic than the last.

---

## 6-layer structure

### Layer 1 — Format header

```
15-second [element]-infused product hero video. [Camera style: macro lens / cinema camera / high-speed slow-motion.] [Mood: energetic / dramatic / premium / raw.]
```

Default to 15s for no-dialogue product hero — maximum visual impact.

### Layer 2 — Product description

Describe precisely. Every detail tells the model what to render.

```
The product: [name] — [shape], [material/finish], [color], [text/label details]. [Current surface state: dry / wet with condensation / frosted / covered in powder.]
```

### Layer 3 — Environment

Backdrop color and surface, plus the elemental effect.

```
[Backdrop: jet black / deep navy / pure white / dark concrete] background. [Surface: matte black platform / wet stone / ice block / glossy dark surface.] [Primary elemental effect: see table below.]
```

#### Elemental effects by product type

| Product type | Primary effect | Secondary effect |
|-------------|----------------|-----------------|
| Beverages / drinks | Water splash, condensation drips | Ice shards, mist cloud |
| Supplements / powders | Powder explosion in motion | Fine particle drift |
| Skincare / serums | Cream swirl, oil droplet | Mist spray, gel bounce |
| Tech / electronics | Electric spark trails, light streaks | Holographic flicker |
| Food items | Steam rising, liquid drip | Crumb burst, oil sizzle |
| Apparel / accessories | Fabric ripple in wind | Dust lift from surface |

### Layer 4 — Shot sequence

Escalate from tight to epic. Describe each shot with camera angle + elemental action.

```
[00:00–00:04] Macro close-up: [extreme detail shot — label text, surface texture, condensation droplet]. [Elemental action starts here — slow drip, first crack of ice, powder begins to settle.]
[00:04–00:09] Interaction shot: [element fully contacts product — wave crashes, powder explodes, mist engulfs]. Camera at [angle]. [Slow motion if possible.]
[00:09–00:13] Dramatic angle: [low angle looking up / 45-degree hero angle]. [Product rotates or elements recede to reveal full product.]
[00:13–00:15] Hero composition: [ideal angle, product perfectly centered or rule-of-thirds]. [Tagline appears.] Camera holds.
```

### Layer 5 — Text overlays

Two text beats maximum for a 15s product hero.

```
Tagline (appears at ~[9-11]s): "[4-8 word punchy tagline]" — centered, [white / gold] text, [font style: bold / elegant serif / clean sans-serif].
End card (appears at ~13s): "[Brand name or CTA — 2-4 words]."
```

Tagline rules:
- 4–8 words maximum
- Active, punchy: "Fuel the mission." / "Zero compromise." / "Engineered to perform."
- NOT a product description — a feeling or identity claim

### Layer 6 — Technical specs

```
[Lighting: dramatic rim light from [direction], [color]. Deep shadows. No flat lighting.] [Camera quality: ultra-sharp, hyper-detailed, macro photography quality.] [Color grade: [desaturated and moody / rich saturated / high contrast monochrome / warm golden hour].] [Audio: [deep bass impact hit / glass resonance / product-specific sound effect — ice cracking, liquid pour] synced to elemental action.] No people, no hands (unless specifically needed), no dialogue, no voiceover.
```

---

## Complete example prompt (15s beverage)

```
15-second water-infused product hero video. High-speed slow-motion cinema camera with macro lens. Dramatic, energetic mood.

The product: Arcads Artificial Cola — tall slim can, matte black with gold and purple lettering. Can is dry at start, then hit by a wall of water.

Jet black background. Matte black elevated platform. Water as the primary element — a wall of water crashes into the can in slow motion.

[00:00–00:04] Extreme macro close-up of the can's label — gold lettering catches rim light. A single condensation droplet forms and rolls slowly down the surface.
[00:04–00:09] A wall of water crashes into the can from the left in ultra-slow motion — water wraps around the can, droplets suspended mid-air catching the light like glass beads.
[00:09–00:13] Low angle hero shot looking up at the can — water recedes, can glistens under rim light. Cool blue light from left, warm amber from right. Camera slowly dollies back.
[00:13–00:15] Hero composition: can perfectly centered, still glistening. Tagline appears in bold white text: "Engineered to perform." Camera holds.

Lighting: cool blue rim from left, warm amber from right. Deep shadows. Specular highlights on water droplets. No flat diffuse light.

Ultra-sharp, hyper-detailed. High-speed slow-motion for water interaction. High contrast, slightly desaturated color grade. Deep bass impact hit synced with the water crash. No people, no hands, no dialogue.
```

---

## Shot sequence templates

### Beverage hero (water/ice)
```
[00:00] Macro: condensation droplet on label → [00:04] Water crash in slow-mo → [00:09] Low hero angle as water recedes → [00:13] Perfect hero + tagline
```

### Supplement hero (powder)
```
[00:00] Macro: powder texture close-up → [00:04] Powder explosion burst in freeze-frame → [00:09] Particles settle around product, dramatic angle → [00:13] Clean hero + tagline
```

### Skincare hero (cream/mist)
```
[00:00] Macro: serum droplet on product surface → [00:04] Mist spray engulfs product in slow-mo → [00:09] Product emerges from mist, 45° angle → [00:13] Glowing hero + tagline
```

---

## Common issues

| Issue | Fix |
|-------|-----|
| Elements look fake/CGI | Add "photorealistic elemental interaction, physically accurate motion" |
| Handheld shake crept in | Explicitly say "locked-off tripod / smooth dolly — no handheld" |
| Tagline appears too early | Specify timestamp for tagline appearance |
| Too many text lines | Max 2 lines for product hero; cut to tagline + brand |
| Product drifts between shots | Add "maintain exact product design, label, and finish across all shots" |

## See also

- [seedance-2.md](seedance-2.md) — base platform rules, forbidden words, prompt checklist
- [seedance-2-premium-reveal.md](seedance-2-premium-reveal.md) — dark void reveal without elemental effects
