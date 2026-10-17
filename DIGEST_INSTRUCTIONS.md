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
- `summary_md`: ~550–700 words (one A4 page). See "How to write the summary" below.

### How to write the summary
**Reader:** a smart, curious person who is NOT an expert in this paper's sub-field (think: a good engineer from a different area, or a first-year grad student). They should finish it truly understanding what was done and why it matters — detailed, but never confusing.

**Research first.** Read the abstract AND the arXiv HTML version (intro, method, main results, limitations). Don't summarize from the abstract alone; the detail comes from the body of the paper.

**Use exactly these markdown headings:**
- `## In one sentence`: what the paper does, in words a non-expert gets instantly.
- `## Background you need`: 2–4 short sentences giving the minimum context: what this area is about and the key terms the rest of the summary relies on, each defined simply.
- `## The problem`: what is broken, slow, expensive or missing today, and why people care. Make it concrete (who is affected, what it costs).
- `## The idea`: the core insight, explained with an everyday analogy or comparison (e.g. "like a librarian who…").
- `## How it works`: 3–5 numbered steps walking through the method in plain words. Keep the important specifics (what the model sees, what it changes, what is trained), but explain each one.
- `## Results`: the main findings with real numbers from the paper, and what each number means in practice (e.g. "2× faster means a reply that took 4 seconds now takes 2"). Say what it was compared against.
- `## Why it matters`: who benefits and what this could change in real products or research.
- `## Caveats`: honest limits: what wasn't tested, costs, open questions.
- `## Key terms`: a short bulleted mini-glossary (3–6 terms) with a one-line plain definition each.

**Style rules**
- Short sentences (aim under 20 words). Short paragraphs (2–4 sentences). Active voice.
- Every technical term gets explained in plain words the first time it appears, e.g. "the KV cache (the model's short-term memory of what it has already read)".
- Prefer concrete examples over abstract statements. Use at least one analogy.
- No unexplained acronyms, no math notation, no hype words ("revolutionary", "game-changing").
- Never invent numbers or claims; if the paper doesn't say, don't say it.
- Write entirely in your own words (no copied sentences from the paper).
- Before saving, reread it as the non-expert reader: if any sentence would make them stop and google something, rewrite it.

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
