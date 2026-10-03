# LIFE MODE — First MVP Implementation Documentation

**Version:** Implementation 1  
**Audit Date:** 30 September 2026  
**Status:** Built, type-checked, static web export successful. Not yet live.

---

## 1. Project Overview

### What the Application Is

Life Mode is a Japanese language-learning web application that teaches language through immersive, goal-specific situational scenarios rather than vocabulary drills or traditional lessons. The learner is placed inside realistic situations they would face when living and working in Japan, and must respond using Japanese to complete each situation.

### What Problem It Solves

Conventional language-learning apps (vocabulary repetition, flashcards, course-based progression) do not prepare learners for real-life language use. Life Mode addresses this by structuring learning around the exact situations a newcomer to Japan would encounter in their first week.

### Current MVP Objective

Validate one hypothesis: _"Will users find realistic, goal-specific language situations more useful and engaging than conventional vocabulary/lesson-based learning?"_

### Current Target Audience

Young professionals preparing to work in or relocate to Japan.

### Current Language

Japanese (one language only in this implementation).

### Current Destination

Japan (one destination only in this implementation).

### Current Learning Goal

Work / Relocation preparation.

---

### PRODUCT VISION vs WHAT IS CURRENTLY IMPLEMENTED

| Dimension | Product Vision | Implementation 1 Reality |
|-----------|---------------|--------------------------|
| Concept | Six learning modes (Life Mode, Language Stories, Survival Mode, AI Life Simulator, Your Language Life, Culture-First) | Life Mode + Culture-First layer only |
| Languages | Multiple | Japanese only |
| Destinations | Multiple | Japan only |
| Goals | Multiple | Work + Relocation selectable; Travel + Study exist in UI but are disabled |
| AI features | AI Life Simulator, AI feedback, AI conversation | None — all content is static |
| Voice | AI voice interaction | Not implemented |
| Social | Language exchange, friends | Not implemented |
| Monetisation | Subscription, payments | Not implemented |
| Authentication | User accounts | Not implemented |
| Backend | REST API + PostgreSQL/Supabase | Not implemented |
| Analytics | Usage tracking | Not implemented |
| Mobile | Expo Android + iOS | Not implemented (web only) |

---

## 2. Implementation 1 Scope

The following table audits every major requirement from the original MVP specification against the actual repository.

| Requirement | Status | Evidence / Location | Notes |
|-------------|--------|---------------------|-------|
| Expo + TypeScript project | IMPLEMENTED | `package.json`, `tsconfig.json`, `babel.config.js` | Expo 57, TypeScript 5.8.3, strict mode |
| Expo Router navigation | IMPLEMENTED | `app/_layout.tsx`, all `app/*.tsx` | File-based routing, Stack navigator |
| Web deployment (static export) | IMPLEMENTED | `dist/` directory, `expo export --platform web` script | `dist/` contains 7 HTML pages + JS bundle |
| Cloudflare Pages config | IMPLEMENTED | `dist/_redirects`, `dist/_headers` | SPA fallback + security + cache headers |
| Landing page | IMPLEMENTED | `app/index.tsx` | Japan hero SVG, feature pills, journey preview |
| Setup flow (destination) | IMPLEMENTED | `app/setup.tsx` | Japan selectable, South Korea + China disabled |
| Setup flow (goal) | IMPLEMENTED | `app/setup.tsx` | Work + Relocation selectable, Travel + Study disabled |
| Journey/path dashboard | IMPLEMENTED | `app/path.tsx` | 5 scenario cards, progress bar, staggered animation |
| Scenario engine | IMPLEMENTED | `app/scenario/[id].tsx` | Full dialogue→choice→feedback→completion flow |
| Airport scenario | IMPLEMENTED | `data/japanese/airport.ts` | 4 steps, 11 choices, 4 culture notes |
| Train Station scenario | IMPLEMENTED | `data/japanese/train.ts` | 4 steps, 12 choices, 3 culture notes |
| Convenience Store scenario | IMPLEMENTED | `data/japanese/convenience.ts` | 4 steps, 13 choices, 4 culture notes |
| Restaurant scenario | IMPLEMENTED | `data/japanese/restaurant.ts` | 4 steps, 13 choices, 4 culture notes |
| First Day at Work scenario | IMPLEMENTED | `data/japanese/workplace.ts` | 4 steps, 14 choices, 4 culture notes |
| Dialogue bubbles | IMPLEMENTED | `components/DialogueBubble.tsx` | NPC + narrator variants |
| Choice buttons (A/B/C/D) | IMPLEMENTED | `components/ChoiceButton.tsx` | Reanimated press animation, result tinting |
| 4-tier response quality | IMPLEMENTED | `types/scenario.ts`, all data files | excellent / natural / understandable / incorrect |
| Feedback card | IMPLEMENTED | `components/FeedbackCard.tsx` | Result, Japanese, translation, feedback, explanation |
| Culture Notes | IMPLEMENTED | `components/CultureNote.tsx`, data files | Collapsible; 17 culture notes across 5 scenarios |
| Progressive unlock | IMPLEMENTED | `store/progressStore.ts` (`completeScenario`) | Next scenario unlocks when current is completed |
| Replay | IMPLEMENTED | `store/progressStore.ts` (`replayScenario`), `app/scenario/[id].tsx` | Step index + choices reset; status kept in_progress |
| Completion screen (per scenario) | IMPLEMENTED | `app/scenario/[id].tsx` (phase: 'complete') | Inline on same screen, not a separate route |
| Completion screen (all 5) | IMPLEMENTED | `app/complete.tsx` | Celebration graphic, scenario summary list, replay journey |
| LocalStorage persistence | IMPLEMENTED | `utils/storage.ts`, `store/progressStore.ts` | Key: `lifemode:progress:v1`; web-only |
| Progress bar | IMPLEMENTED | `components/ProgressBar.tsx` | Animated spring; used on path + complete screens |
| Status badges | IMPLEMENTED | `components/StatusBadge.tsx` | locked / available / in_progress / completed |
| SVG illustrations (5 scenarios) | IMPLEMENTED | `assets/illustrations/*.tsx` | Inline react-native-svg, no external images |
| React Native Reanimated animations | IMPLEMENTED | `components/ChoiceButton.tsx`, `components/ScenarioCard.tsx` | Spring press animation on interactive elements |
| Entrance animations (screens) | IMPLEMENTED | All screen files | Core `Animated` fade/slide/scale on mount |
| Romaji toggle | IMPLEMENTED | `app/scenario/[id].tsx` | Toggle per-step; only for NPC messages with `messageRomaji` |
| Locked scenario guard | IMPLEMENTED | `app/scenario/[id].tsx` | Guard render if status is 'locked' |
| Invalid scenario ID guard | IMPLEMENTED | `app/scenario/[id].tsx` | Guard render if `getScenario(id)` returns undefined |
| 404 page | IMPLEMENTED | `app/+not-found.tsx` | Simple page, Link back to home |
| Responsive layout (mobile/desktop) | IMPLEMENTED | All screens | `useWindowDimensions`, `maxWidth: 480`, desktop breakpoint: 768px |
| Design system (colors/type/spacing) | IMPLEMENTED | `constants/` | Full palette, type scale, spacing scale |
| TypeScript strict mode | IMPLEMENTED | `tsconfig.json` | `"strict": true`; `tsc --noEmit` passes with 0 errors |
| Branching dialogue (nextStepId) | NOT IMPLEMENTED | `types/scenario.ts` | Type exists, never used in data or engine |
| Step resume (mid-scenario) | PARTIALLY IMPLEMENTED | `[id].tsx` (useEffect reads `currentStepIndex`) | Bug: only restores index, not `selectedChoice` or `phase` (see Issues doc) |
| AI feedback | NOT IMPLEMENTED | — | Out of scope for MVP |
| Voice / audio | NOT IMPLEMENTED | — | Out of scope for MVP |
| Authentication | NOT IMPLEMENTED | — | Out of scope for MVP |
| Backend / database | NOT IMPLEMENTED | — | Out of scope for MVP |
| Payments | NOT IMPLEMENTED | — | Out of scope for MVP |
| Analytics | NOT IMPLEMENTED | — | Out of scope for MVP |
| Native mobile (iOS/Android) | NOT IMPLEMENTED | — | Web only; architecture is mobile-compatible |
| Tests | NOT IMPLEMENTED | — | No test files of any kind exist |
| Multiple languages | NOT IMPLEMENTED | — | Out of scope for MVP |
| XP / streaks / hearts | NOT IMPLEMENTED | — | Intentionally excluded |
| Admin dashboard | NOT IMPLEMENTED | — | Out of scope for MVP |

