# WAHMD — Human Annotation Guide

Annotation guidelines for the **Women Abuse & Harassment Meme Dataset (WAHMD)**: a multimodal
(image + text) benchmark for detecting misogyny/abuse targeting women in memes, annotated in the
aspect-based sentiment (ACOS/TASD) style.

> **Golden rule:** a meme is **image + text together**. Always judge from **what the image shows
> AND what the text says**, never text alone. The same caption can be abusive or wholesome
> depending on the picture, and vice-versa.

---

## 1. What you annotate per meme

| field | what to decide | values |
|---|---|---|
| `aspect_category` | Which **topic/type** — **this is the class label**; `Non-Abusive` means not abusive | one of the 8 below |
| `sentiment_polarity` | Sentiment/stance **toward the woman target** | `negative` / `neutral` / `positive` |
| `aspect_term` | The main target entity mentioned | e.g. *wife, feminists, single mothers, women, men* — or `NULL` if only shown in the image |
| `opinion_term` | The sentiment-bearing phrase | e.g. *"belong in the kitchen"* — or `NULL` if implicit/visual |

There is **no separate misogynistic 0/1 field** — abusiveness is captured by the category
(`Non-Abusive` vs one of the 7 abuse categories). `aspect_category` + `sentiment_polarity` are
required. `aspect_term`/`opinion_term` are for the ACOS quadruple (fill when clearly present in text).

---

## 2. Step 0 — Inclusion check (skip bad memes first)

Mark **SKIP / exclude** and move on if the image is any of these (they are not usable memes):
- a **screenshot** of a tweet, chat, Reddit post, or comment thread;
- a plain **photograph** or selfie with no meme caption;
- an **infographic**, chart, news graphic, or wall of text;
- a **collage / starter-pack / tier-list / political-compass** grid;
- **too little in-image text** (< ~5 words) to carry meaning;
- **off-topic** — not about women/gender at all (it only matched a keyword);
- **non-English** or unreadable.

Everything that passes the inclusion check gets labeled.

---

## 3. Is it abusive? (an abuse category vs `Non-Abusive`) — the primary decision

Assign one of the **7 abuse categories** if the meme **endorses, normalizes, trivializes, or
approvingly jokes about** any of: hostility, contempt, inferiority, objectification, control, or
violence toward women — *including when it is "just a joke" or ironic/funny*.
**Funny does not mean not-abusive.**

Assign **`Non-Abusive`** if the meme:
- is **supportive/empowering** of women, or **criticizes/mocks** misogyny, harassers, or sexism
  (counter-speech, satire of sexists);
- is **benign gendered humor** — relationships, marriage, dating, gender differences — *without*
  demeaning women;
- targets **men** or something else, not women.

> **Careful — common traps**
> - **Ironic/"edgy" misogyny is still abusive** → an abuse category. "haha women bad, jk".
> - **Satire of misogynists is `Non-Abusive`.** A meme *making fun of* the "get back in the kitchen"
>   guy → Non-Abusive. Read the stance: is the butt of the joke the *woman* (→ abuse category) or
>   the *sexist* (→ Non-Abusive)?
> - **Meta-commentary is `Non-Abusive`** — a meme *about* misogyny discourse that doesn't itself demean women.
> - **Reclaimed slang is `Non-Abusive`** — "gaslight gatekeep girlboss", "girl dinner", "mother is
>   mothering" used positively/neutrally.

---

## 4. `aspect_category` — the 8 topics

Choose the **single best** topic. For `Non-Abusive` memes still pick the topic they engage
(e.g. a body-positivity meme is *Appearance Attack* topic, sentiment positive) or **Non-Abusive**
if there is no specific abuse topic.

1. **Sexual Harassment** — unwanted sexual attention, catcalling, "she was asking for it", victim-
   blaming, objectification framed sexually, rape/consent jokes.
2. **Violence** — physical violence/abuse toward women played for approval or humor
   ("get back in the kitchen *slap*", wife-beating jokes, black-eye jokes).
