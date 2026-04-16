# Changelog

Reverse-chronological. Newest at top.

## 2.8.0 (in progress) — SPRINT 49 i18n + EN

- **Add:** i18n infrastructure — `i18n/i18n-runtime.js`, `i18n/ru.json` (~250 keys initial)
- **Add:** `MarinaI18n` global API — `t/tArray/tPick/tPlural/init/setLang/getLang/detectSystem`
- **Add:** Lang resolution chain — URL `?lang=` → localStorage → navigator → fallback
- **Add:** `lang` field в lead payload (POST `marshall.timzinin.com/quest-api/lead`) — backend verified ✅
- **Refactor:** `script/lead.js` — all RU literals → `t()` calls с defensive RU fallback
- **Refactor:** `script/bubbles.js` — chat headers / empty states / funnel labels / contact name lookup
- **Pending:** `script/marina.js` heavy refactor (4930 lines, 945 Cyrillic)
- **Pending:** `play.html` + `index.html` — data-i18n attrs + lang overlay
- **Pending:** `i18n/en.json` — EN content with NYC/Brooklyn cultural adaptation
- **Pending:** RU regression playthrough (merge gate)

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
