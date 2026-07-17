# WAHMD — Women Abuse & Harassment Meme Dataset

A multimodal (image + text) benchmark for detecting **misogyny / abuse targeting women in memes**,
annotated in the aspect-based sentiment style (ACOS / TASD). **5,000 memes** labeled across
**8 categories** (7 abuse types + Non-Abusive) with sentiment — there is no separate binary label,
the category *is* the class (`Non-Abusive` marks the non-abusive memes).

**Category distribution (5,000):** Sexual Harassment 829 · Violence 829 · Misogyny 829 ·
Appearance Attack 828 · Non-Abusive 828 · Character Assassination 380 · Other Abuse 288 ·
Morality 189. **Sources:** custom (ours) 2,500 · MAMI 2,055 · Misogynistic-MEME 445.
**Sentiment:** negative 4,082 · neutral 764 · positive 154 (abuse categories are negative by
definition; positive/neutral come from Non-Abusive).

> ⚠️ **Content warning:** this dataset contains misogynistic, sexist, and abusive material,
> included solely for research on detecting and mitigating online abuse.

## What's in this repo
| path | contents |
|---|---|
| `images/` | **2,500 custom meme images** (our own Reddit/X collection) |
| `text/` | post text for each custom meme (`<id>.txt`) |
| `index_custom.csv` | the 2,500 custom rows with full labels + file pointers |
| `labels_external.csv` | our labels for the **2,500 external rows** (MAMI 2,055 + Misogynistic-MEME 445), keyed by source id — **images not included** (see below) |
| `ANNOTATION_GUIDE.md` | human annotation guidelines |
| `MERGE_EXTERNAL.md` | how to obtain the external images and rebuild the full 5,000 |

## Why the external images aren't here (important)
The 5,000-meme benchmark draws 2,500 rows from two third-party datasets:
- **MAMI** (SemEval-2022 Task 5) — 2,055 rows
- **Misogynistic-MEME** — 445 rows

Both are released under **data-use agreements that prohibit public redistribution of their
images.** So this repo ships **only our labels for those rows** (by their public ids) plus
instructions to fetch the images from the official sources and align them. See `MERGE_EXTERNAL.md`.

Our **custom 2,500 memes are included** in full.

## Labels (see `ANNOTATION_GUIDE.md` for definitions)
- `aspect_category` — **the class label**: one of 8 topics — Sexual Harassment, Violence, Misogyny,
  Appearance Attack, Morality, Character Assassination, Other Abuse, **Non-Abusive** (the last marks
  non-abusive memes; there is no separate binary label).
- `sentiment_polarity` — negative / neutral / positive toward the woman target.
- `aspect_term`, `opinion_term` — ACOS spans (custom; `NULL` when implicit/visual).
- `post_text` (explicit caption) and `ocr_text` (in-image transcription) are separate fields.
- `verification` — `human` (eyeballed) vs `auto-screened` (image-filtered via CLIP + OCR + topical
  gates, not individually eyeballed). Use `misogynistic` as the primary label; fine categories for
  auto rows in the weaker classes are ~95% clean, not 100%.

## How it was built
Harvest (Reddit/X) → perceptual-hash dedup → **image-content filter (CLIP: drop screenshots/
photos/infographics/collages)** → **in-image-text filter (OCR ≥ 5 words)** → topical + junk-class
gates → balance. External sets merged with their native labels; the non-misogynistic class is
drawn from our reviewed custom + Misogynistic-MEME (MAMI negatives are noisier).

## Licensing & takedown
Custom memes remain the property of their original creators and are provided for **non-commercial
research** under fair-use principles. If you are a rights holder and want a meme removed, open an
issue. External datasets are **not** redistributed here — obtain them from their official sources
under their respective agreements.

## Citation
If you use WAHMD, please cite this repository, and cite **MAMI** (Fersini et al., SemEval-2022
Task 5) and **Misogynistic-MEME** if you use the external portion.