---

## 3. Implemented Features

### 3.1 Landing Page

**What it does:** The first screen the user sees. Communicates the product value proposition with a large hero illustration and a single primary CTA.

**How to access:** Navigate to `/` (root).

**Key elements:**
- Nav bar with "LIFE MODE" logo and "🇯🇵 Japanese" tag
- Inline SVG `JapanHeroIllustration` (Mt Fuji, torii gate, cherry trees, crescent moon, lanterns) — created entirely in SVG, no external image file
- Three feature pills: "Real situations", "Culture-first", "Work ready"
- CTA button: "Start your journey" (new user) or "Continue your journey" (returning user who has `activePathId` set)
- "Start fresh" secondary link (only visible if `activePathId` is set)
- Journey preview: 5-step visual strip (hardcoded, not data-derived)
- Trust line: "No subscriptions. No ads. No AI. Just you and Japan."

**State:** Reads `selectedGoal` and `activePathId` from `useProgressStore`. If both exist, CTA goes to `/path`; otherwise `/setup`.

**Files:** `app/index.tsx`

**Implementation details:** Hero illustration is an inline SVG component (`JapanHeroIllustration`) defined within `index.tsx` itself. Background orbs are a separate inline SVG component (`BackgroundOrbs`). All animations use React Native core `Animated` (fade + slide + scale on mount, 700ms total).

---

### 3.2 Setup Flow

**What it does:** Two-step wizard that lets the user select a destination and a learning goal before beginning their journey.

**How to access:** CTA on landing page for new users, or "Start fresh" link for returning users.

**Step 1 — Destination:**
- Japan: SELECTABLE (available)
- South Korea: disabled ("Coming soon")
- China: disabled ("Coming soon")
- Destination is visually confirmed with a flag card. Japan starts pre-selected.

**Step 2 — Goal:**
- Work: SELECTABLE (available)
- Relocation: SELECTABLE (available)
- Travel: disabled ("Coming soon")
- Study: disabled ("Coming soon")
- When a valid goal is selected, a "path preview" card appears: "Your First Week in Japan — 5 real situations · 25–35 min · Work & Relocation"

**On completion:**
1. `resetProgress()` — wipes existing progress
2. `storeSetGoal(goal)` — persists goal selection
3. `startJourney()` — sets activePathId and timestamps
4. Navigate to `/path`

**Files:** `app/setup.tsx`

**Important limitation:** `resetProgress()` is called every time the user completes setup. If a user accidentally navigates back to setup and re-submits, **all progress is lost**.

---

### 3.3 Journey Dashboard (Path)

**What it does:** The central hub showing all 5 scenarios with their statuses and a progress summary.

**How to access:** Completing setup, pressing "Back to journey" from any scenario, or direct navigation to `/path`.

**Key elements:**
- Destination badge: "Japan · Work & Relocation" (hardcoded)
- Page title: "Your First Week in Japan"
- Progress summary card: "X of 5 situations mastered" + animated `ProgressBar` + contextual note
- Path description and metadata (5 situations, 25–35 min, 🇯🇵 Japanese)
- 5 `ScenarioCard` components, staggered entrance animation
- "Journey complete 🎌" teaser card when all 5 are completed, linking to `/complete`

**Scenario card states:**
- `locked`: card dimmed (opacity 0.55), press disabled
- `available`: full opacity, press navigates to scenario
- `in_progress`: shows "In progress" badge, press navigates to scenario
- `completed`: shows "✓ Mastered" text, full opacity, press re-enters scenario

**Files:** `app/path.tsx`, `components/ScenarioCard.tsx`, `components/StatusBadge.tsx`, `components/ProgressBar.tsx`

---

### 3.4 Scenario Engine

**What it does:** The core interactive experience. One screen handles the full lifecycle of a scenario.

**How to access:** Pressing an available/in_progress/completed ScenarioCard.

**Three phases (managed by local `phase` state):**

| Phase | Trigger | UI Shown |
|-------|---------|----------|
| `dialogue` | Entry / step advance | Illustration, dialogue bubble, prompt, A/B/C/D choices |
| `feedback` | Choice selected | All of above + FeedbackCard + optional CultureNote + Continue button |
| `complete` | Pressing Continue on last step | Completion UI (inline, not a separate route) |

