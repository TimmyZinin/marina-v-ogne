# 🔥 Марина в огне

Браузерная survival-игра-мессенджер про первый месяц фаундера контент-студии. Лид-магнит для консультаций Тима Зинина по AI-автоматизации бизнеса.

**Live:**
- **v2.1.1 canary (latest):** https://timzinin.com/marina-next/play.html
- **Landing:** https://timzinin.com/marina-next/
- **v1.6a terminal (legacy lead-producing):** https://timzinin.com/marina/
- **Terminal archive:** https://timzinin.com/marina-terminal/

## О проекте

«Марина в огне» — fork [A Dark Room](https://github.com/doublespeakgames/adarkroom) (Michael Townsend / Doublespeak Games, MPL-2.0), переработанный в narrative survival-симуляцию первого месяца фаундера + встроенная механика лидогенерации. Tим Зинин играет роль in-game consultant который разблокирует автоматизации бизнеса и в финале ломает 4-ю стену.

## v2.1.1 — Текущая версия (SPRINT 06)

### Game loop

30 дней. 8 часов в день. $500 на старте. 4 ресурса: **часы / энергия / еда / комфорт**. Три проекта нужно сдать до конца месяца, иначе lose.

### Что в игре

- **22 контакта в Telegram-стиле мессенджере** (Лена, Анна, Тим, Т-Банк, Наталья Валерьевна, Павел (бывший), мама, Денис, Светка-подружка + 13 spam-контактов: Оля Петрова, Кирилл, Krypta, Артур, Вера, сосед, Людочка, OZON, таксист, студент, Катя, свекровь, марафон)
- **Мессенджер UI** с 4 folder tabs: все / 🎯 воронка / 👥 команда / 💰 деньги
- **Top resource HUD** — 6 pills (day/hours/cash/energy/hunger/comfort) с цветом thresholds
- **Funnel particles** (Game Dev Tycoon style) — клик на «искать клиентов» выпускает синие и красные particles по воронке до cash pill
- **4 автоматизации от Тима** — $200 / $300 / $400 / $500 tiers, каждая добавляет passive generation в processPassive
- **115-ФЗ bank lock** — если перевести $100 БРАТ крипте, счёт блокируется на 6 дней → Кирилл приглашает бесплатно → plate_girl_count
- **Khozyaika 6 beats** — rent reminder day 1, komod dream day 2, счётчики 4, тикток 11, rescue 12, кошка 18, гороскоп 25
- **Svetka подружка** — 7 голосовых сообщений с абсурдными сплетнями про бывших и гадания
- **Kirill love arc** — если правильно общаться с Кириллом из Tinder, к day 30 признание + win overlay LOVE ENDING
- **Payвел (бывший)** — шлёт сообщения каждые 2-3 дня до появления Кирилла
- **Contract deadlines** — проекты имеют deadline_day, просрочил → 40% clawback, 60% missed
- **Newest-first chat thread** — новые сообщения сверху, старые уходят вниз
- **4th wall break** — на day 28 Тим пишет «это не персонаж, это реально я» + lead form

### Арт
10 cinematic photoreal hero images через OpenAI gpt-image-1.5 (hero_main, hero_portrait, hero_desk, hero_bedroom, marina_hero, marina_avatar + 11 event photos через Flux).

### Саундтрек
4 оригинальных инструментальных трека в Suno:
1. «Двенадцать дней до конца месяца» (main theme)
2. «Потолок не падает» (rotation)
3. «Обычный вторник» (rotation)
4. «Тридцать дней до потолка» (finale — играет с day 29+)

## Версии

| URL | Версия | Назначение |
|-----|--------|-----------|
| `/marina/` | v1.6a terminal | Рабочий stable lead-producing (не трогать) |
| `/marina-terminal/` | v1.6a archive | Архив terminal версии |
| `/marina-next/` | v2.1.1 | Landing + Canary flagship |
| `/marina-next/play.html` | v2.1.1 | Сама игра |

## Стек

- Vanilla JS + jQuery 1.10 (наследуется от A Dark Room)
- Zero build step
- GitHub Pages-compatible (deploy via rsync to `timmyzinin.github.io-tmp`)
- localStorage save state (`marina-fire:v2.0:state` + version check `2.1.1` auto-wipe старых saves)
- Lead submission через FastAPI proxy `https://marshall.timzinin.com/quest-api/lead`, archetype `marina-v20a`
- OpenAI gpt-image-1.5 для hero art
- Pollinations.ai (Flux) для event photos
- Suno AI для саундтрека

## Architecture

```
marina-next/
├── index.html              # Landing page (cinematic hero + gallery + feature grid)
├── play.html               # Game shell (messenger UI + action dock + HUD)
├── css/
│   ├── marina.css          # Game styles (chat bubbles, HUD, dock, particles)
│   └── landing.css         # Landing page styles
├── script/
│   ├── marina.js           # Game logic (state, beats, actions, endings)
│   ├── bubbles.js          # Messenger rendering (contacts, chat, threads)
│   ├── marina-audio.js     # Playlist + finale track (Web Audio API SFX)
│   └── lead.js             # Lead form submission
├── img/
│   ├── hero/               # 4 cinematic hero key arts (gpt-image-1.5)
│   ├── chars/              # Marina avatar + hero portrait
│   └── events/             # 11 event photos (Flux via Pollinations)
└── audio/
    ├── soundtrack.mp3      # 12 дней до конца месяца (main theme)
    ├── soundtrack_2.mp3    # Потолок не падает
    ├── soundtrack_3.mp3    # Обычный вторник
    └── soundtrack_4.mp3    # Тридцать дней до потолка (finale day 29+)
```

## Game Design

### Ресурсы
- **Hours** (часы) — 0-8 в день, тратятся на actions
- **Energy** (энергия) — 0-100, decay при усталости, eat восстанавливает
- **Hunger** (еда) — 0-100, decay 20/day. <30 → −15⚡ penalty. 0 → lose «слегла от голода»
- **Comfort** (комфорт 💚) — 0-100, decay 8/day. Еда, одежда, свидания, Светкины сплетни поднимают. <30 → impulse spending, breakdown risk
- **Cash** (деньги) — $500 старт. Daily drain $45. Rent $500 на day 10/20/30.
- **Leads / Qualified / Active Projects / Delivered** — воронка

### Экономика
- Анна offer day 5 ($200 upfront + $250 final, 3 work units, 6-day deadline)
- Anna referral day 21 ($350 upfront + $450 final, 3 units, 7-day deadline)
- Cold leads: torg с бюджетом $200-300+
- Artur ex-boss day 15 (40% chance $800 project)
- **Khozyaika rescue day 12** — refund $500 rent с абсурдным оправданием (гарантирован)
- **Lena lifeline** после day 14 если cash < 0 — one-time $300
- Rent $500 × 2 (day 10/20), food $150 (day 7), daily drain $25/day

### Win conditions
- day > 30 AND delivered ≥ 3 AND cash ≥ 0 AND energy ≥ 25 AND hunger ≥ 30 AND comfort ≥ 20

### Lose conditions
- cash < −1500 → eviction
- hunger == 0 AND day ≥ 4 → starvation
- comfort < 10 AND day ≥ 15 → breakdown (random chance)
- day > 30 AND delivered < 3 → no_traction

## Лицензия

Mozilla Public License 2.0 — см. [LICENSE.md](LICENSE.md) и [NOTICE](NOTICE).

**Важно:** это модифицированное произведение. Модифицированные файлы помечены заголовком со ссылкой на MPL 2.0. Audio assets оригинального A Dark Room удалены из этого fork'а.

## Credit

Спасибо Michael Townsend и Doublespeak Games за A Dark Room. Музыка: Тим Зинин через Suno AI. Art: OpenAI gpt-image-1.5, Flux via Pollinations. Code: Claude Opus 4.6.

## Development

```bash
# Локальный запуск
cd marina-v-ogne
python3 -m http.server 8080
# → http://localhost:8080/marina-next/play.html

# Deploy
rsync -av marina-next/ ~/timmyzinin.github.io-tmp/marina-next/
cd ~/timmyzinin.github.io-tmp && git add marina-next && git commit && git push
```

## Changelog

- **v2.1.1 (SPRINT 06)** — Economy tighten, Tim automation arc (4 tiers), Svetka contact, Pavel frequency increase, Khozyaika rent reminder day 1, night work no-hours fix, folder «прочее» removed (spam in «все»), newest-first threads, text banks 5×per action
- **v2.1.0 (BLOCKS A-N)** — 30-day arc, 13 individual spam, food+comfort, top HUD, button badges, bank pinned, 115-ФЗ lock, funnel particles, contract deadlines, Tim 4th wall break, Khozyaika rescue day 12, hotfix hunger wrap
- **SPRINT 01** — Kirill Love Arc (affection + 3 beats + win bonus card)
- **SPRINT 02** — Finale track «Тридцать дней до потолка» day 29+
- **SPRINT 03** — Telegram link preview polish (og:image 1536×1024, twitter summary_large_image)
- **SPRINT 05** — Mobile layout rebuild, HUD moved to bottom dock, contrast fix
- **v2.0b4** — Humor spam dialogues (13 stranger one-shots)
- **v2.0b3** — 2nd night freeze fix, messenger redesign, real soundtrack
- **v2.0b2** — Photos + audio + landing + modern touches
- **v2.0b1** — 4 chars + brand + night overlay + folder tabs
- **v2.0a** — Messenger UI pivot
- **v1.6a** — Terminal UI lead-producing (still live at `/marina/`)
- **v1.5** — Terminal + 12-day arc + inline lead form
- **v1a** — Initial A Dark Room fork

## QA matrix

- Chrome/Edge latest (desktop + mobile viewport 375×812)
- Safari latest (desktop + iOS)
- Firefox latest (desktop)
