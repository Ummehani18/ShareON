# Life Mode — Implementation 2

> **Product thesis:** Life Mode is a pre-departure and real-world rehearsal platform for people who are going to Japan and want to practice the situations they are likely to face before they arrive.

---

## Table of Contents

- [Product Direction](#product-direction)
- [Implementation 2 Priorities](#implementation-2-priorities)
- [1. Visual Redesign](#1-visual-redesign)
- [2. Audio and Speaking Practice](#2-audio-and-speaking-practice)
- [3. Before You Land](#3-before-you-land)
- [4. Panic Mode](#4-panic-mode)
- [5. Product Differentiator](#5-product-differentiator)
- [6. Travel and Study Goals](#6-travel-and-study-goals)
- [7. Goal-Specific Journeys](#7-goal-specific-journeys)
- [8. Survival Skills](#8-survival-skills)
- [9. Ability-Based Learning](#9-ability-based-learning)
- [10. Scenario Branching](#10-scenario-branching)
- [11. Unexpected Moments](#11-unexpected-moments)
- [12. Immersive Scenario Design](#12-immersive-scenario-design)
- [13. Environmental Sound](#13-environmental-sound)
- [14. Technical Fixes](#14-technical-fixes)
- [15. What Not to Build Yet](#15-what-not-to-build-yet)
- [16. Implementation 2 User Flow](#16-implementation-2-user-flow)
- [17. Exact Implementation 2 Scope](#17-exact-implementation-2-scope)
- [18. Product Positioning](#18-product-positioning)
- [19. Landing Page Direction](#19-landing-page-direction)
- [20. MVP Success Test](#20-mvp-success-test)
- [Implementation 2 Thesis](#implementation-2-thesis)

---

# Product Direction

## New Product Positioning

Move the product from:

> **"Learn Japanese through scenarios."**

to:

> **"Rehearse the situations you'll face before you actually face them."**

### Core Problem

Life Mode should solve a specific problem:

> **"I am going to Japan, but I'm afraid that when someone actually speaks Japanese to me, I won't know what to say."**

The existing scenario architecture already supports this direction through real-world situations such as:

- Airport
- Train station
- Convenience store
- Restaurant
- Workplace

The goal of Implementation 2 is therefore not to turn Life Mode into another generic language-learning application. It is to make the existing scenario experience more immersive, practical, and useful.

---

# Implementation 2 Priorities

| Priority | Workstream | Importance |
|:---:|---|:---:|
| **P0** | Visual redesign | Critical |
| **P0** | Audio + speaking practice | Critical |
| **P0** | Before You Land / Survival Pack | Critical |
| **P0** | Enable Travel + Study | Critical |
| **P1** | More immersive scenarios | High |
| **P1** | Improve learning/progress system | High |
| **P2** | Technical cleanup | Medium |
| **P3** | AI / Backend / Mobile | **Do not do yet** |

### Key Principle

Do **not** spend Implementation 2 building:

- Authentication
- Databases
- AI infrastructure
- Social features
- Payments
- Native mobile applications

The core scenario engine already exists.

**Implementation 2 should dramatically improve the existing experience before expanding the technical scope.**

---

# 1. Visual Redesign

The current graphics are functional but too generic.

The existing implementation uses inline SVG illustrations for the scenarios. This is a sensible zero-cost technical approach, but the visuals should become more immersive and memorable.

## Visual Direction

Make the application feel like an:

> **Interactive travel simulation / illustrated travel experience**

Use:

- Richer scene composition
- Foreground and background layers
- Depth
- Environmental objects
- Subtle movement
- Location labels
- Contextual icons
- Atmospheric gradients
- Better typography
- Stronger Japanese typography
- Scenario-specific visual identity

## Scenario Visual Identity

| Scenario | Visual Elements |
|---|---|
| **Airport** | Departure boards, luggage, signs, train icons, staff counter |
| **Train** | Platform, train signage, platform number, queue markings, station environment |
| **Convenience Store** | Shelves, cashier, food packaging, payment counter |
| **Restaurant** | Menu, table, ramen bowl, staff |
| **Workplace** | Desk, laptop, meeting room, Japanese office environment |

The learner should feel **located inside a real situation**, rather than looking at another card.

### Example: Airport

```text
┌──────────────────────────────────────┐
│ NARITA AIRPORT                       │
│                                      │
│       [Illustrated scene]            │
│                                      │
│    ✈ Arrival Hall                    │
│                                      │
│    Station Staff                     │
│    ┌──────────────────────────────┐  │
│    │ 東京駅はどこですか？       🔊 │  │
│    │ Where is Tokyo Station?      │  │
│    └──────────────────────────────┘  │
│                                      │
│    🎙 Your turn                      │
│                                      │
│    [ Speak ]    [ Show choices ]     │
└──────────────────────────────────────┘
```

---

# 2. Audio and Speaking Practice

Audio should become a **core learning mechanic**, not simply a "Play Japanese" button.

The intended learning loop is:

```text
LISTEN
   ↓
SHADOW
   ↓
RESPOND
   ↓
UNDERSTAND
```

Every important Japanese NPC line should support audio.

## Listen Mode

The learner taps:

> ▶ **Listen**

Native-quality Japanese audio plays.

## Shadow Mode

Show:

> 🗣 **Say it with them**

Play the line again and allow the learner to repeat it aloud.

## Speak Mode

Allow the learner to respond verbally:

> 🎙 **Your turn**

For Implementation 2, sophisticated pronunciation scoring is **not required**.

The first goal is to establish the speaking behavior.

## Future Pronunciation Feedback

A future version can provide feedback such as:

```text
Pronunciation
82%

Good:
す

Practice:
り
```

### Important

Do **not** make AI pronunciation scoring a dependency for Implementation 2.

It would increase both cost and technical complexity before the core speaking loop has been validated.

---

# 3. Before You Land

Create a dedicated entry point:

# Before You Land 🇯🇵

### Subtitle

> **The Japanese you should know before your plane touches down.**

This should **not** be a traditional Japanese course.

Avoid making it primarily about:

- Grammar
- Vocabulary lists
- Memorization

Instead, focus on phrases the learner is likely to use immediately.

## Essential Phrases

Start with the **10 phrases you'll actually use**.

| Japanese | Meaning |
|---|---|
| `すみません` | Excuse me |
| `ありがとうございます` | Thank you |
| `お願いします` | Please / I'd like this |
| `大丈夫です` | I'm okay / No thank you |
| `わかりません` | I don't understand |
| `もう一度お願いします` | One more time, please |
| `ゆっくりお願いします` | Please speak slowly |
| `どこですか` | Where is it? |
| `いくらですか` | How much is it? |
| `助けてください` | Please help me |

Every phrase should follow:

```text
LISTEN
   ↓
UNDERSTAND
   ↓
SPEAK
   ↓
USE
```

Not:

```text
WORD → TRANSLATION → NEXT
```

## Make the Starter Pack Scenario-Based

### Situation: Someone spoke too quickly

NPC:

> `すみません、もう一度お願いします。`

Learner practices asking someone to repeat themselves.

### Situation: You didn't understand

Learner learns:

> `すみません、わかりません。`

### Situation: You need help

Learner learns:

> `助けてください。`

The objective is practical use rather than memorization.

---

# 4. Panic Mode

Create a quick-access feature for situations where the learner needs help immediately.

## 🚨 I NEED HELP

| Category | Example Need |
|---|---|
| 🚆 | I'm lost |
| 🍜 | I need food |
| 🏪 | I need something from a store |
| 🚻 | I need a bathroom |
| 💳 | I need to pay |
| 🗣 | I don't understand |
| 🏥 | I need medical help |
| 🚨 | Emergency |

Each category should open **3–5 immediately usable phrases**.

### Example: "I don't understand"

```text
すみません。
🔊 Listen

わかりません。
🔊 Listen

もう一度お願いします。
🔊 Listen

ゆっくりお願いします。
🔊 Listen
```

This should be a real **problem-solving feature**, not another lesson.

---

# 5. Product Differentiator

## Rehearsal Before Reality

Do not position Life Mode simply as:

> "We also have AI conversation."

The product should focus on a more specific experience:

```text
PREPARE
   ↓
REHEARSE
   ↓
EXPERIENCE
```

### Product Story

```text
BEFORE YOU LAND
       ↓
SURVIVAL BASICS
       ↓
REHEARSE
       ↓
Airport
       ↓
Train
       ↓
Restaurant
       ↓
Work
       ↓
REAL LIFE
```

The product should help the learner prepare for the **exact situations they are about to experience**.

---

# 6. Travel and Study Goals

The application has four main goals:

- ✈️ Travel
- 🎓 Study
- 💼 Work
- 🏠 Relocation

Currently, Travel and Study are disabled.

They should be enabled, but simply enabling the buttons and reusing the same five scenarios would create fake personalization.

Each goal should have its own journey.

---

# 7. Goal-Specific Journeys

## ✈️ Travel — Your First 48 Hours in Japan

Initial scenarios:

1. Airport
2. Train
3. Hotel check-in
4. Restaurant
5. Convenience store
6. Asking directions
7. Shopping
8. Emergency / help

## 🎓 Study — Your First Week as a Student

Initial scenarios:

1. Airport
2. Train
3. University check-in
4. Meeting classmates
5. Asking a professor
6. Finding a classroom
7. Convenience store
8. Part-time job

## 💼 Work — Your First Week at Work

Initial scenarios:

1. Airport
2. Train
3. Convenience store
4. Restaurant
5. Office introduction
6. Meeting
7. Asking for clarification
8. End-of-day interaction

## 🏠 Relocation — Your First Month in Japan

Future scenarios:

1. Airport
2. Train
3. Apartment
4. City office
5. Bank
6. Mobile SIM
7. Supermarket
8. Workplace

---

# 8. Keep Implementation 2 Small

Do **not** build every scenario for every goal immediately.

For Implementation 2, build one focused journey for each goal:

| Goal | Initial Journey |
|---|---|
| ✈️ Travel | First 48 Hours |
| 🎓 Study | First Day at University |
| 💼 Work | First Week at Work |
| 🏠 Relocation | First Week in Japan |

Each path can initially contain **3–5 scenarios**.

Expand only after testing.

> **Do not let a three-day MVP become a three-month project.**

---

# 9. Survival Skills

The current application is organized around **situations**.

Add a second learning dimension:

## Situations

- Airport
- Train
- Restaurant
- Work

## Skills

- Ask
- Understand
- Respond
- Clarify
- Refuse politely
- Request help
- Confirm
- Apologize

This changes the outcome from:

> "I completed a scenario."

to:

> "I can perform a real-world communication skill."

---

# 10. Ability-Based Learning

Current feedback includes:

- Excellent
- Natural
- Understandable
- Needs improvement

Keep useful feedback, but add an ability-based summary.

### Example

**You practiced:**

- 🗣 Asking for directions
- 🗣 Clarifying information
- 🗣 Confirming a destination
- 🗣 Making polite requests

**You can now:**

- Ask where something is.
- Ask someone to repeat themselves.
- Make a polite request.

This gives the learner an **ability outcome**, not just a score.

---

# 11. "Can I Actually Say It?"

This should become one of the central learning loops.

```text
You learned:

もう一度お願いします。
"One more time, please."

       ↓

🔊 LISTEN

       ↓

🗣 SAY IT

       ↓

🎭 USE IT IN A SITUATION

       ↓

✓ CAN USE IT
```

This is more meaningful than:

```text
MEMORIZE → MCQ → XP
```

---

# 12. Confidence Check

At the end of each scenario, ask:

> **Could you handle this in real life?**

Options:

| Option | Meaning |
|---|---|
| 😰 **Not yet** | Needs more practice |
| 🙂 **Almost** | Some uncertainty remains |
| 💪 **I could handle it** | Feels ready |

This is a **self-assessment**, not a gamification score.

If the learner selects **Almost**, suggest:

> Rehearse the 2 phrases you struggled with.

This can later become the foundation for personalization.

---

# 13. Scenario Branching

The current scenario model contains `nextStepId`, but branching is not being used.

Implementation 2 should introduce basic branching.

### Example

NPC:

> `東京駅はどこですか？`

Learner chooses:

**A — Polite response**

→ NPC responds normally.

**B — Too vague**

→ NPC asks:

> `東京駅ですか？`

The learner must clarify.

**C — Wrong response**

→ The NPC should respond naturally instead of showing:

> "Incorrect!"

### Core Principle

The learner should experience:

> **Consequence, not quiz grading.**

---

# 14. Conversation Flow

Replace:

```text
Question
   ↓
A / B / C
   ↓
Correct!
   ↓
Next
```

with:

```text
NPC SPEAKS
    ↓
LEARNER RESPONDS
    ↓
NPC REACTS
    ↓
SITUATION CHANGES
    ↓
LEARNER RESPONDS AGAIN
```

This moves Life Mode closer to a simulation without requiring AI.

---

# 15. Unexpected Moments

Real conversations are unpredictable.

Add unexpected moments after the main task.

### Example

NPC suddenly says:

> `すみません、今日は混んでいます。`

The learner must understand and respond.

Other examples:

> `現金ですか、カードですか？`

> `日本語はわかりますか？`

The learner should experience:

> **"I don't know exactly what they're going to say."**

This directly supports the problem Life Mode is trying to solve: freezing during real conversations.

---

# 16. Immersive Scenario Design

## Example: Restaurant

Instead of a static restaurant illustration:

```text
              RAMEN SHOP

        ┌──────────────────┐
        │ いらっしゃいませ │
        │                  │
        │       🍜         │
        │                  │
        │      STAFF       │
        └──────────────────┘

               👤 YOU

          "What would you say?"
```

Add:

- Subtle environmental animation
- Character reactions
- Contextual objects
- Dialogue transitions
- Scenario-specific UI

Small environmental details should create a sense of immersion.

---

# 17. Environmental Sound

Use subtle environmental sounds in addition to Japanese dialogue.

| Scenario | Environmental Sound |
|---|---|
| ✈️ Airport | Announcement ambience |
| 🚆 Train | Station ambience |
| 🍜 Restaurant | Quiet restaurant ambience |
| 🏪 Convenience Store | Store ambience |
| 💼 Workplace | Office ambience |

Environmental sound should be optional.

Provide separate controls:

```text
🔊 Voice
🔈 Environment
```

Always provide a mute option.

---

# 18. Three-Layer Audio System

| Layer | Purpose | Priority |
|---|---|:---:|
| **1. NPC Voice** | Japanese dialogue | Required |
| **2. Learner Speaking** | Speaking practice | Required |
| **3. Environment** | Immersion | Optional |

The learning interaction should remain more important than background music or decorative sound.

---

# 19. Immersion Layer

The combination of:

```text
GRAPHICS
   +
AUDIO
   +
INTERACTION
```

should create the immersion layer.

The current implementation mainly uses entrance and interaction animations.

Implementation 2 should move toward **environmental interaction**.

### Example Interaction

```text
NPC MESSAGE APPEARS
        ↓
FADE IN
        ↓
🔊 JAPANESE AUDIO
        ↓
DIALOGUE BUBBLE APPEARS
        ↓
USER CHOOSES
        ↓
NPC REACTS
        ↓
NEW DIALOGUE
        ↓
CULTURE NOTE
```

---

# 20. Technical Fixes

These issues should be fixed before adding too much new functionality.

## P0 — Progress Reset

`resetProgress()` currently runs whenever setup is submitted.

### Problem

Returning to setup can wipe saved progress.

### Fix

Prevent setup submission from unintentionally resetting existing progress.

---

## P1 — Mid-Scenario Resume

Only the step index is currently restored.

### Problem

Choice and phase state are not fully restored.

### Fix

Improve the persistence model so the complete scenario state can be restored.

---

## P1 — Branching

`nextStepId` exists but is not actually used.

### Fix

Implement the branching engine.

---

## P1 — Completion Route

`/complete` can apparently be accessed before the journey is completed.

### Fix

Protect the completion route and verify completion state before allowing access.

---

## P1 — Automated Tests

Current test coverage is 0%.

You do not need hundreds of tests, but core behavior should be covered.

### Test Areas

- Scenario progression
- Unlocking
- Replay
- Persistence
- Branching
- Goal selection

---

## P2 — Technical Cleanup

Clean up:

- Unused `AsyncStorage` dependency
- Unused `CompletionCard`
- Missing ESLint configuration
- Unused `fadeOutAnim`
- Unused `expo-font` configuration

---

# 21. What Not to Build Yet

Do **not** add the following to Implementation 2:

| Feature | Decision |
|---|:---:|
| Authentication | ❌ Not yet |
| Backend | ❌ Not yet |
| PostgreSQL | ❌ Not yet |
| Payments | ❌ Not yet |
| Social network | ❌ Not yet |
| Human language exchange | ❌ Not yet |
| AI tutor | ❌ Not yet |
| AI avatar | ❌ Not yet |
| Complex recommendation engine | ❌ Not yet |
| Native mobile application | ❌ Not yet |
| Subscription | ❌ Not yet |
| Leaderboards | ❌ Not yet |
| XP | ❌ Not yet |
| Streaks | ❌ Not yet |

### Why?

The current product hypothesis is:

> **Does scenario-based rehearsal make users feel more prepared for real interactions?**

That should be validated before adding expensive infrastructure and features.

---

# 22. Implementation 2 User Flow

```text
                         LIFE MODE
                            │
                            ▼
                     "Going to Japan?"
                            │
              ┌─────────────┴─────────────┐
              ▼                           ▼
       BEFORE YOU LAND               START JOURNEY
              │                           │
              ▼                           ▼
        SURVIVAL PACK                 CHOOSE GOAL
              │                           │
       ┌──────┼──────┐          ┌────────┼─────────┐
       │      │      │          │        │         │
     Speak  Listen  Help      Travel    Study     Work   Relocate
       │      │      │          │        │         │
       └──────┴──────┘          └────────┴─────────┘
              │                           │
              └─────────────┬─────────────┘
                            ▼
                     REAL SITUATION
                            │
                            ▼
                        LISTEN 🔊
                            │
                            ▼
                       UNDERSTAND
                            │
                            ▼
                        SPEAK 🎙
                            │
                            ▼
                       RESPOND
                            │
                            ▼
                       NPC REACTS
                            │
                            ▼
                     CULTURE NOTE
                            │
                            ▼
                  UNEXPECTED MOMENT
                            │
                            ▼
                     SITUATION DONE
                            │
                            ▼
                 "CAN YOU HANDLE THIS?"
```

---

# 23. Exact Implementation 2 Scope

## MUST HAVE

### Product

- [ ] Before You Land
- [ ] Travel goal
- [ ] Study goal
- [ ] Work goal
- [ ] Relocation goal
- [ ] Goal-specific journey metadata
- [ ] Survival phrases
- [ ] Audio playback
- [ ] Listen mode
- [ ] Shadow mode
- [ ] Speak mode
- [ ] Better scenario visuals
- [ ] Scenario-specific environments
- [ ] Better dialogue presentation
- [ ] Unexpected moments
- [ ] Basic branching
- [ ] Ability-based completion summary

### Technical

- [ ] Audio abstraction
- [ ] Scenario branching engine
- [ ] Correct progress persistence
- [ ] Correct setup behavior
- [ ] Completion guard
- [ ] Tests for core progression
- [ ] ESLint setup
- [ ] Remove unused dependencies/components
- [ ] Mobile responsiveness re-test

---

## SHOULD HAVE

- [ ] Self-confidence check
- [ ] Replay weak phrases
- [ ] Skill tracking
- [ ] Environmental sound toggle
- [ ] Audio speed control
- [ ] Hide/show English
- [ ] Hide/show romaji
- [ ] Japanese-only mode
- [ ] Scenario summary
- [ ] Practice Again mode

---

## DO NOT BUILD YET

- [ ] Authentication
- [ ] Backend
- [ ] PostgreSQL
- [ ] Payments
- [ ] Social network
- [ ] Human language exchange
- [ ] AI tutor
- [ ] AI avatar
- [ ] Complex recommendation engine
- [ ] Native mobile application
- [ ] Subscription
- [ ] Leaderboards
- [ ] XP
- [ ] Streaks

---

# 24. Product Positioning

The product should occupy a specific position rather than trying to compete broadly with every language-learning application.

| Product | Core Approach |
|---|---|
| **Duolingo** | Build a language-learning habit |
| **Pimsleur** | Train through audio/conversation |
| **Teuida** | Speak through real-life roleplay and pronunciation practice |
| **Praktika** | Practice conversation with AI tutors |
| **Life Mode** | Prepare for the exact situations you are about to experience |

### Positioning to Test

> **Going to Japan? Rehearse your first week before you arrive.**

Avoid generic positioning such as:

- "An AI language learning app."
- "A better Duolingo."
- "Learn Japanese through conversations."

The product should communicate a specific use case.

---

# 25. Landing Page Direction

## Hero

# Going to Japan?

### Practice your first conversations before you get there.

Supporting copy:

> Airport. Train. Restaurant. Work. Real situations.

> Listen. Speak. Respond. Learn what actually works.

### Primary CTA

**Prepare for Japan →**

### Secondary CTA

**Try a situation**

Immediately demonstrate the product:

```text
✈️ AIRPORT

"Ask for the train to Tokyo."

🔊 Listen

🎙 Say it

💬 Respond
```

The landing page should **demonstrate the product rather than only explain it**.

---

# 26. MVP Success Test

Do not optimize for "perfect."

The important question is:

> **Give someone who is actually planning to visit, work, or study in Japan 15 minutes with Life Mode. Does it make them feel more prepared for a real interaction?**

### If YES

The core product experience is worth expanding.

### If NO

Do not hide the problem by adding more features.

The correct response is to improve the core experience and test again.

---

# Implementation 2 Thesis

## LIFE MODE = PRE-DEPARTURE + REAL-WORLD REHEARSAL

```text
BEFORE YOU LAND
       ↓
SURVIVAL BASICS
       ↓
LISTEN
       ↓
SPEAK
       ↓
REHEARSE
       ↓
REALISTIC SCENARIO
       ↓
UNEXPECTED RESPONSE
       ↓
CULTURAL CONTEXT
       ↓
CONFIDENCE CHECK
       ↓
"YOU'RE READY"
```

### Final Direction

> **Turn Life Mode from a generic scenario-based language-learning MVP into a focused pre-departure and real-world rehearsal experience.**