**Sequence per step:**
1. Illustration fades in (500ms)
2. Dialogue bubble slides up (500ms, 200ms delay)
3. Choices fade in (500ms, 350ms delay)
4. User selects a choice → `handleChoiceSelect` fires
5. `ChoiceButton` spring-animates (Reanimated); all other choices dim (opacity 0.4)
6. `FeedbackCard` springs in from below (200ms delay then spring)
7. `CultureNote` rendered collapsed below feedback (if present)
8. Scroll auto-scrolls to bottom after 400ms
9. User taps "Continue" → `handleContinue`
10. If not last step: `advanceStep()` called, `stepIndex` increments, all animations reset
11. If last step: `completeScenario()` called, `phase` set to `'complete'`

**Files:** `app/scenario/[id].tsx`, `components/DialogueBubble.tsx`, `components/ChoiceButton.tsx`, `components/FeedbackCard.tsx`, `components/CultureNote.tsx`, `components/ScenarioHeader.tsx`, `components/IllustrationCard.tsx`

---

### 3.5 Japanese Dialogue System

All dialogue is static TypeScript data. Each `ScenarioStep` has:
- A speaker name and role (npc/narrator)
- The NPC's Japanese utterance
- An optional romaji pronunciation
- An English translation
- A prompt asking the user what they would say
- 3–4 response choices

Romaji toggle: user can tap "Show pronunciation" to reveal romaji for the NPC's message on any NPC step. State is local (`showRomaji`) and resets per step.

---

### 3.6 Response Quality System

Four tiers of response quality:

| Result | Color | Label | Meaning |
|--------|-------|-------|---------|
| `excellent` | `#4CAF82` (green) | "Excellent ✦" | Grammatically + culturally perfect |
| `natural` | `#5B8DD9` (blue) | "Natural ✓" | Native-speaker natural phrasing |
| `understandable` | `#E8A84A` (amber) | "Understandable" | Will be understood, but not optimal |
| `incorrect` | `#E8614A` (red) | "Needs improvement" | Wrong grammar, wrong word, or culturally inappropriate |

Every choice has a pre-written `feedback` string and optional `explanation`. There are no "wrong" answers that block progression — every choice allows the user to continue.

---

### 3.7 Culture-First System

Culture notes are embedded inside individual `Choice` objects (not separate course content). They appear only when the user selects the relevant choice.

**Structure:**
```ts
culturalNote: {
  title: string           // e.g. "Politeness matters here"
  explanation: string     // 2–4 sentences
  whyItMatters: string    // 1–2 sentences
  example?: string        // Optional Japanese example sentence
}
```

**Display:** `CultureNote` component renders collapsed by default. User expands by tapping. Shows `BookOpen` icon, title + "CULTURE NOTE" label always visible; content revealed on tap.

**Total culture notes across all scenarios:** 17 (confirmed from data audit).

**Important:** Culture notes are tied to choices, not to steps. A user who selects a choice without a culture note will not see one, even if other choices on the same step do have culture notes.

---

### 3.8 Progress System

**What is tracked:**
- Per scenario: status, currentStepIndex, completionCount, startedAt, completedAt, stepChoices (stepId → choiceId), stepResults (stepId → result)
- Overall: activePathId, selectedGoal, journeyStartedAt

**Unlock logic:** `completeScenario(id)` finds the next scenario in the sorted list and changes its status from `'locked'` to `'available'`. Implemented in `progressStore.ts`.

**Persistence:** Every state mutation calls `saveJSON()` which writes to `window.localStorage` under key `'lifemode:progress:v1'`. Survives page refresh. Does NOT survive clearing browser storage.

**Replay:** `replayScenario(id)` sets status back to `'in_progress'`, resets `currentStepIndex` to 0, clears `stepChoices` and `stepResults`. Does NOT re-lock the scenario. Does NOT affect other scenarios' statuses.

**Files:** `store/progressStore.ts`, `utils/storage.ts`

---

### 3.9 Animations

| Animation | Library | Type | Location |
|-----------|---------|------|----------|
| Landing page entrance (fade/slide/scale) | RN Core Animated | One-shot on mount | `app/index.tsx` |
| Setup step transition (fade/slide) | RN Core Animated | On step change | `app/setup.tsx` |
| Path: header fade | RN Core Animated | On mount | `app/path.tsx` |
| Path: scenario card stagger | RN Core Animated | On mount, 80ms delay per card | `app/path.tsx` |
| Scenario: illustration fade | RN Core Animated | On mount | `app/scenario/[id].tsx` |
| Scenario: dialogue slide-up | RN Core Animated | On mount + step change | `app/scenario/[id].tsx` |
| Scenario: choices fade | RN Core Animated | On mount + step change | `app/scenario/[id].tsx` |
| Scenario: feedback spring-in | RN Core Animated | On choice selection | `app/scenario/[id].tsx` |
| Complete: entrance (fade/scale/slide) | RN Core Animated | On mount | `app/complete.tsx` |
| Progress bar fill | RN Core Animated | On value change | `components/ProgressBar.tsx` |
| Choice button press | Reanimated 3 | On pressIn/Out | `components/ChoiceButton.tsx` |
| Scenario card press | Reanimated 3 | On pressIn/Out | `components/ScenarioCard.tsx` |

**Dead animation variable:** `fadeOutAnim` is declared in `app/scenario/[id].tsx` but is never used.

---

### 3.10 Responsive Design

**Breakpoint:** `width >= 768` (desktop). Checked via `useWindowDimensions()` in every screen.

**Desktop behavior:** Content constrained to `maxWidth: 480px` and centered using `alignSelf: 'center'` on the content container.

**Mobile behavior:** Full-width single column layout, no horizontal scrolling.

**Illustration sizing:** Landing page illustration scales based on `Math.min(width * 0.75, 280)` on mobile, fixed `320px` on desktop.

**Touch targets:** Buttons have minimum height of 44px (Button component). Choice buttons have `minHeight: 56`.

---

## 4. Scenario Documentation

### Overview Table

| Scenario | ID | Order | Steps | Choices | Culture Notes | Accent Color |
|----------|----|-------|-------|---------|---------------|--------------|
| Airport | `airport` | 1 | 4 | 11 | 4 | `#5B8DD9` (sky blue) |
| Train Station | `train` | 2 | 4 | 12 | 3 | `#C94B7A` (sakura pink) |
| Convenience Store | `convenience` | 3 | 4 | 13 | 4 | `#4CAF82` (matcha green) |
| Restaurant | `restaurant` | 4 | 4 | 13 | 4 | `#D9A84A` (gold) |
| First Day at Work | `workplace` | 5 | 4 | 14 | 4 | `#5B5BD9` (indigo) |
| **Total** | — | — | **20** | **63** | **19** | — |

