# Daily digest instructions (followed by the scheduled Claude task)

Goal: publish today's issue of the site in `docs/`. Use WebSearch / WebFetch for all research (the shell has no general internet).

## 1. News (8–12 items)
Find the most important AI news from the last ~24h (labs, models, products, policy, funding, chips).
Prefer original reporting (TechCrunch, The Verge, MIT Tech Review, Reuters, Ars Technica, company blogs). One item per story, max 3 per outlet.
Each item: `title`, `url` (the real article URL you saw), `source`, `summary` (1–2 sentences in your own words), `image` (null is fine), `ts` (unix seconds, approximate is fine).

## 2. Papers — 2 per track, 12 total
Tracks (id / name / color):
- autonomous / Autonomous Systems / #22d3ee
- inference / Inference Optimization / #a78bfa
- transformer-opt / Transformer Optimization / #f472b6
- gpu / GPU Kernels / #34d399
- robotics / Autonomous Robotics / #fbbf24
- llm-vlm / LLM & VLM / #fb7185

Where to look: huggingface.co/papers (trending, upvotes), arxiv.org/list/cs.LG|cs.CL|cs.RO|cs.DC|cs.CV/new, alphaxiv / paperswithcode trending.
Prefer papers from the last ~7 days that are getting attention. Never repeat a paper id that appears in any file in `docs/data/archive/`.

For each paper:
- `id` (arXiv id, e.g. 2610.01234), `title`, `authors` (up to 8), `source` ("Hugging Face Trending" or "arXiv new"), `upvotes` (number or 0)
- `tldr`: one sentence, plain English
- `image`: the main figure URL. Fetch `https://arxiv.org/html/<id>` and take the first real figure (usually `.../x1.png`), as an absolute URL. If none, null.
- `abs_url`: https://arxiv.org/abs/<id>, `pdf_url`: https://arxiv.org/pdf/<id>
- `summary_md`: ~450–600 words (one A4 page), plain language for a busy engineer, using exactly these markdown headings:
  `## The problem`, `## The idea`, `## How it works`, `## Results`, `## Why it matters`, `## Caveats`.
  Read the abstract and, when possible, the arXiv HTML intro/results. Explain jargon briefly. No invented numbers. Write in your own words (no copying sentences).

## 3. Write files
`docs/data/latest.json` and `docs/data/archive/<YYYY-MM-DD>.json` (identical), shape:
```json
{"date":"YYYY-MM-DD","generated":"<ISO time>","news":[...],
 "tracks":[{"id":"autonomous","name":"Autonomous Systems","color":"#22d3ee","papers":[...]}, ...]}
```
Then rewrite `docs/data/index.json` as a JSON array of all archive dates, newest first.
Validate with `python3 -c "import json;json.load(open('docs/data/latest.json'))"`.

## 4. Publish
`git add docs/data && git commit -m "Digest YYYY-MM-DD" && git push` to the default branch. GitHub Pages redeploys automatically.
