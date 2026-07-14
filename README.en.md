# SpotCount — field observation and headcount tool

Field tool for counting and qualitative observation of how a public space
is used, originally developed for the Jardin du Peyrou (Montpellier,
France) as part of the **Art of Darkness (AOD)** project, WP4. The tool
is generic: the map, legend and usage checklist are all customisable, so
it can be reused for any other site or observation protocol.

*French version: [README.md](README.md) — License: [LICENSE](LICENSE) (MIT) — Version history: [CHANGELOG.md](CHANGELOG.md)*

## Authors and contributors

- **Claire Bédé** — M1 student in Cognitive Psychology
  and Human Factors Engineering (PCIFH), Université Paul-Valéry
  Montpellier 3 — designed and built the tool and observation protocol,
  internship within the AOD project (WP4)
- **Jean-Marc Clévy** — co-intern (M2), AOD project (WP4)
- **Professor Lionel Brunel** — internship supervisor, Laboratoire
  Epsylon, Université Paul-Valéry Montpellier 3
- **Laboratoire Epsylon** — Université Paul-Valéry Montpellier 3
- **Montpellier Méditerranée Métropole** — AOD project partner (Jardin
  du Peyrou site)
- **AOD (Art of Darkness) project** — WP4

Please keep this list when reusing or redistributing the tool (see the
MIT license below).

## What the tool does

- **Drop pins** on a map: tap = stationary person/group, double-tap =
  person/group in motion.
- **Observation card** per pin: headcount, observed usages (customisable
  checklist), free-text notes, optional photo.
- **Tap-to-blur**: right after taking a photo, tap directly on faces to
  blur them before confirming (or reopen a saved photo to touch it up
  later).
- **Move a pin** afterwards through a dedicated button (no accidental
  drag-and-drop).
- **Undo** the creation of a pin right after placing it (button inside
  the notification that appears).
- **Session sheet**: observer name (then attached to every pin dropped,
  until changed again), timestamped overall headcount (people visible,
  estimated average age, male/female split, people with disabilities),
  with **manually entered weather** (simple icons + temperature).
- **Automatic local save**: all data stays on the device being used
  (browser storage), nothing to configure, nothing lost if the tab
  closes by accident. There is no sync between devices: if several
  tablets are used at once, each keeps its own data, and each one needs
  to be exported to CSV separately and combined afterwards.
- **Screen kept awake** while observing (Wake Lock), where the browser
  supports it.
- **Customisable background map**: any image can replace the default
  map (saved locally on the device).
- **Fully customisable device legend and usage checklist** (settings
  button): add, rename or remove entries without touching the code.
- **Bilingual** French / English, instant switch via the "FR/EN" button
  top-right (preference remembered per device).
- **CSV export** (French-Excel compatible, `;` separator) including
  sessions and all pins with their checked usages, in whichever language
  is currently displayed.
- **Day/night mode** (reduced brightness for night-time observation).

## Data model

All data is kept in the browser (`localStorage`, key `spotcount_state`),
as a single JSON object:

```json
{
  "points": { "p...": { "..." : "see below" } },
  "sessions": { "s...": { "...": "see below" } },
  "customDeviceLegend": [ { "label": "...", "cls": "circle", "color": "#..." } ],
  "customUsageItems": [ { "key": "...", "label": "..." } ],
  "mapImageSrc": "data:image/jpeg;base64,..."
}
```

**Observation point**:
```json
{
  "id": "p...",
  "x": 0.42, "y": 0.31,
  "type": "stationary|moving",
  "time": "2026-...",
  "count": 1,
  "usages": { "footing": false, "danse": true },
  "autreTexte": "",
  "notes": "",
  "photo": "data:image/jpeg;base64,...",
  "hasPhoto": true
}
```

**Session round**:
```json
{
  "id": "s...",
  "date": "2026-07-12", "jour": "Sunday", "heure": "19:30",
  "meteoIcon": "sunny", "meteoTemp": "22",
  "visibles": 45, "age": "35", "genre": "55/45", "handicap": 2,
  "savedAt": "2026-..."
}
```

Language preference is stored separately under `spotcount_lang`
(`"fr"` or `"en"`).

## Reusing this for another team or site

The tool is designed to be reused on another site or for another
observation protocol without touching the code:
- Change the background map (map button).
- Edit the device legend and the observed usage checklist (Settings
  button).
- Switch the whole interface to English (FR/EN button).

Only the shape of the observation cards (headcount, notes, photo,
position on the map) stays fixed.

## License

This project is released under the **MIT License** (see
[LICENSE](LICENSE)): anyone may use, modify and redistribute it freely,
including for commercial purposes, provided the authors are credited
(see "Authors and contributors" above).
