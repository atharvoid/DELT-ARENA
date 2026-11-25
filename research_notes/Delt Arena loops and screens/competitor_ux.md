# Competitor UX teardown: gym and machine-cardio tracking apps (Android focus)

**Method limits (read first):** Every WebFetch failed (getaddrinfo ENOTFOUND for play.google.com, alphaprogression.com, help.hevyapp.com, sensai.fit, techbloat.com). Only WebSearch snippets were available, so nothing below comes from reading a full page. Reddit, Mobbin/Refero and Play Store review pages were not reachable. Many sources are vendor-authored comparisons (Alpha Progression, Hevy, Jefit, Boostcamp blogs) and are flagged. No screen-by-screen flows (tab bars, taps per set, onboarding step counts, exercise media format) could be verified. Those are in Gaps and need a network allowlist or manual app testing. Date of research: 2026-11-25.

## 1. Navigation model, home screen, set-logging flow, taps per set

### Takeaway
Not verified. No source I could reach describes tab bars, home screens or per-set tap counts for any app. Only fragments exist (Hevy rest-timer widget controls, Fitbod equipment profiles, Gravl gym profile creation).

### Cited Findings
- Hevy's help center says its Live Activity widget works on iOS and Android and lets you add or subtract 15 seconds on the rest timer or skip it. — [Hevy help](https://help.hevyapp.com/hc/en-us/articles/35649846517399) (search snippet only)
- Hevy's feature page says the Android widget needs lock screen, badge and pop-up notification types enabled for Hevy, and shows the rest timer, current exercise and next set. — [Hevy feature page](https://www.hevyapp.com/?p=10624) (snippet)
- Fitbod lets users save different equipment setups as profiles (home gym vs commercial gym). — [ScreensDesign Fitbod teardown](https://screensdesign.com/showcase/fitbod-gym-fitness-planner) (snippet)
- Gravl onboarding creates a first "gym profile"; its help center tells users to check the equipment list before the first workout, and starting weights come from onboarding answers. — [Gravl help](https://intercom.help/gravl/en/articles/10185534-gravl-essentials-set-up-your-fitness-plan) (snippet)
- Setgraph positions itself as exercise-first logging for lifters without a fixed routine. — [Jefit-published roundup](https://www.jefit.com/wp/guide/best-workout-apps-for-2026-top-7-options-tested-and-reviewed/) (vendor-adjacent; competitor's own blog)
- Strong is described as a quiet, minimal, mature logging flow, best for lifters who already have a program. — [aggregated 2026 comparisons via search](https://www.techbloat.com/10-lifting-apps-compared-for-easier-progressive-overload.html) (snippet summary only)

### Inferences
- A tap-only AI coach has no tab-bar or set-flow benchmark here. The team should install Hevy, Strong, Alpha Progression and Gravl on a device and count taps themselves.

### Gaps
- Tab structure, home screen, tap count per set: not found for any app. Mobbin/Refero not reachable; Play Store blocked.
- Liftosaur: no search result at all.

## 2. Rest timer presentation (notification, lock screen, widget)

### Takeaway
Hevy uses a live-activity-style widget/notification on Android with +/-15s and skip. Alpha Progression lists "Android live notifications". Hevy's Android timer has a history of background reliability bugs.

### Cited Findings
- Hevy Live Activity on Android: +/-15s and skip controls. — [Hevy help](https://help.hevyapp.com/hc/en-us/articles/35649846517399)
- Hevy 1.30.30 release notes: fixed rest timer alarm not going off in background on some Android 14 devices. — [APKMirror 1.30.30](https://www.apkmirror.com/apk/hevy-gym-workout-tracker/hevy-gym-log-workout-tracker/hevy-gym-log-workout-tracker-1-30-30-release/)
- Hevy 1.30.27: included instructions for fixing background rest-timer problems on Android 14 via notification settings. — [APKMirror 1.30.27](https://www.apkmirror.com/apk/hevy-gym-workout-tracker/hevy-gym-log-workout-tracker/hevy-gym-log-workout-tracker-1-30-27-release/)
- Hevy 1.29.14: rolled back the persistent rest-timer notification because it caused issues on some devices (older, undated version). — [APKMirror 1.29.14](https://www.apkmirror.com/apk/hevy-gym-workout-tracker/hevy-gym-log-workout-tracker/hevy-gym-log-workout-tracker-1-29-14-release/)
- Alpha Progression's site lists "Android live notifications" and a rest timer with alarm in the free tier. — [alphaprogression.com](https://alphaprogression.com/en) (vendor, snippet)
- Hevy Wear OS app exists, syncs live with the phone and has a tile. — [APKMirror Hevy Wear OS](https://www.apkmirror.com/apk/hevy-gym-workout-tracker/hevy-gym-log-workout-tracker-wear-os); a Play reviewer praises it as free and well set up — [Play listing](https://play.google.com/store/apps/details?id=com.hevy) (snippet)

### Inferences
- Rest-timer reliability under Android battery management (Doze, OEM killers) is a recurring product risk. A foreground service with exact alarms is the robust route, and Hevy's rollback history shows what happens otherwise.

### Gaps
- Whether the Hevy widget mirrors to Wear OS: not stated in any source found.
- Timer UX in Strong, Fitbod, Gravl, Boostcamp, JEFIT, MacroFactor: not found.

## 3. Supersets, drop sets, warm-ups, plate calculator, RPE/RIR, notes, swaps, editing past sets

### Takeaway
Only feature gating was recoverable. Plate and warm-up calculators are Pro-only in Strong. RIR is Pro-only in Alpha Progression but free in Hevy. Boostcamp is said to give RPE, supersets and drop sets free.

### Cited Findings
- Strong: plate calculator and warm-up calculator are PRO only; free tier is 3 custom routines with unlimited workouts. — [AI Tools Bakery Strong review](https://aitoolsbakery.com/blog/strong-app-review/); [App Store listing](https://apps.apple.com/il/app/id464254577)
- Alpha Progression free tier: unlimited logging, supersets, dropsets, rest timer with alarm, exercise videos, body measurements, CSV export, no ads, no account. RIR tracking requires Pro. — [alphaprogression.com](https://alphaprogression.com/en); RIR gating also stated in [Hevy's comparison](https://www.hevyapp.com/?p=18340) (competitor-authored, which also claims Hevy offers RPE/RIR free)
- Boostcamp free tier described as full tracker including RPE logging, supersets, drop sets, Weekly Report, no routine cap — [Boostcamp budget page](https://www.boostcamp.app/best/budget) (vendor)
- Gravl help claims its drop sets and varied set schemes beat Fitbod — [Gravl help](https://help.gravl.ai/en/articles/11173711-fitbod-vs-gravl) (vendor)
- MacroFactor Workouts: custom routines with weight, reps, RIR, "advanced set types", auto-progression, rep-progression schemes (Static, Linear, Reverse Linear, Undulating). — [MacroFactor Workouts page](https://macrofactor.com/workouts/); [Play listing](https://play.google.com/store/apps/details?id=com.sbs.train); [APKPure](https://apkpure.com/macrofactor-workouts---tracker/com.sbs.train)
- Hevy enforces a 150-set limit per workout/routine even on Pro. — [Hevy help Pro article](https://help.hevyapp.com/hc/en-us/articles/35119778922263)

### Inferences
- Gating warm-up/plate calculators behind Pro (Strong) is a common complaint area; making them free is a cheap differentiator. (Complaint evidence not verified.)

### Gaps
- Superset UI, swap flow, past-set editing, notes: not found for any app. Hevy superset/plate calc support not confirmed by my search.

## 4. Exercise media

### Gaps (entire section)
No reliable source retrieved on GIF/video/3D/still format per app. Only: Jefit claims 1,400+ exercises with HD demos, muscle activation maps and form instructions ([Jefit blog, vendor](https://www.jefit.com/wp/guide/best-workout-apps-for-2026-top-7-options-tested-and-reviewed/)); Alpha Progression lists exercise videos in its free tier ([alphaprogression.com](https://alphaprogression.com/en)). Presentation (inline vs full-screen) unknown.

## 5. Complaints and praise

### Takeaway
Verified complaint evidence is thin: Hevy rest-timer reliability on Android, Fitbod billing and repetitiveness. Praise: Hevy's price and free Wear OS app.

### Cited Findings
- Hevy timer complaints (stops at 30s, muted, auto shuts off, silent when app backgrounded) from an independent blog and an AI-aggregated review site — [dr-muscle review](https://dr-muscle.com/hevy-workout-app-review/); [JustUseApp Hevy](https://justuseapp.com/en/app/1458862350/hevy-gym-trainingstagebuch/reviews) (iOS-sourced aggregation, weak)
- Hevy Play listing shows about 290K reviews; one reviewer praises the free Wear OS app. — [Play listing](https://play.google.com/store/apps/details?id=com.hevy) (snippet, rating not captured)
- Fitbod: Trustpilot reports of paid-but-locked accounts and unresponsive support; slow, crashing, hard to navigate; algorithm generic early; repetitive workouts. — [Indie Hackers review](https://www.indiehackers.com/post/fitbod-app-review-2026-honest-take-after-real-testing-45d5f07a1b); [Trustpilot](https://www.trustpilot.com/review/fitbod.me); [Sikayetvar](https://www.sikayetvar.com/en/fitbod-us/fitbod-gave-me-repetitive-workouts-and-an-unreliable-app-experience)
- Fitbod praised for customizing workouts to feedback and equipment — [Indie Hackers](https://www.indiehackers.com/post/fitbod-app-review-2026-honest-take-after-real-testing-45d5f07a1b)
- Gravl: one reviewer calls it a "straight up Fitbod copycat"; JustUseApp aggregate says 66.7% positive from 2,277 reviews (automated, weak); a reviewer praises its public feedback board. — [SensAI](https://www.sensai.fit/blog/gravl-app-review-2026); [JustUseApp Gravl](https://justuseapp.com/en/app/6450921637/personal-trainer-gains-ai/reviews)
- Ratings (vendor-reported): Alpha Progression 4.9 App Store / 4.8 Google Play as of Sept 2026 — [alphaprogression.com glossary](https://alphaprogression.com/en/glossary/alpha-progression). Jefit Android 4.45 vs iOS 4.8 per a Jefit-authored roundup — [Jefit blog](https://www.jefit.com/wp/guide/best-workout-apps-for-2026-top-7-options-tested-and-reviewed/). Fitbod 4.8 from 288K and Gravl 4.9 from ~6K App Store ratings — [SensAI](https://www.sensai.fit/blog/gravl-vs-fitbod-2026)

### Gaps
- No Google Play review text with URLs retrieved; no Reddit threads (r/Hevy, r/strongapp, r/fitbod etc.) reachable via search results.

## 6. AI-programming onboarding (Fitbod, Gravl, Alpha Progression)

### Takeaway
Fitbod asks goal and experience level, plus equipment profiles; Gravl builds from onboarding answers plus a gym profile. Question counts and duration were not found.

### Cited Findings
- Fitbod: goal (e.g., get stronger, build muscle) and experience (beginner/intermediate/advanced); full onboarding and first generated workout are free; first paywall appears after workout generation but before start (yearly with "Save 50%" vs monthly), second paywall after workout summary. — [Indie Hackers](https://www.indiehackers.com/post/fitbod-app-review-2026-honest-take-after-real-testing-45d5f07a1b); [ScreensDesign](https://screensdesign.com/showcase/fitbod-gym-fitness-planner)
- Fitbod builds sessions from goals, experience, equipment, time, history and recovery estimates (Fitbod's own claim). — [Fitbod blog](https://fitbod.me/blog/fitbod-vs-gravl-strength-training-app-review/)
- Gravl: plan from onboarding info; first gym profile created; frequency, variety and duration settings; "consistent" variety suggested to beginners. — [Gravl help](https://intercom.help/gravl/en/articles/10185534-gravl-essentials-set-up-your-fitness-plan)

### Gaps
- Alpha Progression onboarding: not found. Exact question lists and time to complete: not found for any.

## 7. Pricing and paywall placement

### Cited Findings
- Hevy: free = 4 routines, 7 custom exercises, 3 months of graph history; Pro $2.99/mo, $23.99/yr or $74.99 lifetime (one outlier source disagrees). — [Hevy help](https://help.hevyapp.com/hc/en-us/articles/35119778922263); [AI Tools Bakery Hevy](https://aitoolsbakery.com/blog/hevy-review/); [Hevy comparison](https://www.hevyapp.com/?p=18340) gives $23.99/yr vs Alpha $79.99/yr
- Alpha Progression: $12.99/mo or $79.99/yr US, 14-day trial on annual for eligible new users (older pages cite other numbers). — [alphaprogression.com](https://alphaprogression.com/en)
- Strong: PRO $4.99/mo or $29.99/yr per one listing; a 2026 review says $3.99/$23.99 (conflict, likely regional). — [App Store](https://apps.apple.com/il/app/id464254577); [AI Tools Bakery Strong](https://aitoolsbakery.com/blog/strong-app-review/)
- Fitbod $15.99/mo or $95.99/yr; Gravl $14.99/mo or $59.99-$89.99/yr; Gravl has 3 free workouts, Fitbod blocks starting workouts until paid. — [SensAI](https://www.sensai.fit/blog/gravl-app-review-2026)
- Boostcamp free tier described as full tracker (vendor claim; another comparison lists "Trial only", conflict). — [Boostcamp](https://www.boostcamp.app/best/budget); [Jefit roundup](https://www.jefit.com/wp/guide/best-workout-apps-for-2026-top-7-options-tested-and-reviewed/)
- Jefit prices conflict across sources ($12.99/mo + $69.99/yr vs Elite $9.99/mo). Setgraph sources conflict (free forever vs Pro Membership). — Jefit roundup above; [Setgraph App Store](https://apps.apple.com/us/app/setgraph-workout-tracker/id1209781676)
- MacroFactor Workouts price: not found.

### Inferences
- Hevy's cheap-logger model and the AI-coach apps at roughly $60-96/yr leave a pricing gap for a mid-priced coach, but this is unvalidated.

## 8. Android-specific support

### Cited Findings
- Hevy: Android Live Activity widget, Wear OS app and tile (above).
- Alpha Progression: Android live notifications (vendor).
- Strong: a single review found no Wear OS app; Apple Watch lacks plate/warm-up calculators. — [AI Tools Bakery Strong](https://aitoolsbakery.com/blog/strong-app-review/)
- Jefit: Wear OS and web listed (vendor roundup). Boostcamp, Setgraph: Android listed; Setgraph web too. — Jefit roundup above
- MacroFactor Workouts is on Google Play (package com.sbs.train); min Android version conflicting (8.0 vs 10.0) across listings. — [APKPure](https://apkpure.com/macrofactor-workouts---tracker/com.sbs.train); launched per [MacroFactor Jan 2026 newsletter](https://macrofactor.com/mm-jan-2026/)

### Gaps
- Health Connect support per app, home-screen widgets (non-timer), Fitbod/Gravl Android parity: not found. Fitbod/Gravl comparison coverage is mostly iOS.
- 2025-2026 newcomers beyond Gravl and MacroFactor Workouts: not identified (Strongsplit appeared in one result but unexamined).

## Candidate gaps for a new flagship (inferences, not verified)
- Reliable Android rest timer (foreground service, exact alarms) given Hevy's documented Android 14 issues.
- Free warm-up and plate calculators (Strong gates them).
- Machine-cardio logging: no source found describing how any app handles it.
