# Rebuilding the full 5,000 (adding the external images)

This repo ships our **2,900 custom** memes in full, plus our **labels** for the **2,100 external**
rows in `labels_external.csv`. The external images are **not redistributed** (data-use agreements).
To reconstruct the full benchmark, obtain the external images from their official sources and align
by `id`.

## 1. MAMI (SemEval-2022 Task 5) — 1,400 rows (`id` = `mami_<file_name>`)
- Register for and download the MAMI 2022 dataset from the SemEval-2022 Task 5 organizers
  (Multimedia Automatic Misogyny Identification), accepting their data-use agreement.
- Images are named `<file_name>.jpg` in their `training_images/` and `test_images/` folders.
- In `labels_external.csv`, a MAMI row's `id` is `mami_<file_name>` (e.g. `mami_8716` → `8716.jpg`);
  the `split` column tells you which folder. The MAMI transcription (image text) is the `text`
  column in their TSVs.

## 2. Misogynistic-MEME — 700 rows (`id` = `ENG*` / `ENGN*`)
- Obtain the Misogynistic-MEME dataset from its official source under its terms.
- Images are named `res_<id>.jpg` (e.g. `res_ENG01.jpg`, `res_ENGN01.jpg`).

## 3. Align
Join `labels_external.csv` (our unified `misogynistic` / `aspect_category` / `sentiment_polarity`
plus the native label columns) to the source images by `id`, then concatenate with
`index_custom.csv` to get all 5,000 rows.

> We provide our derived labels only; the images and original annotations remain governed by each
> source dataset's license.
