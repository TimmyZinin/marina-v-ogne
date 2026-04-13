# Features

## Resources

| Resource | Range | Daily decay | Critical |
|---|---|---|---|
| `cash` | -∞..+∞ | -$45 passive + drain events | <-1500 → game over |
| `hours` | 0..8 | reset to 8 each morning | end_day available always |
| `energy` | 0..100 | overnight recovery 5/12/20 | <30 warns, hunger amplifies |
| `hunger` | 0..100 | -25/day | =0 day4+ → starvation lose |
| `comfort` | 0..100 | -10/day | ≤5 day15+ 30% chance burnout |

## Funnel actions

```mermaid
flowchart LR
    A[reach_out<br/>1h, -5e] -->|hit| B[lead]
    B --> C[brief_lead<br/>1h, -3e]
    C --> D[qualified_lead]
    D --> E[send_offer<br/>1h]
    E --> F{torgi}
    F -->|accept 100%| G[active_project]
    F -->|counter +150 70%| G
    F -->|jzhe +350 40%| G
    F -->|decline| H[lead burned]
    G --> I[work_on_project<br/>2h, -5e]
    I -->|3 work units| J[delivered]
    G --> K[work_night<br/>-15e, -15c]
    K -->|2 work units| J
    J --> L[+final payment]
```

## Tim automation tiers

```mermaid
stateDiagram-v2
    [*] --> Manual: day 1-4
    Manual --> Tier1: day 5 buy auto_reach_out $200
    Tier1 --> Tier2: day 10 buy auto_brief_lead $300
    Tier2 --> Tier3: day 16 buy auto_send_offer $400
    Tier3 --> Day28: 4th wall break — Tim is real
    Day28 --> LeadForm: player submits real lead
```

## Khozyaika arc

```mermaid
stateDiagram-v2
    [*] --> Day1: rent reminder $500/dekad
    Day1 --> Day2: комод dream
    Day2 --> Day3: noise complaint -5c
    Day3 --> Day4: water meter -1h or -5c
    Day4 --> Day5: electric meter -1h or -5c
    Day5 --> Day7: damage + plumber -$50
    Day7 --> Day9: chain letter -1h or -5c
    Day9 --> Day11: tiktok subscription
    Day11 --> Day12: RESCUE — +$500 + sweet
    Day12 --> Day14: sweet beat (flowers)
    Day14 --> Day17: sweet beat (quote)
    Day17 --> Day21: sweet beat (candle for Murka)
    Day21 --> Day22: домовой dream
    Day22 --> Day25: horoscope
    Day25 --> Day27: полнолуние warning
```

## Win/lose conditions

```mermaid
flowchart TD
    A[Day 30 reached] --> B{delivered >= 3?}
    B -->|no| L1[lose: no_traction or burnout]
    B -->|yes| C{cash >= 0?}
    C -->|no| L2[lose: eviction]
    C -->|yes| D{energy >= 25?}
    D -->|no| L3[lose: burnout]
    D -->|yes| E{hunger >= 30?}
    E -->|no| L3
    E -->|yes| F{comfort >= 20?}
    F -->|no| L3
    F -->|yes| W[WIN]
    W --> LE{love_ending_unlocked?}
    LE -->|yes| LW[Love Ending unlock]
    LE -->|no| W
```

## Characters (24)

**Core (7):** Лена, Анна, Тим, Т-Банк, Наталья (хозяйка), Павел, мама, Денис, Светка, Настя

**Spam recurring (6):** Оля Петрова, Кирилл, БРАТ крипта, Артур, Вера Николаевна, сосед

**Spam one-shot (7):** Людочка, OZON курьер, водитель яндекса, студент СПбГУ, Катя, неизвестный номер, женская сила

**System:** scratch (Marina's notes)

## Crisis UX

When resources critical:
- **Crisis banner** top of screen (yellow warn / red crit pulsing)
- **Brand subtitle** dynamic ("🍔 очень голодна", "⚡ на пределе", "💔 грустит")
- **Avatar grayscale** when comfort < 30
- **HUD pills** color transitions green→yellow→red

## Mobile

- Stack layout: contacts list ↔ chat view (slide transition)
- Disabled non-work buttons hidden (shopping/kirill/denis/night)
- "Turn on computer" CTA on contacts list
- Compact dock max-height 44vh
