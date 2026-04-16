# Changelog

Reverse-chronological. Newest at top.

## 2.8.0 (in progress) — SPRINT 49 + 51

### SPRINT 51 (viral mechanic) — shipped

- **Add:** `script/viral.js` (330 lines) — surface-aware emoji card generator, share modal with 6 platform intents, URL params (`?from=` referrer, `?challenge=` base64-encoded stats)
- **Add:** Alice→Bob→Charlie referral loop — landing hero auto-override с outcome-aware copy
- **Add:** 4 emoji card templates per surface (end_of_day / rescue / lose / win)
- **Add:** Hooks in `marina.js` — share CTA on win/lose/rescue overlays (primary surfaces > funnel-gated win only)
- **Add:** 7 new Umami events (share_card_rendered/viewed/copied, share_platform_clicked, referral_landing/game_started, challenge_viewed)
- **Add:** viral.* i18n namespace in ru.json + en.json (~30 keys)
- **Add:** CSS — modal, toast, in-overlay share block, lang overlay, lang switcher nav

### SPRINT 49 (i18n infra + EN) — shipped

- **Add:** `i18n/i18n-runtime.js` — `MarinaI18n.{t,tArray,tPick,tPlural,init,setLang,getLang,detectSystem}`
- **Add:** `i18n/ru.json` — source of truth, **~760 leaf keys** across namespaces: lead / bubble / contact / text / action / brand / crisis / system / ui / overlay / meta / landing / beat / rescue / ending / viral
- **Add:** `i18n/en.json` — full EN NYC/Brooklyn cultural adaptation (Marina → Marina (Brooklyn), Т-Банк → Chase, 115-ФЗ → IRS 1099 review, Лена → Lucy, Денис → Denis, Кирилл → Chris, Оля Петрова 11-Б → Lily class of '18, OZON → DoorDash, Яндекс → Uber, доширак → instant ramen, Рив Гош → Sephora, парк горького → Prospect Park, регата → Hamptons sailing trip)
- **Add:** Lang resolution — URL `?lang=` → localStorage → navigator → 'en' fallback
- **Add:** `lang` field in lead payload (backend verified accepts ✅)
- **Refactor:** `lead.js` — all RU literals → `t()` calls с defensive RU fallback
- **Refactor:** `bubbles.js` — chat headers, empty states, funnel labels, contact name lookup
- **Refactor:** `marina.js` — 217 of 234 extraction edits applied (93% coverage):
  - Text banks (19 callsites via `tPickOr()`)
  - renderDock (12 action labels + costs + disable reasons)
  - renderBrandStatus (5 states + version)
  - renderCrisisBanner (7 messages with `{daysLeft}` / `{absCash}` interpolation)
  - Beat-functions (anna, lena, tim_creator_fired 4th-wall, khozyaika 11 beats, pavel 9, mama 4, denis 6, olya, krypta, nastya, kirill love arc 10)
  - Endings (win/lose_burnout/lose_eviction/lose_no_traction/love 8-paragraph epilogue)
  - Rescues (mama_money, hospital, lena_breakdown, father)
  - System callbacks, bank unlocks, contract clawbacks, anna/nastya chip flows
  - `track()` wrapper auto-injects `lang` into every Umami event
- **Refactor:** `play.html` — full data-i18n attributes + lang-overlay + footer lang switcher + bootstrap MarinaI18n.init()
- **Refactor:** `index.html` — full data-i18n coverage + lang `<select>` switcher + auto-detect head script
- **Deferred:** 17 array/object edits (RESCUE_CONFIG, SVETKA arrays, ONESHOT_SPAM bubbles, khozyaika post12) — fall back to RU for those specific strings в non-RU locales

### Blocked / Pending

- **🚫 SPRINT 50 TR/PT:** agents running async in background — tr.json / pt.json generation
- **🚫 Wiki bootstrap:** repo not accessible until Тим manually initializes at github.com/TimmyZinin/marina-v-ogne/wiki → Create first page. 9 pages prepared in docs/wiki-pages/ ready to copy.
- **🚫 Hero image regen:** Gemini nano-banana "This is Fine" composition pending (needs API access + Тим approval iterations)
- **🚫 RU regression playthrough:** manual/bot test pending before production deploy
- **🚫 Native playtester QA:** TR + PT need 1-2 native playtesters per locale

## 2.7.0 — SPRINT 48 (2026-04-14)

- **Change:** New `win_love.webp` art via Gemini 2.5 Flash Image
- **Add:** Win-overlay love-bonus rewrite — 9 paragraphs, "two years later" Marina AI studio narrative

## 2.6.x — SPRINT 38-46 (2026-04-12 → 2026-04-14)

- SPRINT 46: Fix HUD clock vs chat timestamp desync
- SPRINT 43: Self-hosted Umami analytics — 6 new events (intro_dismissed, chat_opened, reply_chosen, action_used, project_delivered, landing_cta_clicked)
- SPRINT 42: Win polish — confetti + earlier music
- SPRINT 41: Tim formal 4th wall + TG subscribe + Kirill day 29 morning
- SPRINT 40: Mutual exclusion: day work XOR night work
- SPRINT 39: Olya retry/final chips + krypta_wallet regen
- SPRINT 38: Kirill scenes context-aware

## 2.5.x — SPRINT 31-37

- SPRINT 37: Pinned scratch chat (Telegram-style sticky)
- SPRINT 36: Kirill brings dinner if Marina ignores him
- SPRINT 35: Eat anytime (evening meal free of work hours)
- SPRINT 34: UX clarity + economy easing + night work visibility
- SPRINT 33: Denis raises comfort + energy
- SPRINT 32: Custom HUD tooltip popup (touch + hover)
- SPRINT 31: Realistic founder day + rent progress bar
