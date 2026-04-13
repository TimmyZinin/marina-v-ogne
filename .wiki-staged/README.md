# Wiki Pages — Staged for GitHub Wiki

These 4 pages are ready to push to https://github.com/TimmyZinin/marina-v-ogne/wiki

GitHub Wiki requires the first page to be created via web UI before `git clone wiki.git` works.

## To activate:

1. Open https://github.com/TimmyZinin/marina-v-ogne/wiki
2. Click "Create the first page"
3. Save a placeholder (any content)
4. Then locally:

```bash
cd /tmp && rm -rf marina-wiki && \
  git clone https://github.com/TimmyZinin/marina-v-ogne.wiki.git marina-wiki && \
  cp /Users/timofeyzinin/marina-v-ogne/.wiki-staged/Home.md marina-wiki/ && \
  cp /Users/timofeyzinin/marina-v-ogne/.wiki-staged/Architecture.md marina-wiki/ && \
  cp /Users/timofeyzinin/marina-v-ogne/.wiki-staged/Features.md marina-wiki/ && \
  cp /Users/timofeyzinin/marina-v-ogne/.wiki-staged/Changelog.md marina-wiki/ && \
  cd marina-wiki && \
  git add -A && \
  git commit -m "init: full wiki content" && \
  git push
```

## Pages

- `Home.md` — overview + status + quick map (Mermaid)
- `Architecture.md` — file structure, state shape, day cycle (4 Mermaid diagrams)
- `Features.md` — resources, funnel, Tim automation, Khozyaika arc, win/lose (5 Mermaid diagrams)
- `Changelog.md` — sprint history, version timeline (Gantt Mermaid)