3. **Misogyny** — general hostility/inferiority/gender-role stereotyping ("women belong in the
   kitchen", "women can't drive", "women logic", "make me a sandwich").
4. **Appearance Attack** — body-shaming, makeup/"catfish", aging/"hitting the wall", ugliness.
5. **Morality** — slut-shaming, "body count", "for the streets", gold-digger-as-immoral, single-
   mother shaming, purity policing.
6. **Character Assassination** — "women lie/manipulate", false-accusation tropes, "crazy ex",
   gold-digger, divorce/alimony framing, "Karen".
7. **Other Abuse** — women-targeted abuse not covered above (women in sports/STEM put-downs,
   "girl math", gender-pay-gap denial, general put-downs).
8. **Non-Abusive** — empowerment, counter-memes, anti-sexism/anti-harassment, wholesome, or benign
   gendered humor (the "hard negatives").

If two apply, pick the **most central** one (the main point of the meme).

---

## 5. `sentiment_polarity` — toward the woman target

Sentiment expressed **toward women / the female target** (not the meme's overall mood):
- **negative** — demeans, attacks, or ridicules women (all abuse-category memes are negative).
- **positive** — praises, defends, uplifts, or celebrates women (empowerment, counter-speech).
- **neutral** — mentions women/gender with no clear pro/anti valence (observational, relatable
  humor, factual).

> An anti-men joke that isn't about women → target is *men*; toward *women* it's usually `neutral`.

---

## 6. `aspect_term` & `opinion_term` (ACOS — fill when explicit)

- **aspect_term**: the exact target span in the **text** (*wife, feminists, single mothers, women,
  Karen, men*). If the target is only shown in the **image** (not written), use `NULL` (implicit).
- **opinion_term**: the exact sentiment-bearing span (*"belong in the kitchen", "gold digger",
  "can't drive"*). If the "opinion" is carried by the **image** (visual), use `NULL` (implicit).

Memes are often implicit — `NULL` is a valid, common answer.

---

## 7. Text fields you'll see

- `post_text` — the poster's caption (Reddit title / tweet). May be empty.
- `ocr_text` — the text **inside** the image (transcription). Use both, but remember `ocr_text`
  *is* part of the image.

---

## 8. Edge cases quick-reference

| situation | label |
|---|---|
| Ironic/funny misogyny ("jk women bad") | Misogyny (or fitting abuse category), negative |
| Mocking a sexist / "kitchen guy" | Non-Abusive (or the topic), positive |
| Body positivity / "all bodies beautiful" | Appearance Attack topic, positive |
| "believe survivors" / anti-harassment | Sexual Harassment topic, positive |
| Empowerment / girl power / women's day | Non-Abusive, positive |
| Wholesome wife/mom, benign dating humor | Non-Abusive, neutral |
| Anti-men / misandry joke | Non-Abusive (target = men), neutral toward women |
| Meta-meme about misogyny discourse | Non-Abusive, neutral |
| Reclaimed slang (girl dinner, girlboss) | Non-Abusive, positive/neutral |
| Screenshot / infographic / collage / off-topic | **SKIP** |

---

## 9. Workflow & agreement

1. Do the **inclusion check** first (Section 2).
2. Decide **abuse vs `Non-Abusive`** (Section 3) — this anchors everything.
3. Pick **`aspect_category`** and **`sentiment_polarity`**.
4. Fill **`aspect_term`/`opinion_term`** if explicit in text.
5. If unsure, flag for a second annotator rather than guessing. Aim for ≥2 annotators per meme;
   resolve disagreements by discussion or majority. Record confidence if your tool supports it.

**When in doubt on abuse vs Non-Abusive:** ask *"would a reasonable woman find this demeaning to
women?"* If the meme relies on a woman being the inferior/ridiculed party for its humor, it belongs
in an abuse category (not Non-Abusive).
