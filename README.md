# ⚡ AI-Daily

**Daily AI news and trending papers in plain English — updated every morning at 6:45 AM Eastern Time (Toronto).**

👉 **Live site: [ell-hosse.github.io/ai-daily](https://ell-hosse.github.io/ai-daily/)**

---

## What you get every morning

**📰 Headlines** — the 8–12 most important AI stories from the last 24 hours (new models, labs, products, chips, policy), each with a short summary and a link to the original article.

**📄 Papers worth your time** — 12 trending research papers, 2 in each of these areas:

| Track | What it covers |
|---|---|
| 🤖 Autonomous Systems | agents, planning, decision-making, multi-agent systems |
| ⚡ Inference Optimization | quantization, KV cache, speculative decoding, serving |
| 🧠 Transformer Optimization | efficient attention, MoE, long context, state-space models |
| 🟩 GPU Kernels | CUDA, Triton, FlashAttention-style kernels, compilers |
| 🦾 Autonomous Robotics | manipulation, locomotion, navigation, VLA policies |
| 👁️ LLM & VLM | language and vision-language models, reasoning, RL |

Each paper comes with:
- its **main figure** from the paper
- a **one-line TL;DR**
- a **~1 A4 page plain-language summary**: the problem · the idea · how it works · results · why it matters · caveats
- links to the **arXiv page, PDF and discussion**

Past issues are kept in an archive — pick any date from the menu at the top right of the site.

## How it works

No servers, no API keys, no cost beyond a Claude plan.

1. A **scheduled Claude task** runs every day at 6:45 AM ET.
2. It follows [`DIGEST_INSTRUCTIONS.md`](DIGEST_INSTRUCTIONS.md): searches the news, finds trending papers on Hugging Face Papers and arXiv, reads them, and writes the summaries.
3. It saves the issue as JSON in `docs/data/` and pushes it to this repo.
4. **GitHub Pages** republishes the site automatically.

## Repo layout

```
docs/
  index.html              the website (single page)
  data/latest.json        today's issue
  data/archive/*.json     every past issue
  data/index.json         list of archive dates
DIGEST_INSTRUCTIONS.md    what the daily task does — edit this to change topics, sources or style
```

## Customizing

Edit `DIGEST_INSTRUCTIONS.md` to change the research tracks, the number of papers, the news sources or the summary style. The next morning's run picks up the change automatically.
