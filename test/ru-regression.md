# RU Regression Test Plan — SPRINT 49 Merge Gate

**Purpose:** Verify that i18n refactor (v2.8.0) does NOT break existing RU gameplay. This is the BLOCKING gate before deploy.

## Manual playthrough checklist (20-30 min)

### Phase 1: Boot sanity
- [ ] Open `/marina-next/play.html?lang=ru` в incognito (clean localStorage)
- [ ] Language overlay appears с 4 кнопками: 🇷🇺 🇺🇸 🇹🇷 🇧🇷
- [ ] Click 🇷🇺 Русский → overlay closes, state persists (`localStorage['marina-fire:lang'] === 'ru'`)
- [ ] Intro overlay text appears in Russian ("Марина только что ушла из агентства...")
- [ ] Click "начать игру" → game starts, contacts sidebar shows Russian names (Лена, Анна, Тим...)
- [ ] DevTools console: zero `[i18n-miss]` warnings

### Phase 2: Core gameplay (days 1-5)
- [ ] Open Лена chat — intro message Russian, preserved exactly as pre-2.8
- [ ] Open Анна chat — offer appears на день 2/3, reply chips (да, беру / подумаю)
- [ ] Click "искать клиентов" — scratch chat shows one of 6 RU outreach texts
- [ ] Click "делать работу" — scratch shows one of 8 work texts
- [ ] Click "поесть дома" — shows one of 5 RU food texts (гречка, макароны etc.)
- [ ] End day 1 → day 2 → morning monologue fires в зависимости от state
- [ ] Dock action labels all Russian: "искать клиентов", "созвон с лидом", "делать работу"...
- [ ] Disable reasons appear on hover: "нет часов", "нет энергии", "нет лидов"...

### Phase 3: HUD + crisis
- [ ] Brand subtitle shows "теледрам v2.8.0-i18n-wip" (or similar version string)
- [ ] Low hunger → subtitle changes to "🍔 очень голодна"
- [ ] Low energy → "⚡ на пределе"
- [ ] Низкий cash → crisis banner shows "💰 БАЛАНС КРИТИЧЕСКИЙ · −$XXX"
- [ ] Let bank get locked via Krypta beat → banner shows "🔒 СЧЁТ ЗАБЛОКИРОВАН ПО 115-ФЗ · ещё N дн."

### Phase 4: Beats (sample 5)
- [ ] **Khozyaika day 1 rent** (day 3-5): Russian verbatim, rent demand
- [ ] **Pavel loan** (day 5-7): "бывший просит $300 в долг", reply chips Russian
- [ ] **Mama medicine** (day 6): "мама просит на лекарства", choice Russian
- [ ] **Olya MLM** (day 8-10): "Оля Петрова (11-Б)", choice chips
- [ ] **Denis hangout** (day 3+): regatta invite, price dialog Russian

### Phase 5: Tim 4th wall (day 15-24)
- [ ] Tim automation intro (day ~15): tier 1 $200 pitch, Russian
- [ ] Tier 2 / Tier 3 upgrades (day ~20/25): Russian dialog
- [ ] **Day 24 Tim creator fired** — 4th-wall break, "Привет. Спасибо большое..." messages in Russian
- [ ] Telegram subscribe chip works → opens t.me/timofeyzinin

### Phase 6: Lead form (day 28)
- [ ] Notebook/блокнот form appears
- [ ] Labels Russian ("как к тебе обращаться", "@telegram (3-32)", "что горит")
- [ ] Submit form — POST sent with `lang: "ru"` (verify in Network tab)
- [ ] Backend returns 200 OK
- [ ] Tim responds in Russian, bank notification Russian, scratch memo Russian

### Phase 7: Endings (pick ONE path)

**Win path:**
- [ ] Survive to day 30 with ≥3 projects, cash ≥0, energy ≥25
- [ ] Win overlay appears: kicker "ПЕРВЫЙ МЕСЯЦ ПРОЙДЕН" Russian
- [ ] Stats template "X проекта сданы · $Y · энергия Z/100" Russian
- [ ] Love ending (if unlocked): 8 Russian paragraphs
- [ ] **Viral share card appears** below narrative with "🔥 Марина в огне" title + URL
- [ ] Click "📱 поделиться" → modal opens with 5 platforms

