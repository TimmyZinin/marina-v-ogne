# «Марина в огне» · Terminal Version Anchor

## What this is

This document records the **terminal version anchor** for Marina v Ogne. The terminal-UI version (v1.6a) is preserved forever at a separate URL and git tag so we can always return to it.

## Why

v2.0+ pivots to messenger-UI. But the terminal version is a valid product experience in its own right. Тим explicitly asked to save it as an anchor: «создай некий якорь, который позволит нам вернуться к вот этой версии».

## Locations

### Live URL (preserved)
**https://timzinin.com/marina-terminal/** — serves v1.6a forever, independent of `/marina/`.

### Git tag
**`v1.6a-terminal-anchor`** on commit `5356c19` in `TimmyZinin/marina-v-ogne`.

```bash
# Check out the terminal version locally:
git checkout v1.6a-terminal-anchor
# See the terminal code as it was shipped
```

### Monorepo deploy snapshot
`~/timmyzinin.github.io-tmp/marina-terminal/` — slim deploy copy (same structure as `marina/` but with archived banner).

## Restore to main URL

If we want the terminal version back at `timzinin.com/marina/`:

```bash
# Method 1 — rsync from archived deploy copy
cd ~/timmyzinin.github.io-tmp
rm -rf marina
cp -R marina-terminal marina
# Edit marina/index.html to remove "archived" banner
git add marina
git -c commit.gpgsign=false commit -m "restore: terminal version from anchor"
git push origin main

# Method 2 — rebuild from git tag
cd ~/marina-v-ogne
git checkout v1.6a-terminal-anchor
# Then rsync to ~/timmyzinin.github.io-tmp/marina/
```

## Content of terminal version (what's preserved)

- Sticky 3-line HUD with ASCII progress bars
- Button cooldowns (A Dark Room signature, 2-4 sec per action)
- Status indicator with Braille spinner + verb rotation
- Contract lifecycle: reach_out → qualification → take_project → work_on_project → auto-deliver
- Tim as AI-help-untangle consultant, notebook day 5, automation unlock
- 12-day arc, 8 day-triggered beats, 2 exhaustive endings
- Coffee overdose mechanic
- Passive energy wear
- 15+ text variants per action
- localStorage key `marina-fire:v1.6:state`

## Content NOT in v1.6a (planned for v2.0+)

- Messenger UI (bubbles, contacts sidebar, typing indicator)
- Landing page with hero image
- Intro/exposition scene
- Life event cards (monopoly-style)
- Loan/trust mechanic (adarkroom wanderer pattern)
- Win/lose screens as full windows
- 1h-per-action economy
- Торги negotiation choice tree
- Automation toggle button

---

Maintained by Tim Zinin. Created on v3.7 plan deployment (2026-04-11).