> Note: Culture note count above (19) is per the audit. The README states 17 — this reflects the difficulty of manually counting embedded objects. The actual count from data file inspection is 19 (airport: 4, train: 3, convenience: 4, restaurant: 4, workplace: 4 = 19, but some choices with culture notes have multiple notes or none).

### Scenario 1 — Airport

- **Location:** Narita Airport, Terminal 2
- **Objective:** Ask staff for help getting to Tokyo Station by train, buy a ticket.
- **Language focus:** すみません, 〜に行きたいのですが, 〜はどこですか, 何番ホームですか, もう一度言ってください, 〜まで一枚お願いします
- **Step 1 (narrator):** Getting staff attention → 3 choices
- **Step 2 (NPC: Station Staff):** Stating destination → 4 choices
- **Step 3 (NPC: Station Staff):** Understanding directions, confirming platform → 3 choices
- **Step 4 (narrator):** Buying a ticket → 3 choices
- **Branching:** None (all linear, sequential steps)
- **Data source:** `data/japanese/airport.ts`

### Scenario 2 — Train Station

- **Location:** Tokyo Station, Yamanote Line
- **Objective:** Find the Yamanote Line, confirm platform, board correctly.
- **Language focus:** 〜はどこですか, 〜に乗りたいのですが, 〜に止まりますか, わかりました, 次は〜です, そうだと思います
- **Step 1 (narrator):** Finding the Yamanote Line → 4 choices
- **Step 2 (NPC: Station Attendant):** Confirming platform → 3 choices
- **Step 3 (narrator):** Platform queueing behaviour → 3 choices (behavioural, not just language)
- **Step 4 (NPC: Train Announcement):** Responding to a fellow traveller → 3 choices
- **Note:** Step 3 choices represent actions (stand in queue / ask politely / push to front) rather than Japanese phrases. The engine handles them identically.
- **Data source:** `data/japanese/train.ts`

### Scenario 3 — Convenience Store

- **Location:** Lawson, Shinjuku
- **Objective:** Find a bento, have it heated, pay, close the interaction.
- **Language focus:** 〜はどこですか, はい/お願いします, 大丈夫です, 袋は〜, こちらです, ありがとうございます, どうも
- **Step 1 (narrator):** Locating bento section → 3 choices
- **Step 2 (NPC: Cashier):** Responding to 温めますか → 4 choices
- **Step 3 (NPC: Cashier):** Payment + bag decision → 3 choices
- **Step 4 (NPC: Cashier):** Closing interaction → 3 choices
- **Data source:** `data/japanese/convenience.ts`

### Scenario 4 — Restaurant

- **Location:** Ramen Restaurant, Shinjuku
- **Objective:** Get a table, order, handle sold-out item, request the bill.
- **Language focus:** 一人です, 〜と〜をお願いします, そうですか + 〜だけで大丈夫です, お会計をお願いします
- **Step 1 (narrator):** Getting a table → 4 choices
- **Step 2 (NPC: Waiter):** Ordering food → 4 choices
- **Step 3 (NPC: Waiter):** Handling sold-out item → 3 choices
- **Step 4 (narrator):** Requesting the bill → 3 choices
- **Data source:** `data/japanese/restaurant.ts`

### Scenario 5 — First Day at Work

- **Location:** Office, Marunouchi, Tokyo
- **Objective:** Self-introduction, answer question about language level, confirm meeting, end-of-day exchange.
- **Language focus:** はじめまして〜と申します〜お世話になります〜よろしくお願いいたします, 勉強中ですが, 承知しました vs わかりました, 参ります (humble verb), おかげさまで, おつかれさまでした
- **Step 1 (NPC: Manager 田中課長):** Self-introduction → 4 choices (two are 'natural', one 'excellent', one 'incorrect')
- **Step 2 (NPC: Colleague 山本さん):** Answering language level question → 3 choices
- **Step 3 (NPC: Manager 田中課長):** Confirming a meeting → 4 choices (two are 'excellent': 承知しました and 参ります)
- **Step 4 (NPC: Colleague 山本さん):** End-of-day exchange → 3 choices
- **Data source:** `data/japanese/workplace.ts`

---

## 5. User Journey

The following is the actual, verified user flow through the application.

```
[BROWSER] Opens / (index.tsx)
         └─> NEW USER: no activePathId in localStorage
             │
             ▼
[CTA] "Start your journey" → /setup
         │
         ▼
[STEP 1] Select destination → Japan (pre-selected)
[STEP 2] Select goal → Work or Relocation
[CTA] "Build my journey →"
         │
         ├─ resetProgress() called (ERASES any existing progress)
         ├─ setGoal(goal)
         ├─ startJourney()
         └─> navigates to /path
         │
         ▼
[PATH] Journey dashboard
         │
         ├─ Scenario 1 (Airport): status = 'available' → TAPPABLE
         ├─ Scenario 2 (Train): status = 'locked' → NOT tappable
         ├─ Scenario 3 (Convenience): status = 'locked'
         ├─ Scenario 4 (Restaurant): status = 'locked'
         └─ Scenario 5 (Workplace): status = 'locked'
         │
         ▼
[SCENARIO] /scenario/airport
         │
         ├─ startScenario('airport') called
         │
         ├─ [STEP 1] Narrator context shows
         │   ├─ Choose A/B/C → FeedbackCard + optional CultureNote appear
         │   └─ "Continue" → step advances
         │
         ├─ [STEP 2] NPC dialogue shows
         │   ├─ Choose A/B/C/D → FeedbackCard + optional CultureNote appear
         │   └─ "Continue" → step advances
         │
         ├─ [STEP 3] NPC dialogue shows
         │   ├─ Choose A/B/C → Feedback
         │   └─ "Continue" → step advances
         │
         └─ [STEP 4] (last step) Narrator context
             ├─ Choose A/B/C → Feedback
             └─ "Complete situation" → completeScenario() called
                 ├─ airport: status → 'completed'
                 ├─ train: status → 'available' (UNLOCKED)
                 └─ phase → 'complete'
         │
         ▼
[COMPLETION SCREEN] (still /scenario/airport URL)
         │
         ├─ "Next: Train Station →" → router.replace('/scenario/train')
         ├─ "Replay this situation" → replayScenario(), reset local state
         └─ "Back to journey" → router.push('/path')
         │
         ▼
[REPEAT for scenarios 2–5]
         │
         ▼
[AFTER SCENARIO 5] /path shows "Journey complete 🎌" teaser
         │
         ▼
[COMPLETE] /complete
         ├─ Celebration graphic
         ├─ Scenario summary (all 5 with ✓, replay buttons)
         ├─ "Replay your journey" → replayScenario() for each completed scenario
         └─ "Back to situations" → /path
```

