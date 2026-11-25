# Gap research: lifting app flows, Mobbin blocked

## Method

Mobbin redirected to its home page with a redirect_to parameter, which means the browser is not signed in there. Per the brief, Mobbin was not pursued further. Sources were the vendors' own help centers, product pages and app store listings, read through the user's browser.

No tap count in this file was counted from a live screen. Every figure is either stated by a vendor source (marked "stated") or left as "not reached". Onboarding screen counts, bottom-nav tabs beyond those named, and taps per logged set were not observed for any app.

## Comparison

| App | Onboarding | Bottom-nav tabs | Taps to log one set | Rest timer start | Swap, note, superset, warm-up | Coach or AI | Sources |
|---|---|---|---|---|---|---|---|
| Hevy | Not counted. Trainer intake lists 11 questions plus one health-terms acceptance (stated, Trainer only) | Workout and Coach named (stated). Others not reached | Not reached | Starts when a set is marked complete, set per exercise (stated) | Superset: three-dot menu, Add To Superset (stated). Warm-up: tap set number, W - Warm up set (stated). Swap and note paths not reached | Hevy Trainer: Pro feature, program built by an algorithm, help states it does not use AI (stated). Hevy Coach: human coaching, Coach tab (stated) | help.hevyapp.com/hc/en-us/articles/35385404949143 (rest timer); .../34896293707927 (set types); .../35650286563095 (supersets); .../38385724273047 (Trainer); .../38279631262359 (Coach subscription) |
| Strong | Not reached | Not reached | Not reached | Not reached | Not reached | Not reached | strongapp.io timed out, no page loaded |
| Fitbod | Not counted. Help says onboarding asks about experience, goals and equipment (stated, no count) | Workout and Log named (stated). Others not reached | Not counted. Help describes tap field, type value, swipe to delete (stated) | Rest timer sits below the exercise name, tap to adjust (stated). Start trigger not stated | Swap: swipe left, Replace (stated). Warm-up: More, Add Warm-Up Set (stated). Superset: three dots, Build Superset/Circuit (stated). Note: More, Notes (stated) | Per-exercise AI recommendations for sets, reps and weight (stated). No separate coach found | help.fitbod.me/hc/en-us/articles/360006335593 (editing workouts); Exercise Details Screen article in Getting Started; .../30721771750039 (new user guide) |
| Alpha Progression | Not reached | Not reached | Not reached | "Rest timer with alarm" listed as a feature. Start trigger not reached | Swap for today or in the plan (stated, FAQ). Superset, dropset, notes listed as features (stated, no path) | Pro plan generator and per-set weight and rep recommendations (stated, Pro only) | alphaprogression.com/en and alphaprogression.com/en#faq |
| JEFIT | Not reached | Workout and Progress tabs named (stated). Coach page linked in footer, not read | Not counted. Vendor says most sets take a single tap to confirm, with last session pre-filled (stated, vendor claim) | Starts automatically when a set is logged, no extra tap (stated) | Swap on the log screen, Elite only (stated). Note on any exercise (stated). Superset: three-dot menu, Add a superset (stated). Warm-up: set type (stated) | Elite "Your next weight" suggests weight and target reps (stated). Coach page not read | jefit.com/features/log-track; jefit.com/features/rest-timer |
| Gravl | Not counted. Essentials article lists setup sections, not screens | Not reached (app site not live, store page not loaded) | Not reached | Help article "Adjust Your Rest Times" exists. Body not captured | Help articles exist for Replace an Exercise, Create a Superset. Body not captured. Warm-up: number of warm-up sets selectable (stated, article summary) | Described as an AI personal trainer that coaches each workout (stated, search snippet) | gravl.ai/help; gravl.ai/help/gravl-essentials-set-up-your-fitness-plan; DuckDuckGo result for apps.apple.com/us/app/personal-trainer-gravl/id6450921637 |
| Strava | Not reached | Not reached | Not reached | Not reached | Not reached | Not reached | Not reached |
| Whoop | Not reached | Not reached | Not reached | Not reached | Not reached | Not reached | Not reached |
| Oura | Not reached | Not reached | Not reached | Not reached | Not reached | Not reached | Not reached |
| Peloton | Not reached | Not reached | Not reached | Not reached | Not reached | Not reached | Not reached |

## Prose

Hevy's help center documents the rest timer as starting when a set is marked complete, and documents superset and warm-up entry through the set number and three-dot menus. JEFIT's product page documents the same automatic start and places warm-up in the set type. Fitbod documents the rest timer as a control below the exercise name, with no stated start trigger. Alpha Progression and Gravl pages describe features without the screens that deliver them, so their rows carry the feature names only.

The coach column differs by vendor. Hevy has two different things, an algorithm-built program (Trainer) and a human coaching service (Coach). Fitbod and Alpha Progression describe per-set recommendations. Gravl describes an AI trainer, sourced from a search snippet only.

## What this means for Delt Arena

Delt Arena's predictive mode logs a set in one tap, which is the target to hold. None of the sources here counted taps on a live screen, so no competitor baseline exists yet. JEFIT's single-tap claim is the closest public statement, and it remains a vendor claim.

Two patterns are documented often enough to design around: the rest timer starts on set completion with no separate tap (Hevy, JEFIT), and warm-up, superset and swap sit behind a set-number or three-dot menu (Hevy, Fitbod, JEFIT). Delt Arena's one-tap path should not depend on those menus. A real tap count needs a logged session in each app on a test account, which this pass did not do.

## Still not reached

1. Mobbin flows for all six apps and the optional four. Mobbin needs sign-in.
2. Strong. strongapp.io timed out.
3. Gravl in-app screens. gravl.ai/app returns no live app, and the help article bodies for rest, replace, and superset were not captured.
4. Taps per logged set for all six apps. None counted on a live screen.
5. Onboarding screen counts for all six apps.
6. Bottom-nav tabs beyond the names listed in the table.
7. Alpha Progression logging screens and rest timer start trigger.
8. Strava, Whoop, Oura, Peloton.
9. YouTube walkthrough transcripts. Searched, none read.
