# Android + Flutter platform reference for a gym + machine-cardio app (late 2026)

Research note. Date of research: 2026-11-25. Several key hosts were unreachable from the research sandbox (DNS failure, i.e. not in the allowed network list): m3.material.io, blog.google, android-developers.googleblog.com, docs.flutter.dev, design.google, play.google.com, gs.statcounter.com. Claims that would have come from those hosts are listed under Gaps, not reconstructed from memory.

## Material 3 Expressive: what changed and how Flutter adopts it

### Takeaway
M3 Expressive is a research-backed refresh (springy motion, shape morphing, variable fonts, deeper tonal color, new components). Flutter does NOT ship it in the SDK as of the latest evidence (Aug 2026): Material/Cupertino are being decoupled into standalone packages and Expressive work is expected there, so a flagship Flutter app must either use a community package or build Expressive components itself on its own design-token layer.

### Cited Findings
- Google says Expressive came from 46 research studies, hundreds of designs and 18,000+ participants worldwide, including an eye-tracking study comparing 10 apps in Expressive vs standard M3 — [search summary of design.google page](https://design.google/library/expressive-material-design-google-research) (page itself not fetchable; figures come via a search-engine summary, treat as second-hand)
- A new motion-physics system that is "easier to implement and more customizable, powered by tokens"; a shape library of 35 shapes with built-in shape-morph motion — [Google codelab listing via search](https://codelabs.developers.google.com/codelabs/mdc-102-objc) (second-hand summary; verify)
- On Wear OS, Expressive brings: deeper tonal palettes and a wider color-token set; a simpler type scale using variable-font axes (dynamic weight and width as motion feedback; Roboto Flex cited as a 3P equivalent); new type roles (arc text, numerals); flexible container shapes with corner rounding/sharpening that support shape-morphing lists and button states; edge-hugging buttons for round screens; adaptive button groups and shape-morphing loading animations — [Android Developers: Wear M3 Expressive](https://developer.android.com/design/ui/wear/guides/get-started/apply)
- Flutter tracking issue #168813: May 2025 maintainers said they were not developing Expressive and would not accept contributions; June 10 2025 "strategic pause"; July 29 2025 Material and Cupertino being decoupled into standalone packages with Expressive work to follow there; Aug 17 2026 a contributor pointed to flutter/packages#12093 as the likely effort; issue still open — [flutter/flutter#168813](https://github.com/flutter/flutter/issues/168813)
- A commenter on that issue (June 27 2026) claimed Material's site says Flutter is in "maintenance mode" for Material; another (June 30 2026) disputed that, saying Flutter remains committed and Expressive will arrive after decoupling. Conflicting, unofficial comments — [flutter/flutter#168813](https://github.com/flutter/flutter/issues/168813)
- Community packages exist: `material_3_expressive` (v1.0.8 requires Flutter 3.44+ and a `material_ui` package instead of `package:flutter/material.dart`), `m3_expressive`, `material_expressive_ui` (unofficial port from Compose), `m3e_core` — [pub.dev search results](https://pub.dev/packages/material_3_expressive), [m3_expressive](https://pub.dev/packages/m3_expressive), [material_expressive_ui](https://pub.dev/packages/material_expressive_ui)

### Inferences
- Treat Expressive as a design language to implement via your own tokens (springs, shape morph, variable fonts like Roboto Flex) rather than waiting for SDK widgets; isolate it behind a thin design-system layer so a later switch to official `material_ui` Expressive is cheap.
- Gym UX fits Expressive: big numerals (variable-font weight/width), morphing start/stop buttons, springy set-complete feedback.

### Gaps
- Official M3 Expressive spec (m3.material.io) unreachable: exact spring stiffness/damping tokens, new component list (e.g. button groups, FAB menu, loading indicator, split button, toolbars), color/type scale details unverified here.
- Which shipped apps use Expressive well: no source retrieved.
- Whether Flutter's `material_ui` package has shipped Expressive components as of Nov 2026: not confirmed.

## Android 16/17 platform features for workouts

### Takeaway
Live Updates (promoted ongoing notifications with ProgressStyle/MetricStyle) are the right surface for an active workout and rest timer, with strict eligibility rules (no RemoteViews, ongoing, user-initiated). Edge-to-edge is enforced from Android 15; large-screen adaptivity and Health Connect session writing have clear official guidance.

### Cited Findings
- Android 16 introduced `Notification.ProgressStyle` with Points and Segments and a tracker icon; originally pitched at rideshare/delivery/navigation — [progress-centric notifications](https://developer.android.com/develop/ui/views/notifications/progress-centric)
- Live Update requirements: style must be standard, BigTextStyle, CallStyle, ProgressStyle or MetricStyle; manifest permission `POST_PROMOTED_NOTIFICATIONS` (non-runtime); request promotion via `setRequestPromotedOngoing`/`EXTRA_REQUEST_PROMOTED_ONGOING`; must be ongoing; must have contentTitle; no custom RemoteViews; not a group summary; not colorized; channel not IMPORTANCE_MIN — [Live Updates](https://developer.android.com/develop/ui/views/notifications/live-update)
- Promoted notifications appear at the top of the shade, on the lock screen, and as a status-bar chip; cards are expanded and uncollapsible; users can demote them. OEMs can add criteria — [Live Updates](https://developer.android.com/develop/ui/views/notifications/live-update)
- Docs list "starting a workout" as a user-initiated example; inappropriate uses include ads, alerts, chat messages and "quick access to app features" (use widgets or Quick Settings tiles for that) — [Live Updates](https://developer.android.com/develop/ui/views/notifications/live-update)
- Status chip: max width 96dp; `setShortCriticalText` or `setWhen` provide the text; a Chronometer countdown can show in the chip (relevant to rest timers); text under 7 chars shows whole, otherwise icon-only if less than half fits — [Live Updates](https://developer.android.com/develop/ui/views/notifications/live-update)
- Use `setDeleteIntent` and do not repost dismissed Live Updates; abuse risks users revoking permission. APIs to check state: `canPostPromotedNotifications()`, `hasPromotableCharacteristics()`, `Settings.ACTION_MANAGE_APP_PROMOTED_NOTIFICATIONS`. Live Updates bridge to some Wear OS devices — [Live Updates](https://developer.android.com/develop/ui/views/notifications/live-update)
- Edge-to-edge is enforced on Android 15 (transparent status bar by default); keep gesture nav bar transparent; use WindowInsets; avoid touch targets under gesture insets; button-nav scrim removable via `setNavigationBarContrastEnforced(false)` — [System bars](https://developer.android.com/design/ui/mobile/guides/foundations/system-bars)
- Large-screen tiers: Tier 3 adaptive ready (portrait+landscape, multi-window), Tier 2 optimized (responsive layouts, keyboard/mouse/stylus), Tier 1 differentiated (e.g. tabletop posture); canonical layouts list-detail/feed/supporting pane — [Large screens](https://developer.android.com/guide/topics/large-screens/get-started-with-large-screens)
- Health Connect workout guidance: `ExerciseSessionRecord` is the central record; associated HeartRate, Speed, Distance, TotalCalories, Elevation, StepsCadence, Power records; routes written with the session; use a foreground service (`foregroundServiceType` health or location) for screen-off collection; WorkManager for deferred sync; batch writes (up to 1000 records per request), write at most every 15 min during tracking; set `metadata.clientRecordId` to dedupe; avoid overlapping sessions; check permissions before every read/write; Health Connect Toolbox and FakeHealthConnectClient for testing — [HC workouts](https://developer.android.com/health-and-fitness/health-connect/experiences/workouts)
- Data types relevant to gym/cardio: ExerciseSession (types include STRENGTH_TRAINING, WEIGHTLIFTING, BIKING_STATIONARY, ROWING_MACHINE, RUNNING_TREADMILL, ELLIPTICAL, STAIR_CLIMBING_MACHINE, HIIT), HeartRate (series), Power, CyclingPedalingCadence, Speed, Distance, ActiveCalories, TotalCalories, Vo2Max, Weight, BodyFat, LeanBodyMass, PlannedExercise (feature-flagged), ActivityIntensity (feature-flagged). Extra permissions: `READ_HEALTH_DATA_IN_BACKGROUND`, `READ_HEALTH_DATA_HISTORY` (older than 30 days). Play Console health-apps declaration required — [HC data types](https://developer.android.com/health-and-fitness/health-connect/data-types)
- Note: no HC record type for per-set weight x reps; strength detail (sets/reps/load) must live in the app's own store, with the session/HR/calories mirrored to Health Connect — inference from the type list above, not a stated doc claim.

### Inferences
- Rest timer = promoted ongoing notification with Chronometer countdown (chip shows remaining time) plus action buttons ("+15s", "Skip"); active-workout Live Update with MetricStyle/ProgressStyle (set progress segments per exercise). Avoid RemoteViews. Fall back to a standard ongoing foreground-service notification when promotion is denied.
- Quick-start belongs in a widget or QS tile, not a Live Update (per docs).

### Gaps
- MetricStyle details, Android 17 specifics, and which API level each Live Updates piece needs: not confirmed (fetched page did not state minimum API level).
- Glance widgets, Quick Settings tile API, predictive back specifics, haptics APIs (fetch 404), Android 16 large-screen orientation-restriction removal (page did not mention it), foreground-service type rules for Android 14-17: no verified source retrieved.
- Wear OS Ongoing Activity / Tiles / Health Services: fetch 404; only the Live-Updates-bridge-to-Wear fact above is verified.

## Flutter in 2026: engine, plugins, performance

### Takeaway
Plugins for the two critical integrations exist and are current: `health` v14 (Health Connect) and `flutter_blue_plus` (BLE; note commercial license). Widgets, Live Updates and QS tiles need native Kotlin via platform channels (no verified Flutter-native path found).

### Cited Findings
- `health` 14.0.0 (CARP, DTU; verified publisher carp.dk; 682 likes): wraps HealthKit and Health Connect; requires Dart 3.12+/Flutter 3.44+, Android minSdk 26, compileSdk 37, AGP 9.1+, Gradle 9.3.1+ for Flutter 3.47; supports permissions, reads, aggregates, writing workouts incl. GPS routes, incremental change tracking on Android, per-app Health Connect quota errors (`rateLimitExceeded`); Health Connect on Android 13 and lower needs the separate app; some types depend on OS/Health Connect version — [pub.dev/health](https://pub.dev/packages/health)
- `flutter_blue_plus` 2.3.15: minSdk 21; Android 12+ needs BLUETOOTH_SCAN/CONNECT (`neverForLocation` if no location use); BLE central role only, no Bluetooth Classic; Android throttles startScan to 5 per 30 s; must rediscover services after each reconnect; background BLE is advanced and may need a fork; license is free for personal/nonprofit/education but requires a paid Commercial License for for-profit use — [pub.dev/flutter_blue_plus](https://pub.dev/packages/flutter_blue_plus)
- The Flutter version in the ecosystem is at least 3.44, with 3.47 referenced by `health` — [pub.dev/health](https://pub.dev/packages/health)

### Inferences
- Budget for the flutter_blue_plus commercial license, or evaluate alternatives, before shipping a for-profit app with BLE machine/HR-strap support (alternatives not researched).
- Keep the Health Connect and BLE layers behind repository interfaces for testability.

### Gaps
- Impeller status on Android, fragment shaders, Rive/Lottie recommendations, app-size figures, mid-range device performance benchmarks, latest stable Flutter release notes: docs.flutter.dev unreachable, no other source retrieved.
- Flutter plugins/approaches for home-screen widgets (e.g. home_widget), Live Updates, QS tiles: not researched.

## Accessibility

### Takeaway
Android's official guidance centres on labelled elements, merged semantics for grouped content, custom actions for gesture-only interactions, non-color cues, and meaningful action labels. The EAA has applied since 28 June 2025 with EN 301 549 (WCAG 2.1 AA based) as the benchmark; a v4.1.1 move to WCAG 2.2 is reported but unverified.

### Cited Findings
- Android guidance: label every interactive element; unique labels within collections (`collectionInfo`); group related elements into a single announcement and make only the parent interactive; mark headings; set pane titles (unique across the app); mark decorative elements as hidden; expose swipe/drag gestures as custom accessibility actions for TalkBack, Voice Access and Switch Access; give long-press an action label; custom components must supply role and state description; use shapes/text/haptics besides color; captions/transcripts for media — [Android accessibility principles](https://developer.android.com/guide/topics/ui/accessibility/principles) (Compose-based examples; Flutter equivalents are Semantics, MergeSemantics, ExcludeSemantics, CustomSemanticsAction — from my knowledge of Flutter API, not verified here)
- Live Updates add an end-of-progress white dot as an accessibility visualization — [Live Updates FAQ](https://developer.android.com/develop/ui/views/notifications/live-update)
- EAA: compliance date commonly stated as 28 June 2025; EN 301 549 v3.2.1 incorporates WCAG 2.1 AA and covers mobile apps; microenterprise exemption (under 10 staff and turnover/balance sheet no more than EUR 2M) covers services not products; sources are vendor blogs and disagree on whether EN 301 549 v4.1.1 (WCAG 2.2, reportedly published 2 Sep 2026) is yet operative — [Level Access](https://www.levelaccess.com/blog/eu-accessibility-requirements-and-eaa-compliance/), [CCPC Ireland](https://www.ccpc.ie/business/enforcement/accessibility/european-accessibility-act-guidelines-for-microenterprises/), [CookieYes](https://www.cookieyes.com/blog/european-accessibility-act/)

### Inferences
- Designing to WCAG 2.2 AA is the safe target given the possible EN 301 549 update. Gym-specific risks: swipe-to-delete sets and drag-to-reorder need custom actions; color-only effort/zone coding (HR zones) needs labels/patterns; timers need non-visual announcements (live regions).

### Gaps
- Numeric thresholds (48dp targets, 4.5:1 / 3:1 contrast, 200% font scaling) were not confirmed in a fetched source; the principles page did not state them. Remove-animations / reduced-motion setting and Flutter `MediaQuery.disableAnimations`: not sourced.
- Whether the EAA actually covers a fitness app (service-category scope: e-commerce/subscription sales likely in; pure tracking uncertain) needs legal confirmation; primary Directive text not read.

## Play "Best of" and Material Design Awards traits

### Takeaway
Little verified. The 2025 Best of list has no dedicated health & fitness category; health-adjacent winners were scattered.

### Cited Findings
- Google Play Best of 2025: overall best app Focus Friend (Hank Green); Calm won Best for XR Headsets; SleepisolBio won Best for Watches; Wiser won Best Everyday Essential; Runna appears in a third-party roundup but its award category was not confirmed — [search results summarising Google's post](https://blog.google/products/google-play/best-apps-games-2025/), [YugaTech roundup](https://www.yugatech.com/news/here-are-the-list-of-google-plays-best-apps-of-2025/), [TechRadar](https://www.techradar.com/phones/these-are-the-10-best-android-apps-of-the-year-according-to-google)
- Watch/XR winners suggest Google rewards multi-form-factor support (Wear OS, XR) — inference from the two category names above.

### Gaps
- Shared design/quality traits of winners, Material Design Awards 2024-2026, 2024 and 2026 lists, health/fitness winners (e.g. any fitness app): primary pages unreachable; not established.

## Android market facts for fitness

### Gaps
- Android vs iOS share in India, Europe, US; device tiers; offline expectations: StatCounter unreachable and no alternative source retrieved. Nothing is claimed here.
- Weak signal from fetched docs only: Health Connect needs Android 9+ (health plugin minSdk 26) — [pub.dev/health](https://pub.dev/packages/health).

## Suggested follow-ups (needs allowed hosts)
Allow m3.material.io, docs.flutter.dev, blog.google/android-developers.googleblog.com, play.google.com, gs.statcounter.com, then research: Expressive spec tokens, Impeller/Rive/Lottie, Glance/QS tile/predictive back/haptics, Wear OS Ongoing Activity, Play awards traits, market share.
