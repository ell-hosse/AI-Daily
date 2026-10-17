# Signal — your daily AI brief

A static site on GitHub Pages (`docs/`). Every morning a scheduled Claude task follows
`DIGEST_INSTRUCTIONS.md`: it researches the top AI news and 12 trending papers across 6 tracks,
writes a ~1-page plain-language summary of each, adds each paper's main figure, and pushes the
new JSON to this repo. No API key and no GitHub Actions needed.

## Setup
1. Create a public repo and upload these files.
2. Settings → Pages → Branch `main`, folder `/docs` → Save.
3. Site: `https://<username>.github.io/<repo>/`
