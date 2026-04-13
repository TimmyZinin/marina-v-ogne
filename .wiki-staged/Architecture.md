# Architecture

## File structure

```
marina-next/
├── play.html              # Game entry point, all overlays
├── index.html             # Landing page
├── css/marina.css         # 1700 lines — messenger UI, mobile, animations
├── script/
│   ├── marina.js          # 3500 lines — STATE, beats, actions, endings
│   ├── bubbles.js         # 332 lines — chat render, contacts list, chips
│   ├── marina-audio.js    # 350 lines — SFX, soundtrack, finale track
│   └── lead.js            # 200 lines — inline lead form (CTA)
└── img/events/            # 40 webp photos for chat attachments
```

## Module flow

```mermaid
sequenceDiagram
    participant Player
    participant marina.js as marina.js (STATE + actions)
    participant bubbles.js as bubbles.js (render)
    participant audio as marina-audio.js
    participant LS as localStorage

    Player->>marina.js: click dock button
    marina.js->>marina.js: runAction(): isBusy=true, deduct hours/cash
    marina.js->>bubbles.js: postMessage to scratch thread
    bubbles.js->>bubbles.js: appendToThreadHistory + renderBubble
    marina.js->>audio: messagePing()
    marina.js->>marina.js: checkEndings()
    marina.js->>LS: saveState()
    marina.js->>Player: renderDock() → UI updated
```

## State shape

```mermaid
erDiagram
    STATE ||--|| SAVE : persists
    STATE {
        int day
        int hours
        int energy
        int hunger
        int comfort
        int cash
        int leads
        int qualified_leads
        array active_projects
        int delivered_projects
        bool lamp_on
        bool bank_locked
        bool worked_night_last_day
        bool _hangover_active
        array contacts
        object threads
        string current_chat
    }
    STATE ||--o{ contacts : has
    contacts {
        string id
        string name
        string avatar
        bool visible
        int unread
    }
    STATE ||--o{ threads : has
    threads {
        string contact_id
        array messages
    }
    STATE ||--o{ beat_flags : tracks
    beat_flags {
        bool beat_xxx
        bool _xxx_pending
    }
```

## Day cycle

```mermaid
flowchart TD
    A[Day starts: 8h, +energy recovery] --> B{hunger check}
    B -->|<30| C[overnight recovery 5-12]
    B -->|>=30| D[overnight recovery 20]
    C --> E[postMorningMonologue]
    D --> E
    E --> F{hangover_active?}
    F -->|yes| G[hangover bubble + 0.75x debuff]
    F -->|no| H[hunger/sad/tired/fine bubble]
    G --> I[fireDayBeats day]
    H --> I
    I --> J[processPassive: -45 cash, -25 hunger, -10 comfort]
    J --> K{drain event day?}
    K -->|day 3/6/8/11| L[beatDrainCharger/Phone/Dentist/Electric]
    K -->|other| M[Player plays day]
    L --> M
    M --> N[end_day clicked]
    N --> A
```

## Save versioning

```mermaid
flowchart LR
    A[loadState] --> B{ver in COMPATIBLE_VERSIONS?}
    B -->|yes| C[parsed.version = VERSION]
    C --> D[merge missing keys from defaultState]
    D --> E[deep-merge contacts + threads]
    E --> F[return parsed]
    B -->|no| G[return defaultState]
```

## Action pipeline

```mermaid
sequenceDiagram
    participant UI
    participant marina.js as runAction()
    participant Bubbles
    participant State

    UI->>marina.js: click handler
    marina.js->>State: deduct cost (hours, energy, cash)
    marina.js->>Bubbles: showTyping(900ms)
    Note over Bubbles: marina печатает...
    Bubbles->>marina.js: callback after typing
    marina.js->>State: post outgoing/incoming bubble
    marina.js->>State: checkEndings(false)
    marina.js->>State: save()
    marina.js->>UI: renderDock() — buttons enabled
```