**Lose path:**
- [ ] Trigger burnout (energy 0, day 20+) or eviction (cash <-1500)
- [ ] Lose overlay shows Russian kicker "МЕСЯЦ НЕ ДОШЁЛ"
- [ ] Reason text Russian
- [ ] Narrative body 4 Russian paragraphs
- [ ] **Viral share card appears** with outcome-aware card

**Rescue path:**
- [ ] Trigger hunger crisis (day 4+, hunger ≤5) OR cash crisis (cash < -800)
- [ ] Rescue overlay: "КРИЗИС" kicker, reason + body Russian
- [ ] Click "📞 позвонить" → rescue accepted
- [ ] **Viral share card appears** in rescue overlay

### Phase 8: Viral mechanic e2e (critical SPRINT 51 check)
- [ ] Prompt asks name (once): enter "TestUser" → saved to localStorage
- [ ] Share modal "📋 Копировать" → toast "скопировано в буфер"
- [ ] Paste content: contains URL `?from=TestUser&challenge=<base64>&lang=ru`
- [ ] Open URL in private browser:
  - [ ] Landing hero eyebrow override: "🔥 TestUser сгорела на дне X..." (or similar)
  - [ ] Click play → game starts
  - [ ] localStorage `referred_by` = "TestUser"
  - [ ] Umami: `referral_landing` + `challenge_viewed` events fire
  - [ ] Play until end → on win/lose `referral_game_started` fires

### Phase 9: Language switching
- [ ] Click footer "🌐 язык" → lang overlay re-opens
- [ ] Switch to 🇺🇸 English → mid-run modal warns "chat history stays in current language"
- [ ] Confirm → new bubbles render in EN, old stay RU
- [ ] Switch back to 🇷🇺 → works bidirectionally

### Phase 10: XSS safety
- [ ] Open `?from=%3Cscript%3Ealert(1)%3C%2Fscript%3E`
- [ ] Assert: no alert fires, hero eyebrow shows escaped text
- [ ] DevTools Elements: no script element injected

## Automated checks (if bot harness available)

SPRINT_15_PLAYTEST.md harness if ресейвовать:
```bash
cd ~/marina-v-ogne/marina-next
# Load game in playwright, run bot through 30 days
playwright-cli open https://timzinin.com/marina-next/play.html?lang=ru
playwright-cli exec-js "localStorage.clear(); location.reload();"
# (Manual clicks via snapshot+click sequence)
```

## Diff check (mechanical)

```bash
# Check all RU strings still render identically
cd ~/marina-v-ogne
git diff 4cc8ee6..HEAD -- marina-next/script/marina.js | grep '^-' | grep -E "'[А-Я]" | wc -l
# Expected: many removals (wrapped in tStr now)
git diff 4cc8ee6..HEAD -- marina-next/script/marina.js | grep '^+' | grep "tStr(" | wc -l
# Expected: similar count — each RU literal has a corresponding tStr() call
```

## Acceptance criteria

**PASS** требует:
- [ ] Full 30-day playthrough completes без JS errors
- [ ] Zero `[i18n-miss]` console warnings
- [ ] All 10 phases pass
- [ ] Network tab shows lead POST with `lang: "ru"`
- [ ] Umami dashboard shows `lang: "ru"` в events
- [ ] Save migration: load pre-2.7.0 save → boots in RU без регрессий

**FAIL** блокирует deploy:
- Any overlay/button shows `[MISSING:key]` placeholder
- Any crash during normal play
- Diff breaking existing user's save (state migration fails)
- Any Cyrillic в console (except in user-generated content)

## Rollback

If test fails post-deploy:
```bash
cd ~/marina-v-ogne
git revert HEAD~5  # revert SPRINT 49 commits
git push origin main
# Redeploy to mirror
```

i18n runtime is additive — removing `i18n/i18n-runtime.js` script tag restores hardcoded RU flow because `tStr()`/`tPickOr()` fall back to RU literals when runtime unavailable.
