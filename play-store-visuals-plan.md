# SummitReady — Google Play store visuals

## 1. What's actually in Drive

**Marketing library** (`SummitReady` → folders 01–07):

| Folder | Contents |
|---|---|
| 01 - Brand Assets | `logo.gif` only |
| 02 - Original Creatives | 7 social renders + the screenshots folder |
| 02 → Actual App Screenshots - Verified | **15 real Android app screenshots** + 3 Chrome browser screenshots |
| 03 - Ad Campaigns | 4 format folders (4x5, 1x1, 9x16, 16x9) — 01 has 4 renders, the rest are empty |
| 04 - Video Advertising | empty |
| **05 - App Store Marketing** | **empty** |
| 06 - Approved for Use | `SR_BigDays_StartSmall_AuthenticApp_V01_APPROVED.png` |
| 07 - Archive | empty |

**The gap: there is no feature graphic anywhere.** Play requires one (1024×500) and will not let you
publish without it. The `05 - App Store Marketing` folder — the one place it should live — is empty.

The only feature graphic that exists is `artifacts/summit-ready/assets/store-feature-graphic.png`
in the repo (the cartoon mascot one), which you've said isn't yours.

## 2. The 15 real app screenshots

All from the Android app (filenames `Screenshot_2026…_SummitReady.jpg`), captured 25 Oct 10:36–10:41.

| Time | Screen |
|---|---|
| 103625 | Expeditions — Matterhorn Ridge Challenge, "Simulated in Eryri", 44% (700/1,600 m), next stage Crib Goch Traverse |
| 103632 | Explore — "Discover your next peak", featured Ben Nevis + Snowdon via Pyg Track |
| 103641 | Mountain detail — Ben Nevis, safety & hazards, about, key facts |
| 103734 | Route planner — drawing a route near Tryfan, follow-paths, Save route / GPX |
| 103749 | Route planner map — Ogwen valley, car parks |
| 103814 | Track — Scafell, Start hike / Free hike / Plan a route to here |
| 103837 | Track map — Scafell contours |
| 103853 | Track map — Wasdale, Scafell Pike, Great Gable |
| 103916 | Track map — Scafell Pike massif |
| 103926 | Expeditions hub — "Take on a real objective", 12 expeditions, custom builder |
| 103931 | Popular Expeditions — Everest Scotland, Matterhorn Lake District, Welsh Mont Blanc |
| 104106 | Training Basecamp — Mont Blanc, 157 days to go, readiness 67%, this week's mission |
| 104112 | AI Coach — session analysis, next priority, 67% → 68% projected |
| 104128 | Training Plan — Base phase week 3 of 25, schedule, hill session detail |
| 104140 | Incline Treadmill — session prescription |

The 3 `…_Chrome.jpg` files are browser captures with Chrome's address bar visible — **don't use these**.

## 3. Recommended Play screenshot set (8, in order)

Play shows the first 3–4 most prominently, so the distinctive idea has to land immediately.

| # | File | Caption suggestion |
|---|---|---|
| 1 | 104106 Training Basecamp | Train for the mountain you've chosen |
| 2 | 103931 Popular Expeditions | Everest in Scotland. Mont Blanc in Wales. |
| 3 | 103625 Matterhorn Ridge Challenge | Every stage is a real hill near you |
| 4 | 104128 Training Plan | A plan built back from your summit date |
| 5 | 104112 AI Coach | Coaching that reacts to what you actually climbed |
| 6 | 103632 Explore | Verified mountains, routes and parking |
| 7 | 103853 Track map | Track every ascent by GPS |
| 8 | 103734 Route planner | Draw your own route. Export the GPX. |

Dropped: 103641 (text-heavy), 103749 / 103837 / 103916 (duplicate maps), 103814 (weaker than 103853),
103926 (overlaps 103931), 104140 (indoor treadmill undercuts the outdoor positioning as a first impression).

**Caption wording:** keep clear of any phrasing that implies a UK hill prepares someone to safely
climb the real alpine peak — same line you drew for the route-matching work. "Train for",
"simulated in", "banked toward" are all fine. "Ready for Mont Blanc" is not.

## 4. Specs

| Asset | Requirement | Status |
|---|---|---|
| App icon | 512×512, 32-bit PNG, ≤1 MB, no pre-rounded corners or shadow | repo's `store-icon-512.png` **passes** |
| Feature graphic | 1024×500, JPEG or 24-bit PNG, **no alpha**. Required. | **missing** |
| Phone screenshots | 2 min, 4+ recommended. 320–3840 px per side. **Long side ≤ 2× short side.** JPEG or 24-bit PNG, no alpha | needs checking |
| Tablet | optional to publish; 4+ wanted for large-screen placements | none |
| App name / short / full description | 30 / 80 / 4000 chars. No "#1", no prices | — |

### The aspect-ratio catch

Play's rule is that the long side can't exceed twice the short side. A typical modern Android
phone screenshot is 1080×2400 (20:9) — that's 2.22:1, which **breaks the rule**. If your captures
are that shape they'll be refused at their native size.

Two fixes:
- **Play Console's Asset Library has a built-in crop tool** that appears automatically when an upload
  doesn't fit the slot. Easiest path — crop in the Console.
- Or pad/crop to **1080×1920** (9:16) before uploading.

Check the actual dimensions in Drive: open a file → the ⓘ details pane shows them.

## 5. Also worth fixing

- **`app.json` has no `adaptiveIcon`** under `android`. Android 8+ launchers therefore fall back to
  the legacy square icon. Add a foreground/background pair (and a `monochromeImage` for Android 13+
  themed icons). Separate from the store icon.
- **`scripts/generate-screenshots.cjs` outputs 1290×2796** (iPhone 6.7") — breaks Play's 2:1 rule, and
  it *hand-draws* app UI with canvas rather than capturing real screens, which is a Play metadata-accuracy
  risk. `scripts/take-screenshots.mjs` is the honest one (drives the real app via Playwright); it needs
  `deviceScaleFactor: 3` at a 360×640 viewport to land on 1080×1920.
- The repo's feature graphic was encoded **48-bit** (16 bits/channel), not the 24-bit Play asks for.
  Whatever artwork replaces it, flatten to 8 bits/channel with no alpha.
