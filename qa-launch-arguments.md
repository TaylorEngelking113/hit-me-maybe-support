# QA and UI-test launch arguments

These hooks let QA agents and UI tests reach a deep state directly instead of tapping through it. They are DEBUG-only unless the table says otherwise; Release builds ignore them. Pass arguments with `xcrun simctl launch <udid> com.engelking.HitMeHuman <args…>` (or `XCUIApplication.launchArguments`). Pass `UI_TEST_SCREEN` as an environment variable: `SIMCTL_CHILD_UI_TEST_SCREEN=<screen> xcrun simctl launch …` (or `XCUIApplication.launchEnvironment`).

DEBUG builds are **Pro by default**. Add `--force-free-tier` for anything that involves energy, ads or the paywall.

## Jump straight to a screen: `UI_TEST_SCREEN`

The router lives in `HitMeMaybe/HitMeMaybeApp.swift` (`UITestScreen`). It skips the splash and Home.

| Value | Opens |
|---|---|
| `home` | Home |
| `practice` | Practice table |
| `flashcards` | Flash cards (study) |
| `quiz` | Quiz hub |
| `drill` | Drill hub |
| `story` | Story map |
| `stats`, `trends`, `monthly` | Stats, Trends, Monthly competition |
| `cheatsheet` | Cheat sheet |
| `settings` | Settings |
| `paywall` | Paywall |
| `achievements` | Achievement gallery |
| `countdown` | Deck Countdown. The rung comes from `--countdown-mode` (default `fullDeck`). |

## State jumps

| Argument | Effect | Example |
|---|---|---|
| `--seed-shoe=<n>` | The Practice shoe is a deterministic 6-deck shuffle seeded with `n` (UInt64). It replaces any saved shoe. Seed `5` deals player 4+10 (hard 14) against a dealer 6, with no naturals; the Practice UI tests use it (#45). | `--seed-shoe=5` |
| `--seed-energy=<n>` | Sets today's remaining free energy to `n` (clamped to 0…50). Needs `--force-free-tier`. The value is saved and **persists until midnight ET** on that simulator; relaunch with `--force-free-tier --seed-energy=50` to refill. | `--force-free-tier --seed-energy=0` (first Deal shows the out-of-energy sheet) |
| `--countdown-mode=<mode>` | The rung that `UI_TEST_SCREEN=countdown` opens: `tagWarmup`, `halfDeck`, `fullDeck` or `timed`. | `--countdown-mode=halfDeck` |
| `--countdown-at-entry` | An entry-mode Deck Countdown (any rung except `tagWarmup`) skips the card reveal and opens on the count-entry keypad. It applies to every Deck Countdown screen in that launch, including ones opened from the Card Counting hub. A jumped run awards no XP or daily-goal credit. A full deck always counts to **0**. | `UI_TEST_SCREEN=countdown --countdown-at-entry` |
| `--force-split` | Practice's opening hand is a pair, and the dealer's hole card is a 6. | |
| `--force-free-tier` | Turns off the DEBUG Pro unlock (free tier: energy, ads, paywall). | |
| `--show-paywall` | Home opens the paywall on its first appearance. | |
| `--stub-ad=reward` / `--stub-ad=fail` | Rewarded ads use the offline stub, which either grants the reward or closes early. | `--force-free-tier --seed-energy=0 --stub-ad=reward` |
| `--ump-debug-eea` | Google consent treats the simulator as being in the EEA, so the consent form appears. | |
| `--enable-card-counting-hud` / `--card-counting-quiz` | Shows the Practice count HUD, or puts it in quiz mode, without changing Settings. | |
| `--show-hilo-primer` | Deck Countdown warmup always shows the Hi-Lo primer. | |
| `--force-counting-nudge` | Home shows the "learn counting" nudge. | |

## Test harness and data

| Argument | Effect |
|---|---|
| `--uitest` | Skips the splash dwell, resets career progress once, uses the stub ad provider, and skips Game Center sign-in and ad startup. **Not DEBUG-gated**: it is checked in shipping code paths too. |
| `--seed-rich-data` | On an empty store, inserts a deterministic data set (used by the upgrade-regression harness). |
| `--seed-store=corrupt` | Writes an invalid store before launch, to exercise the no-data-loss recovery ladder. |
| `--verify-rows` | Exposes a row-count probe element for UI tests. |

## Adding a new one

Read it through `DebugLaunch` (`HitMeMaybe/DebugLaunchSupport.swift`) behind `#if DEBUG`. Put the parsing in a pure function and add a unit test in `HitMeMaybeTests/DebugLaunchTests.swift`. Then add a row here.
