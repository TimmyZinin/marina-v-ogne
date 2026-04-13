# 🔥 Марина в огне

Survival-мессенджер про 30 дней фаундера. Игрок управляет Мариной — копирайтером, ушедшей из агентства, у неё $500, 12 дней до первой аренды, и три проекта надо закрыть до конца месяца.

**Live:** https://timzinin.com/marina-next/play.html
**Stack:** vanilla JS + jQuery, single-file game logic, telegram-style messenger UI
**Fork:** [doublespeakgames/adarkroom](https://github.com/doublespeakgames/adarkroom) (MPL-2.0)
**Deploy:** GitHub Pages → timzinin.com/marina-next/

## Pages

| Page | What's inside |
|------|---------------|
| [Home](Home) | This page — overview |
| [Architecture](Architecture) | File structure, state, modules |
| [Features](Features) | Mechanics, characters, beats |
| [Changelog](Changelog) | Sprint history, version timeline |

## Quick map

```mermaid
flowchart LR
    A[index.html<br/>landing] --> B[play.html<br/>game shell]
    B --> C[script/marina.js<br/>3500 lines<br/>game logic]
    B --> D[script/bubbles.js<br/>messenger render]
    B --> E[script/marina-audio.js<br/>SFX + music]
    B --> F[script/lead.js<br/>inline form]
    B --> G[css/marina.css<br/>1700 lines]
    C --> H[(localStorage<br/>marina-fire:v2.0)]
    C --> I[img/events/<br/>40 webp photos]
```

## Status

- **Version:** 2.2.3
- **Last sprint:** SPRINT 14.4 (hygiene)
- **Active arc:** 30-day month, win/lose conditions
- **Characters:** 24 contacts (7 core, 6 recurring, 7 spam, 4 parallel arc)

## Game arc

```mermaid
stateDiagram-v2
    [*] --> Day1: lamp on
    Day1 --> Day12: economy drains $390 + rent $500
    Day12 --> Day14: Khozyaika rescue (+$500, mood swing)
    Day14 --> Day30: 2nd half — projects, love arc, partnerships
    Day30 --> Win: delivered≥3, cash≥0, energy≥25, hunger≥30, comfort≥20
    Day30 --> Lose: any condition fails
    [*] --> Lose: cash<-1500, hunger=0 day4+, comfort≤5 day15+
```
