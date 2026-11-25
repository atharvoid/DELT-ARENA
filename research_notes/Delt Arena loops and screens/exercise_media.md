# Exercise Demonstration Media: Sources, Licensing, and Flutter Delivery

Research date: 2026-11-25. Tool budget was exceeded (about 22 calls) and several key hosts were unreachable from this session (see Gaps). Everything marked "search snippet" was not verified on the page itself.

## Which exercise media libraries/APIs exist, and can they be licensed commercially?

### Takeaway
The only open-licence library I could verify on the page is free-exercise-db (Unlicense, about 800+ exercises, JPG image pairs), which is public-domain-equivalent but has no motion media. Hosted GIF APIs (ExerciseDB/AscendAPI, WorkoutX, MuscleWiki) could not be verified on their own terms pages from this session, so commercial terms for their media remain unconfirmed.

### Cited Findings
- free-exercise-db (yuhonas) is licensed under the Unlicense, describes itself as an "Open Public Domain Exercise Dataset", lists "over 800 exercises" and stores JPG images in per-exercise folders with numbered files (for example `Air_Bike/0.jpg`); the README reports 25 duplicate image files; the last-commit date was not visible — [GitHub: yuhonas/free-exercise-db](https://github.com/yuhonas/free-exercise-db). The page shows only the licence name, not the licence text, and does not state a separate licence for the images.
- A GitHub issue on the same repo asks whether the images can be used in a commercial app; I could not read the answer — [GitHub issue #12](https://github.com/yuhonas/free-exercise-db/issues/12) (search snippet only, not fetched).
- wger (open-source workout tracker) README licence section lists: application code AGPL-3.0-or-later; exercise/ingredient data "Creative Commons (see individual entries)"; documentation CC-BY-SA-4.0. No separate image licence is stated and no mention of Wikipedia-sourced images appears on the README itself — [GitHub: wger-project/wger README](https://github.com/wger-project/wger/blob/master/README.md).
- wger repositories say some exercise images were taken from Wikipedia and that per-folder SOURCES files give details (search snippet) — [search result, wger repos](https://github.com/wger-project/wger/blob/master/extras/docker/development/README.md) (not fetched in full).
- A third-party wger scraper lists per-record licence "CC-BY-SA 4.0" with author "wger.de contributors" (secondary source, not verified against wger's API) — [Apify wger scraper](https://apify.com/parseforge/wger-exercise-database-scraper.md) (search snippet only).
- ExerciseDB (now branded AscendAPI) advertises a free tier of 1,500 exercises with GIFs (search snippet). No licence or commercial-use statement for the GIFs was found — [Dev.to write-up](https://dev.to/furkanuruk/i-built-a-free-exercisedb-alternative-1300-exercises-with-gif-animations-5868), [Exercise Database API listing](https://zylalabs.com/id/392) (search snippets only). The exercisedb.dev site and the JakobDrist/exercisedb-api GitHub repo were unreachable (HTTP 451 on GitHub; DNS failure on exercisedb.dev).
- MuscleWiki API search snippet: pricing page lists a free tier (500 Playground calls/month, all exercises and videos, but no routines, bodymap images or secondary/tertiary muscles) and paid tiers from $10 to $199.99/month for 1,000 to 300,000 calls; "every paid plan includes commercial use rights"; annual plans get 25% off — [MuscleWiki API pricing](https://api.musclewiki.com/pricing) (search snippet; api.musclewiki.com failed DNS resolution on fetch). A third-party wrapper (Parse) claims MuscleWiki has no documented public API, so this is contested.
- API Ninjas: two ToS versions disagree. One (dated 2026-09-13 per search snippet) limits free-plan use to personal/non-commercial and allows commercial use only while a paid plan is active. An older one (2026-04-27 per snippet) appears to restrict commercial use of Services/Output in any commercial product, and says users own their Output. Exercises-specific terms were not found — [API Ninjas terms](https://api-ninjas.com/terms), [API Ninjas ToS](https://api-ninjas.com/tos) (search snippets; api-ninjas.com failed DNS resolution on fetch).
- Hevy (search snippet from Google Play and feature pages): 400+ exercises; Google Play lists "+200 exercise videos"; the claim is marketing copy and the split between videos and images was not confirmed — [Hevy feature page](https://www.hevyapp.com/features/exercise-library/), [Hevy Google Play listing](https://play.google.com/store/apps/details?id=com.hevy). The help-center article was unreachable.
- Fitbod (search snippet): video demonstrations from "expert" presenters, described as hi-res, multi-angle, filmed footage, plus written walkthroughs; library size cited as 1,500+ (help article) or 1,000+ (App Store); older 2021 listing mentions about 400 HD videos — [Fitbod help: Exercise Details](https://help.fitbod.me/hc/en-us/articles/30721437384215-How-to-Navigate-the-Exercise-Details-Screen), [Fitbod App Store](https://apps.apple.com/gb/app/id1041517543) (search snippets).
- Mixamo (Adobe, rigged characters and animations, FBX): community forum posts say commercial use including games is allowed, but redistribution, reselling, bulk download and asset-store packaging are not. One post cites a CC BY-NC claim that conflicts with the rest and is likely wrong. The official Mixamo FAQ and Additional Terms (2021 PDF per forum) were not fetched — [Adobe community FAQ thread](https://community.adobe.com/t5/mixamo-discussions/mixamo-faq-licensing-royalties-ownership-eula-and-tos/td-p/13234775) (search snippet).

### Inferences
- For a commercial app, free-exercise-db is the only verified-clean licence for images, but its material is static JPG pairs, not motion. Pairing it with a filmed or vector animation source is the realistic path.
- wger's mixed licensing means each exercise record needs a per-record licence check before shipping; a blanket "CC-BY-SA" claim is not safe.
- The hosted GIF APIs are likely commercially usable only on paid plans (MuscleWiki says so explicitly; API Ninjas' terms conflict), so a licence contract or written permission should be obtained before launch.

### Gaps
- ExerciseDB/AscendAPI media licence: no verified terms (site unreachable).
- MuscleWiki: pricing is a search snippet, not checked against the page; media licence terms not verified.
- API Ninjas: which ToS version is current was not resolved.
- WorkoutX, Gymvisual, exercise.com, and 3D animation vendors were not researched.
- Whether the free-exercise-db images are shipped on the same Unlicense basis as the JSON was not confirmed.

## Which apps do major apps use, and how do they present it?

### Takeaway
Hevy and Fitbod both show exercise demos from their own libraries (Hevy: 400+ exercises with video on some; Fitbod: filmed multi-angle videos plus written steps). Neither was verified to use animated GIFs or 3D animation from this session. JEFIT and Strong were not researched.

### Cited Findings
- Hevy opens an exercise's details on tap, and its library includes custom exercises (free tier up to 7, Pro unlimited) — [Hevy help](https://help.hevyapp.com/hc/en-us/articles/35688251991575-Hevy-Exercise-Library-400-Exercises-and-Custom-Exercises) (unreachable; search snippet only).
- Fitbod shows a video demo at the top of each exercise's details page, reached through "How To" — [Fitbod help](https://help.fitbod.me/hc/en-us/articles/30721437384215-How-to-Navigate-the-Exercise-Details-Screen) (search snippet).

### Inferences
- Both competitors pair video with written instructions, which supports a text-cue fallback in the app.

### Gaps
- JEFIT and Strong presentation, not checked.
- Whether Hevy or Fitbod use GIFs or 3D models: not verified.

## Building your own (3D rigged, mocap, Rive/Lottie): feasibility

### Takeaway
Rive and Lottie are both mature, MIT-licensed Flutter runtimes, so vector animation is feasible in-house. Cost and mocap pipelines were not researched.

### Cited Findings
- rive 0.14.11 on pub.dev, publisher rive.app (verified), supports Android, iOS, Linux, macOS, Web, Windows; licence MIT — [pub.dev/packages/rive](https://pub.dev/packages/rive). Loaded with `File.asset()`; state machine docs are linked but not summarised on the page.
- lottie 3.8.2 on pub.dev, MIT; supports .json, .zip with images, .tgs, and dotLottie via `decodeZip`; `renderCache` added in 3.0 to reduce energy use at the cost of memory; plays at the After Effects frame rate by default — [pub.dev/packages/lottie](https://pub.dev/packages/lottie).
- Callstack benchmark (search snippet): Lottie JSON 46.2 KB vs GIF 164.5 KB for one animation — [Callstack: Lottie vs Rive](https://callstack.com/blog/lottie-vs-rive-optimizing-mobile-app-animation) (not fetched; figure from search snippet). LottieFiles claims "up to 6x smaller" than GIF — [LottieFiles vs GIF](https://lottiefiles.com/blog/working-with-lottie-animations/lottie-vs-gif) (vendor claim).
- Mixamo commercial use is generally allowed (see above) — this is the cheapest rigged-character source, but it only gives generic mocap, not an exercise-specific library.

### Inferences
- A small in-house team could make vector Lottie/Rive exercise animations for a limited set of movements, but a full library of 500+ exercises at quality would need a studio or large effort. No cost estimate was found.

### Gaps
- Typical cost of a custom exercise animation (per movement) and studio pricing: not researched.
- Motion capture pipeline and hardware costs: not researched.

## Delivery format for Flutter: sizes, packages, caching, offline

### Takeaway
For vector-style movement diagrams, Lottie or Rive is smallest and scales well; for filmed or raster content, MP4/HEVC via video_player is the practical choice. Animated WebP is smaller than GIF but has iOS compatibility concerns for older devices. Precise file-size comparisons for the same clip in each format were not measured.

### Cited Findings
- video_player 2.14.1 (BSD-3-Clause): Android uses ExoPlayer with SDK 24+; Android needs INTERNET permission for network video; iOS needs NSAppTransportSecurity for http — [pub.dev/packages/video_player](https://pub.dev/packages/video_player). Caching not covered by the package page.
- cached_network_image 4.0.7 (MIT): disk caching via flutter_cache_manager; no mention of animated WebP or GIF support; no web caching — [pub.dev/packages/cached_network_image](https://pub.dev/packages/cached_network_image).
- flutter_cache_manager 3.5.0 (MIT): files go to the app's temporary directory by default, so the OS may delete them at any time; `getFileFromCache` returns only already-cached files; example settings are stalePeriod 7 days and maxNrOfCacheObjects 20, but the page does not state them as defaults — [pub.dev/packages/flutter_cache_manager](https://pub.dev/packages/flutter_cache_manager).
- Animated WebP: one developer post says 50–80% smaller than GIF (unverified claim); Safari did not support it until 2020 (per one article) — [Cloudinary GIF vs WebP](https://cloudinary.com/guides/image-formats/gif-vs-webp), [Dev.to: GIF vs WebP vs APNG](https://dev.to/michael_lip_52d5151c3e364/gif-vs-webp-vs-apng-the-animated-image-format-war-nobody-won-4fj) (search snippets).

### Inferences
- For offline use, the cache directory is not durable; a bundled-asset or app-documents copy is needed for guaranteed offline playback.
- Bundling a full library in the APK would add size; a download-on-demand plus cache approach is likely needed. No size budget was measured.

### Gaps
- Size of a representative 5-second clip in MP4/HEVC, WebP, Lottie, and GIF: not measured.
- Whether cached_network_image handles animated WebP/GIF playback: not verified.
- Android-specific APK/app-bundle size impact: not researched.

## Accessibility

### Takeaway
Not researched in this pass.

### Gaps
- Reduced-motion handling in Flutter (MediaQuery disableAnimations), captioning, and text cues: not searched.

## Muscle-map assets (front/back body diagrams with selectable muscles)

### Takeaway
Not researched in this pass.

### Gaps
- Open-source or licensable muscle-map SVG sets (e.g. react-body-highlighter and similar): not searched or verified.

## Recommendation

Use free-exercise-db as the seed library only after confirming image licences per exercise; build or license motion media (Lottie/Rive for diagrams, MP4 for filmed clips); obtain written commercial terms from ExerciseDB/AscendAPI and MuscleWiki before launch, since their terms could not be verified here.

## Sources that failed to load
- api.musclewiki.com (DNS failure on fetch)
- api-ninjas.com (DNS failure on fetch)
- exercisedb.dev (DNS failure on fetch)
- help.hevyapp.com (DNS failure on fetch)
- github.com/JakobDrist/exercisedb-api (HTTP 451)

Network allowlist needs these hosts added before re-checking the licence terms above.
