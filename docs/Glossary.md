# Glossary

## Game terms

- **Beat** — narrative event (e.g. `beatAnnaOffer`, `beatKhozyaika1`). Function in `marina.js` that posts messages, presents reply chips, transitions plot. ~68 beats total в `marina.js:2557-3530`.
- **Surface** — point in game where viral share CTA appears. Hierarchy: lose / rescue (primary), end-of-day / first-project (secondary), win (tertiary).
- **Chip** — reply button player clicks (renderReplyChips). Each chip has id, label, optional cost.
- **Drain** — guaranteed economy events (charger break $60, phone $80, dentist $150, electric $100) that ensure pressure.
- **Rescue** — mid-game crisis save (mum money, hospital, Lena breakdown, father). Each fires once per game when conditions met.
- **Tim 4th wall** — moment где Tim Zinin (real person) appears as character. Day 24 break: "this game IS me".

## i18n terms

- **t(key)** — translate key to current locale string. Defensive: returns `[MISSING:key]` + console.warn if unknown.
- **tArray(key)** — get array (for random-pick text banks).
- **tPick(key)** — random item from array (replaces old `pick(WORK_TEXT)` pattern).
- **tPlural(key, n)** — Intl.PluralRules-aware (one/few/many/other).
- **Fallback chain** — active locale → en → ru → MISSING placeholder.
- **Pseudo-localization** — `?pseudo=1` URL param wraps every key as `⟦key⟧`. Used to find missing extractions visually.

## Cultural adaptation terms

- **Local substitution (D1=B)** — characters/brands/cities adapt per locale. Marina relocates, friends rename, banks/stores swap.
- **Scenario adaptation (D10)** — beat-level rewrite, не просто translation. ~25 beats need NYC/Istanbul/SP-specific narrative.
- **Cultural minefield** — locale-specific risks: race/class (US), religion/gender (TR), regional slang (BR carioca vs paulistano).
- **Mentality framework** — register/tone matching: hustle culture (US), abi/abla warmth (TR), jeitinho (BR).

## Plot/lore terms

- **115-ФЗ** — Russian Federal Law 115 (anti-money-laundering). In game: triggers Marina's bank to freeze account when crypto transaction detected via Krypta scam beat. Localized as IRS 1099 / MASAK / COAF.
- **MASAK** — Turkish Financial Crimes Investigation Board (Mali Suçları Araştırma Kurulu). EN equivalent for crypto-related freeze.
- **COAF** — Brazilian Council for Financial Activities Control (Conselho de Controle de Atividades Financeiras). PT equivalent.
- **PIX** — Brazilian instant payment system. Used in BR locale for cash flow context.

## Analytics terms

- **K-factor** — viral coefficient. K = `referral_game_started / share_platform_clicked`. Target 0.3-0.5 for text narrative game.
- **Surface-aware K** — K-factor segmented by share surface (lose/rescue/win etc). Identifies which moment drives most conversions.
- **Funnel reach** — % of `game_started` sessions that reach a given surface. Lose ~30%, rescue ~20%, win ~5%.
- **Umami event** — privacy-respecting analytics event sent via `umami.track(name, payload)`. 12+ custom events live, 7 viral events planned for SPRINT 51.

## Asset terms

- **"This is Fine" composition** — meme-inspired hero image (SPRINT 51): Marina at laptop in centre, fire 60-70% frame, calm expression. References dog meme.
- **OG preview** — Open Graph image shared automatically when link pasted in TG/LinkedIn/Twitter. Single source: `img/hero/hero_main.webp`.
- **Cache invalidation** — manual force-fetch via @WebpageBot (TG), Post Inspector (LinkedIn), Card Validator (Twitter) after image swap.

## Operational terms

- **Codex review** — independent AI code review via `/codex-review` skill. Required gate for merge of i18n refactor + viral mechanic.
- **Pseudo-loc pass** — `?pseudo=1` testing run to find missed extractions.
- **Native QA** — playtest by native speaker per locale (TR Kaş network, PT Twitter network, EN Tim).
- **Regression gate** — bot playthrough must pass with pixel-identical RU output before merge.
