# Creative Brief Playbook (Arcads)

## 1. Capture the marketing intent (ask the user)

- **Audience:** Who is this for? (one sentence)
- **Job to be done:** What should the viewer feel or do after watching?
- **Offer / proof:** Product name, one concrete benefit, optional social proof.
- **Hook:** First 1–2 seconds—pattern interrupt, curiosity, or relatable moment.
- **CTA:** Exact words if spoken or on-screen (e.g. "Shop the drop," "Book a demo").
- **Constraints:** Length, aspect ratio, banned topics, brand words to avoid.

## 2. Turn intent into a single coherent prompt

- Prefer **one paragraph** of clear direction over a bag of keywords.
- Name the **subject**, **setting**, **camera / motion**, **lighting**, **style**, and **audio mood** when the API or workflow supports audio.
- If the user gave a vague adjective ("premium," "fun"), **translate** into visual specifics.

## 3. Map the brief to Arcads

1. Pick the **API route** using `SKILL.md` decision tree and reference.md.
2. Open the matching **`prompting/prompt-library/*.md`** for the chosen model.
3. Copy required IDs from prior `GET` responses or ask the user.

## 4. Merge with project memory

If `MASTER_CONTEXT.md` lists brand voice, banned phrases, or winning prompts, **prefer those** over generic templates.

## 5. Quality check before sending

- [ ] Required JSON fields present per OpenAPI / reference.md.
- [ ] Prompt matches the **vendor guide style** for the chosen model.
- [ ] No secrets in the request body.
- [ ] User confirmed aspect ratio and duration where enums apply.