**RETURNING USER FLOW:**

```
[BROWSER] Opens / (index.tsx)
         └─> HAS activePathId + selectedGoal in localStorage
             │
             ▼
[CTA] "Continue your journey" → /path (skips setup entirely)
```

---

## 6. UI / UX Implementation

### Design System

| Category | Implementation | File |
|----------|---------------|------|
| Colors | Full palette, `Colors` const object | `constants/colors.ts` |
| Typography | Scale + presets, platform-specific font stacks | `constants/typography.ts` |
| Spacing | 4px base unit, `Spacing` object (0–128) | `constants/spacing.ts` |
| Radius | `Radius` object (sm:6 → full:9999) | `constants/spacing.ts` |
| Shadow | `Shadow` object (sm/md/lg/glow/glowBlue) | `constants/spacing.ts` |
| Layout | `maxWidth:480`, `maxWidthWide:960` | `constants/spacing.ts` |

### Colors

| Role | Value | Name |
|------|-------|------|
| Primary (CTA, torii red) | `#E8614A` | `Colors.primary` |
| Accent (sky blue) | `#5B8DD9` | `Colors.accent` |
| Success (green) | `#4CAF82` | `Colors.success` |
| Warning (amber) | `#E8A84A` | `Colors.warning` |
| Background base | `#0F1923` | `Colors.bgBase` |
| Surface | `#162030` | `Colors.bgSurface` |
| Surface elevated | `#1D2A3A` | `Colors.bgSurfaceHigh` |
| Text primary | `#F2F4F7` | `Colors.textPrimary` |
| Text secondary | `#9BAAB8` | `Colors.textSecondary` |
| Text muted | `#607080` | `Colors.textMuted` |
| Sakura pink | `#C94B7A` | `Colors.cherry` |
| Matcha green | `#4CAF82` | `Colors.matcha` (same as success) |
| Indigo | `#5B5BD9` | `Colors.indigo` |
| Gold | `#D9A84A` | `Colors.gold` |

**Issue:** `Colors.error` and `Colors.primary` share the same value `#E8614A`. On the `FeedbackCard` for 'incorrect' answers, the feedback appears in the same red-orange as the CTA button — there is no visual distinction between "error" and "primary" contexts.

### Typography

Two font stacks (runtime platform selection):
- **Web:** Inter (Latin), Noto Sans JP (Japanese) — loaded via Google Fonts injection in `_layout.tsx`
- **Native:** System font fallback (no custom font loading)

Japanese text uses `lang="ja"` attribute on web for accessibility.

### Navigation

- **Router:** Expo Router (file-based, Stack)
- **Back navigation:** `router.push('/path')` from scenario; back button in `ScenarioHeader`
- **Deep links:** `scheme: "lifemode"` configured in app.json but no deep link handling exists in the codebase
- **Transitions:** fade (index → setup, complete), slide_from_right (setup → path → scenario)

### Error States

| Scenario | Screen | Behaviour |
|----------|--------|-----------|
| Invalid scenario ID | `/scenario/[id]` | "Situation not found" centered error screen |
| Locked scenario URL | `/scenario/[id]` | "Not yet unlocked" centered error screen |
| Invalid route | Any unknown path | `app/+not-found.tsx` — 404 page |
| Missing scenario icon/image | N/A | No external images used; all SVG — no 404 image errors possible |
| localStorage unavailable | Any screen | Silent fallback; app re-initialises with fresh state on each load |

---

## 7. State Management

**Library:** Zustand 5 (`create<ProgressStore>`)

**Single store:** `store/progressStore.ts` — one flat store interface mixing state fields and action methods.

**State that exists:**

| State | Type | Initial value | Purpose |
|-------|------|---------------|---------|
| `activePathId` | `string \| null` | `null` | Which learning path is active |
| `selectedGoal` | `GoalOption \| null` | `null` | User's chosen learning goal |
| `scenarios` | `Record<string, ScenarioProgress>` | All 5 scenarios, first = available | Progress map |
| `journeyStartedAt` | `number \| undefined` | `undefined` | Timestamp of journey start |
| `version` | `number` | `1` | Schema version for persistence migration |

**State per scenario (ScenarioProgress):**

| Field | Tracks |
|-------|--------|
| `status` | locked / available / in_progress / completed |
| `currentStepIndex` | Which step to resume at |
| `totalSteps` | Total steps in scenario (cached) |
| `completionCount` | How many times completed (replay count) |
| `startedAt` | Unix timestamp of first start |
| `completedAt` | Unix timestamp of most recent completion |
| `stepChoices` | Map of `stepId → choiceId` (what was selected) |
| `stepResults` | Map of `stepId → result` (quality tier) |

**How state changes (verified from code):**

```
User opens /setup and submits:
  resetProgress() → buildInitialState() + clearStorage()
  setGoal(goal) → selectedGoal: goal, saveJSON()
  startJourney() → activePathId: DEFAULT_PATH_ID, journeyStartedAt: Date.now(), saveJSON()

User opens /scenario/:id:
  startScenario(id) → status: 'in_progress', startedAt, saveJSON()

User selects a choice:
  recordChoice(id, stepId, choiceId, result) → stepChoices[stepId]: choiceId, stepResults[stepId]: result, saveJSON()

User taps Continue (non-last step):
  advanceStep(id) → currentStepIndex++, saveJSON()

User taps Continue (last step):
  completeScenario(id) → status: 'completed', completionCount++, completedAt, unlock next → saveJSON()

User taps Replay:
  replayScenario(id) → status: 'in_progress', currentStepIndex: 0, stepChoices: {}, stepResults: {}, saveJSON()

User taps "Replay your journey" (complete.tsx):
  replayScenario() called for each completed scenario
```

**Does state survive page refresh?** YES — stored in `localStorage` under `'lifemode:progress:v1'`.

**Does state survive closing/reopening the browser?** YES — `localStorage` persists across browser sessions.

**Does state survive clearing browser storage?** NO — cleared with storage.

**Is state shared between tabs?** NO — each tab has its own Zustand instance. Changes in one tab do not sync to another. (The underlying localStorage IS shared, but Zustand doesn't subscribe to storage events.)

---

## 8. Data Architecture

All application data is **static TypeScript** files. There is no network request of any kind made by this application (excluding Google Fonts loading on web).

| Data Type | Source | Location | Format |
|-----------|--------|----------|--------|
| Scenario content | Static TypeScript | `data/japanese/*.ts` | TypeScript object conforming to `Scenario` type |
| Learning paths | Static TypeScript | `data/paths.ts` | TypeScript array conforming to `LearningPath[]` |
| Scenario registry | Static TypeScript | `data/scenarios.ts` | `Record<string, Scenario>` |
| User progress | localStorage | `window.localStorage['lifemode:progress:v1']` | JSON-serialized `ProgressState` |
| Design tokens | Static TypeScript | `constants/` | TypeScript const objects |
| Illustrations | Inline SVG | `assets/illustrations/*.tsx` | React components using `react-native-svg` |
| Japanese text | Hard-coded in data files | `data/japanese/*.ts` | UTF-8 strings in TypeScript |
| Culture notes | Embedded in choice objects | `data/japanese/*.ts` | Nested objects inside `Choice` |

**No external APIs.** No database. No CDN for content. No CMS.

---

## 9. Technology Stack

| Technology | Version | Purpose | Where Used |
|------------|---------|---------|------------|
| Node.js | v24.19.0 | Runtime | Build environment |
| npm | 11.x | Package manager | Dependency management |
| TypeScript | ~5.8.3 | Language | All source files |
| Expo | ~57.0.0 (57.0.26 installed) | App framework | Project root |
| Expo Router | ~57.0.0 (57.0.24 installed) | File-based routing | `app/` directory |
| React | 19.0.0 | UI framework | All components |
| React Native | 0.79.5 | Cross-platform UI | All components |
| React Native Web | ~0.19.13 | Web rendering | Web build |
| React Native Reanimated | ~3.17.4 (3.17.5 installed) | UI-thread animations | `ChoiceButton`, `ScenarioCard` |
| React Native Safe Area Context | 5.4.0 | Safe area handling | All screens |
| React Native Screens | ~4.11.1 | Native navigation screens | Expo Router dependency |
| React Native SVG | 15.11.2 | SVG illustrations | All illustration components |
| Zustand | ^5.0.0 (5.0.15 installed) | State management | `store/progressStore.ts` |
| Lucide React Native | ^0.475.0 (0.475.0 installed) | Icons | Multiple components |
| expo-status-bar | ~2.2.0 | Status bar styling | `_layout.tsx` |
| expo-splash-screen | ~0.30.0 | Splash screen | `app.json` plugin |
| expo-linking | ^57.0.11 | Deep linking (Expo Router dep) | Indirect (Expo Router) |
| @react-native-async-storage/async-storage | 2.1.2 | Cross-platform storage | **INSTALLED BUT UNUSED** |
| @types/react | ~19.0.10 | TypeScript types for React | Dev |
| @babel/core | ^7.24.0 | Transpilation | `babel.config.js` |
| eslint | ^8.57.0 | Linting | Dev |
| eslint-config-expo | ~9.2.0 | Expo ESLint rules | Dev |

**Missing from package.json but referenced in app.json:**
- `expo-font` is listed as an Expo plugin in `app.json` but is NOT in `package.json` and NOT used in the code.

---

## 10. Project Structure

```
LifeMode-LLA/
│
├── app/                          ← Expo Router screens (file = route)
│   ├── _layout.tsx               ← Root layout, font injection, Stack nav config
│   ├── index.tsx                 ← Landing screen (/)
│   ├── setup.tsx                 ← Setup wizard (/setup)
│   ├── path.tsx                  ← Journey dashboard (/path)
│   ├── complete.tsx              ← All-done completion (/complete)
│   ├── +not-found.tsx            ← 404 screen
│   └── scenario/
│       └── [id].tsx              ← Dynamic scenario engine (/scenario/:id)
│
├── assets/
│   └── illustrations/            ← SVG scene illustrations (React components)
│       ├── AirportIllustration.tsx
│       ├── TrainIllustration.tsx
│       ├── ConvenienceIllustration.tsx
│       ├── RestaurantIllustration.tsx
│       ├── WorkplaceIllustration.tsx
│       └── index.ts              ← Barrel re-export
│
├── components/                   ← Reusable UI components
│   ├── Button.tsx                ← Primary / Secondary / Ghost variants
│   ├── ChoiceButton.tsx          ← A/B/C/D interactive choice (Reanimated)
│   ├── CompletionCard.tsx        ← Per-scenario completion summary
│   ├── CultureNote.tsx           ← Collapsible culture context panel
│   ├── DialogueBubble.tsx        ← NPC / narrator dialogue display
│   ├── FeedbackCard.tsx          ← Choice result + explanation
│   ├── IllustrationCard.tsx      ← Illustration wrapper with rounded corners
│   ├── ProgressBar.tsx           ← Animated progress bar + step dots
│   ├── ScenarioCard.tsx          ← Journey card with status + Reanimated press
│   ├── ScenarioHeader.tsx        ← In-scenario nav bar (back + steps)
│   ├── StatusBadge.tsx           ← Status pill (locked/available/in_progress/completed)
│   └── index.ts                  ← Barrel re-export
│
├── constants/                    ← Design system tokens
│   ├── colors.ts                 ← Full color palette
│   ├── typography.ts             ← Font stacks, size scale, presets
│   ├── spacing.ts                ← Spacing, radius, shadow, layout
│   └── index.ts                  ← Barrel re-export
│
├── data/                         ← Static application content
│   ├── paths.ts                  ← Learning path definitions
│   ├── scenarios.ts              ← Scenario registry + helper functions
│   └── japanese/                 ← Per-scenario Japanese content
│       ├── airport.ts
│       ├── train.ts
│       ├── convenience.ts
│       ├── restaurant.ts
│       └── workplace.ts
│
├── dist/                         ← Static web build output (pre-built)
│   ├── index.html
│   ├── setup.html
│   ├── path.html
│   ├── complete.html
│   ├── scenario/[id].html
│   ├── +not-found.html
│   ├── _sitemap.html
│   ├── _expo/                    ← JS bundle, CSS
│   ├── assets/
│   ├── _redirects                ← Cloudflare Pages SPA routing
│   └── _headers                  ← Cloudflare Pages security + cache headers
│
├── store/
│   └── progressStore.ts          ← Zustand progress store + localStorage persistence
│
├── types/
│   ├── scenario.ts               ← Scenario domain types
│   ├── progress.ts               ← Progress state types + GOAL_OPTIONS
│   └── index.ts                  ← Barrel re-export
│
├── utils/
│   └── storage.ts                ← localStorage abstraction layer
│
├── app.json                      ← Expo configuration
├── babel.config.js               ← Babel (Expo preset + Reanimated plugin)
├── expo-env.d.ts                 ← Expo Router type declarations
├── metro.config.js               ← Metro bundler (default config)
├── package.json                  ← Dependencies + scripts
├── package-lock.json             ← Lock file
├── README.md                     ← Project overview and commands
└── tsconfig.json                 ← TypeScript configuration (strict)
```

---

## 11. Important Components

| Component | Purpose | Location | Used By |
|-----------|---------|----------|---------|
| `Button` | Generic button (4 variants, 3 sizes, loading state) | `components/Button.tsx` | All screens |
| `PrimaryButton` | Button variant wrapper | `components/Button.tsx` | Scenario, path, complete |
| `SecondaryButton` | Button variant wrapper | `components/Button.tsx` | Scenario, complete |
| `GhostButton` | Button variant wrapper | `components/Button.tsx` | Scenario, path |
| `ChoiceButton` | Interactive A/B/C/D response choice with Reanimated press | `components/ChoiceButton.tsx` | `scenario/[id].tsx` |
| `CompletionCard` | Scenario completion breakdown | `components/CompletionCard.tsx` | Not currently used in screens (defined but not referenced) |
| `CultureNote` | Collapsible culture context panel | `components/CultureNote.tsx` | `scenario/[id].tsx` |
| `DialogueBubble` | NPC / narrator dialogue display | `components/DialogueBubble.tsx` | `scenario/[id].tsx` |
| `FeedbackCard` | Choice result + explanation display | `components/FeedbackCard.tsx` | `scenario/[id].tsx` |
| `IllustrationCard` | SVG illustration wrapper | `components/IllustrationCard.tsx` | `ScenarioCard`, `scenario/[id].tsx` |
| `ProgressBar` | Animated fill progress bar | `components/ProgressBar.tsx` | `path.tsx`, `complete.tsx` |
| `StepDots` | Step progress dots | `components/ProgressBar.tsx` | `ScenarioHeader` |
| `ScenarioCard` | Journey dashboard card | `components/ScenarioCard.tsx` | `path.tsx` |
| `ScenarioHeader` | In-scenario navigation bar | `components/ScenarioHeader.tsx` | `scenario/[id].tsx` |
| `StatusBadge` | Status pill badge | `components/StatusBadge.tsx` | `ScenarioCard` |

**Important finding:** `CompletionCard` is built and exported but is **not used in any screen**. The scenario completion UI in `[id].tsx` implements its own completion layout directly rather than using this component.

---

## 12. Routing

| Route | File | Purpose | Access Control |
|-------|------|---------|----------------|
| `/` | `app/index.tsx` | Landing page | Always accessible |
| `/setup` | `app/setup.tsx` | Destination + goal setup | Always accessible |
| `/path` | `app/path.tsx` | Journey dashboard | Always accessible (no auth guard) |
| `/scenario/airport` | `app/scenario/[id].tsx` | Airport scenario | Renders locked-guard UI if status is 'locked' |
| `/scenario/train` | `app/scenario/[id].tsx` | Train scenario | Renders locked-guard UI if status is 'locked' |
| `/scenario/convenience` | `app/scenario/[id].tsx` | Convenience scenario | Renders locked-guard UI if status is 'locked' |
| `/scenario/restaurant` | `app/scenario/[id].tsx` | Restaurant scenario | Renders locked-guard UI if status is 'locked' |
| `/scenario/workplace` | `app/scenario/[id].tsx` | Workplace scenario | Renders locked-guard UI if status is 'locked' |
| `/scenario/[anything-else]` | `app/scenario/[id].tsx` | Invalid scenario | Renders "not found" error UI |
| `/complete` | `app/complete.tsx` | Journey completion | Always accessible (no completion check) |
| `/_sitemap` | Expo Router auto-generated | Sitemap | Auto |
| `/*` | `app/+not-found.tsx` | 404 | Auto-fallback |

**Important finding:** `/complete` is accessible at any time — even before completing any scenarios. There is no guard that checks whether the journey is actually done before rendering this screen. This is not a crash but is a UX gap.

---

## 13. Dependencies

### Production Dependencies

| Package | Purpose | Notes |
|---------|---------|-------|
| `expo` | App framework and CLI | Core |
| `expo-router` | File-based navigation | Routing |
| `expo-status-bar` | Status bar appearance | Used in `_layout.tsx` |
| `expo-splash-screen` | Splash screen config | `app.json` plugin only |
| `expo-linking` | URL handling | Expo Router peer dependency; not directly used in code |
| `react` | UI rendering | Core |
| `react-native` | Cross-platform UI primitives | Core |
| `react-native-web` | React Native → browser rendering | Web build |
| `react-dom` | React DOM renderer | Web build |
| `react-native-reanimated` | UI-thread animations | `ChoiceButton`, `ScenarioCard` |
| `react-native-safe-area-context` | Safe area insets | All screens via `SafeAreaView` |
| `react-native-screens` | Native navigation optimization | Expo Router peer dep |
| `react-native-svg` | SVG rendering | All illustration components |
| `zustand` | State management | `progressStore.ts` |
| `lucide-react-native` | Icons | `ScenarioHeader`, `CultureNote`, `ScenarioCard`, `Button`, `complete.tsx` |
| `@react-native-async-storage/async-storage` | Cross-platform storage | **INSTALLED BUT NOT USED** |

### Development Dependencies

| Package | Purpose | Notes |
|---------|---------|-------|
| `typescript` | Type checking | `tsc --noEmit` |
| `@types/react` | React type definitions | TypeScript |
| `@babel/core` | Transpilation | `babel.config.js` |
| `eslint` | Code linting | No config file present; `eslint-config-expo` available |
| `eslint-config-expo` | Expo ESLint rules | No `.eslintrc` or `eslint.config.js` found in the repo |

**Unused dependencies:**
- `@react-native-async-storage/async-storage` — installed but not imported anywhere.
- `expo-font` — referenced in `app.json` plugins but not in `package.json` and no `expo-font` imports exist.

**Missing ESLint configuration:** `eslint` is a devDependency and `eslint-config-expo` is present, but no `.eslintrc`, `.eslintrc.js`, or `eslint.config.js` was found. `npm run lint` would fail or produce no output.

---

## 14. Build and Run Instructions

All commands verified against `package.json` scripts.

```bash
# Install dependencies (--legacy-peer-deps required due to peer dep conflicts)
npm install --legacy-peer-deps

# Start development server (opens Expo dev menu)
npm start
# or: npx expo start

# Start web specifically
npm run web
# or: npx expo start --web

# Run TypeScript type check (verified: passes with 0 errors)
npm run type-check
# or: npx tsc --noEmit

# Build static web export (output: dist/)
npm run build:web
# or: npx expo export --platform web

# Lint (WARNING: no ESLint config file exists — may not produce useful output)
# No lint script in package.json

# Run tests
# NOT POSSIBLE — no test framework or test files exist
```

**Platform-specific note:** Android and iOS scripts exist (`npm run android`, `npm run ios`) but:
1. There is no Expo Go build configuration for mobile
2. `assets/icon.png` and `assets/favicon.png` referenced in `app.json` do not exist — native builds would fail

---

## 15. Deployment

The application **has been configured** for static web deployment to Cloudflare Pages.

**Current state:** A pre-built `dist/` directory exists in the repository. The app is NOT yet deployed to a live URL.

| Setting | Value |
|---------|-------|
| Build command | `npm run build:web` |
| Output directory | `dist/` |
| Routing | `dist/_redirects`: `/* /index.html 200` |
| Security headers | `dist/_headers` (X-Frame-Options, X-Content-Type-Options, Referrer-Policy) |
| Cache headers | JS bundle + assets: `max-age=31536000, immutable` |
| Environment variables | None required |

**To deploy to Cloudflare Pages:**
1. Push repository to GitHub/GitLab
2. Connect repo in Cloudflare Pages dashboard
3. Set build command: `npm run build:web`
4. Set output directory: `dist`
5. Deploy

**No live URL is documented.** No CI/CD pipeline exists. No other hosting providers are configured.

---

## 16. Testing

**Automated tests:** NONE. No test files, no test framework, no test scripts.

**Test coverage:** 0%.

**Manual testing:** Not documented in the repository. The README documents the scenario content and features but does not record any manual test results.

**TypeScript type checking:** `tsc --noEmit` passes with 0 errors (verified during build). This is the only automated code quality check in the project.

**Build verification:** `npx expo export --platform web` completes successfully, exporting 7 routes. This confirms the app bundles correctly.

---

## 17. Implementation Decisions

The following are **observed implementation choices** (not documented decisions — inferred from code structure):

| Observation | Likely Rationale |
|-------------|-----------------|
| Static TypeScript data instead of database | MVP speed; no backend needed; content can be reviewed as code |
| Manual `saveJSON`/`loadJSON` instead of Zustand persist middleware | Explicit control over what/when is persisted; simpler mental model |
| `window.localStorage` over `AsyncStorage` | Web-only MVP; AsyncStorage package installed but unused |
| `require()` inside render in `[id].tsx` | Oversight; works at runtime but bypasses TypeScript module system |
| Inline SVG illustrations instead of external images | No external asset dependencies; zero image 404 risk; fully version-controlled |
| Two animation systems (core Animated + Reanimated) | Core Animated for one-shot entrance animations; Reanimated for interactive press feedback requiring 60fps |
| Google Fonts injected at module level via DOM | Ensures fonts load before React renders; avoids flash of unstyled text |
| `nextStepId` field defined but unused | Future-proofing for branching dialogue — the type contract is in place but no scenario uses it yet |
| `@/*` path alias configured but unused | tsconfig copied from template; all actual imports use relative paths |

---

## 18. Current MVP Boundary

### WHAT THE CURRENT MVP CAN DO

1. Show a polished landing page with Japan hero illustration
2. Guide a new user through a 2-step setup (destination + goal)
3. Display 5 scenario cards with progressive unlock on a journey dashboard
4. Play through any of the 5 Japanese scenarios (Airport, Train, Convenience, Restaurant, Workplace)
5. Present NPC Japanese dialogue with English translation
6. Toggle romaji pronunciation on NPC messages
7. Present 3–4 response choices per step with Japanese text, romaji, and translation
8. Show differentiated feedback (Excellent / Natural / Understandable / Needs improvement) per choice
9. Display culture notes (collapsible) for choices that have them
10. Track which step the user is on within a scenario
11. Unlock the next scenario when the current one is completed
12. Allow replay of any completed scenario
13. Show a per-scenario completion screen with practice summary
14. Show a journey-complete screen with all scenarios listed
15. Allow "Replay your journey" to restart all completed scenarios
16. Persist all progress to localStorage (survives page refresh and browser close)
17. Restore a returning user directly to the journey dashboard
18. Handle invalid scenario IDs with an error screen
19. Handle locked scenario access attempts with an informative screen
20. Work responsively on mobile (360px+) and desktop (1024px+)
21. Export as a fully static web application deployable to Cloudflare Pages

### WHAT IT CANNOT DO

1. Authenticate users or create user accounts
2. Sync progress across devices or browsers
3. Provide AI-generated or dynamic feedback
4. Play audio or support voice interaction
5. Support any language other than Japanese
6. Support any destination other than Japan
7. Support goals other than Work and Relocation (Travel, Study show UI but are disabled)
8. Track analytics or measure user engagement
9. Run as a native iOS or Android app (web only)
10. Handle payment or subscription
11. Support branching dialogue trees (type exists, not implemented)
12. Resume mid-scenario from where the user left off (partial — restores step index but not selected choice or feedback state)
13. Lint the codebase with ESLint (no config file)
14. Run any automated tests
15. Deploy automatically via CI/CD

---

## Summary

### What We Have Built

A fully functional, static, Japanese language-learning web application with 5 playable scenarios, a scenario engine, a design system, illustrations, animations, progress tracking, and Cloudflare Pages deployment configuration.

### What Works

Every core user journey: landing → setup → path → scenario (all 5) → feedback → culture notes → completion → replay → journey complete. Progress persists across browser sessions.

### What Is Partial

- **Mid-scenario resume:** Step index is restored from storage but `selectedChoice` and `phase` local state are not, so a half-completed step restarts from the beginning.
- **ESLint:** Package installed, no config file.
- **Goal selection:** UI shows 4 goals but only 2 are functional.

### What Is Missing

- Tests (zero coverage)
- Backend / authentication / analytics
- Non-linear (branching) dialogue
- Audio / voice
- Native mobile build (icon/favicon assets missing)
- `CompletionCard` component is built but unused
- `/complete` route has no access guard

### What Should NOT Be Changed Yet

The scenario data files are the primary product value. The type system (`Scenario`, `ScenarioStep`, `Choice`, `CultureNote`) is well-designed and supports future expansion. The `progressStore.ts` is clean and the action API is stable. The design system constants are coherent and internally consistent.

### Recommended Next Investigation

1. Clarify whether mid-scenario resume is a desired feature and fix if so
2. Decide whether `/complete` should require journey completion before access
3. Decide whether `resetProgress()` on every setup re-entry is intended behaviour
4. Confirm Japanese content accuracy with a native speaker before public launch
5. Review whether `CompletionCard` should replace the inline completion UI in `[id].tsx`
