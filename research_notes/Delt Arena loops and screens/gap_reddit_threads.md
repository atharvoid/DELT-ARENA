# Reddit gap research: Hevy, strongapp, fitbod, weightroom

## Method and limits

Browsed logged out through the user's Chrome via Tether on www.reddit.com (not old.reddit.com, which now forces a login wall). Reddit's JSON and fetch endpoints returned 403, so every read came from the rendered page. Search used Reddit's in-subreddit search with sort=top and t=year, with some OR-joined queries. Reddit's index for these subreddits is thin, so many topics returned zero relevant threads. Dates below are approximate: they convert Reddit's relative ages ("5mo ago") as of 2026-11-26 and are not exact. Vote and comment counts come from search snippets unless marked as read in full. No login, vote, comment or post was made. The one tab opened was closed.

## Topic 1: How fast logging a set feels and how many taps it takes

No thread found that directly complains about or praises tap count for set logging in these four subreddits.

- https://www.reddit.com/r/strongapp/comments/1s1qtb3/previous_set_column/ (approx. Mar 2026, 4 votes, 0 comments, snippet only). Title suggests a request for a previous-set column during logging. Body not read.

## Topic 2: Rest timer problems (notifications, Android background, Wear OS)

- https://www.reddit.com/r/Hevy/comments/1qvex1v/timer_noise_is_grindr_notification/ (approx. Jan 2026, 121 votes, 43 comments, read in full). The poster says Hevy's rest-timer sound is almost identical to a dating app's notification sound, which causes confusion mid-workout. Replies describe false alerts that look like new messages, and a few users say the sound is loud in gyms. One reply says the timer can be changed in settings. Another asks for the timer to use a custom sound, because the sound masks the music the user is listening to.
- https://www.reddit.com/r/strongapp/comments/1rof29r/rest_timer_suddenly_not_visible/ (approx. Feb 2026, 3 votes, 2 comments, read in full). The timer keeps counting but stops being visible until the user leaves and re-enters the screen. A second user says this happens when they leave the exercise list while the timer runs, and it clears on its own or after re-entering the exercise. Support asked the poster to email with details.
- https://www.reddit.com/r/strongapp/comments/1ww6h8q/rest_timer_auto_expand_glitch_on_apple_watch/ (approx. Sep 2026, 3 votes, 3 comments, read in full). After an iPhone upgrade, the rest timer on the Apple Watch expands after every set and covers the next set's weight and reps until dismissed. Reinstalling did not help. Switching the timer to inline mode removes the timer entirely. A commenter reports a similar Android problem lasting almost a year, and another says Strong does not launch on Watch with iOS 27.
- Hevy Trainer launch thread (see Topic 9) lists "Rest timer customization" among planned improvements, per Hevy's own post.

Android background and Wear OS: no thread found that is specific to Wear OS. The only Android-specific rest-timer report is the single comment above.

## Topic 3: Auto-progression and AI-generated workouts (trusted or distrusted, Fitbod especially)

- https://www.reddit.com/r/fitbod/comments/1swb753/considering_leaving_this_app/ (approx. Apr 2026, read in full). The poster says weight targets are far above their logged personal bests, such as 22 x 20 kg after a 15 x 20 kg best, and the app keeps suggesting max-effort shoulder work with too many reps. Several replies describe editing weights and reps on most exercises, one says they stopped renewing, and one switched to Hevy after three years of paying. Fitbod's staff replied asking the poster to email support with account logs.
- https://www.reddit.com/r/fitbod/comments/1uct7qr/how_fitbods_algorithm_actually_works/ (approx. Jun 2026, official Fitbod post by the company account, read in full). Fitbod addresses "the app feels random", weight suggestions, repeating exercises and muscle freshness. It says the app builds weight suggestions from logged loads, Reps in Reserve (RiR) and performance trends, and that the first 4 to 6 weeks are a learning period. It describes an Exercise Variability setting with More Consistent, Balanced and More Variable options, where More Consistent is said to keep roughly 70 to 80 percent of exercises week to week. It also says the app cycles through strength, hypertrophy and endurance phases. The post gives two vendor-reported figures: new users who logged RiR on most early workouts had about 16 percent lower error by workouts 6 to 8, and average gap between suggested and logged weight fell from about 26.6 percent to 9.9 percent. These figures are unverified.
- https://www.reddit.com/r/fitbod/comments/1t6lvp0/so_long_fitbod/ (approx. Apr 2026, read in full). A long-time user describes sharp decline over months with buggy and illogical workouts and missing logs, and moves to Gravl. Replies say the staff seem to answer complaints with canned temporary fixes.
- https://www.reddit.com/r/fitbod/comments/1tp5lyg/thoughts_on_the_new_coach_beta_does_it_work_for/ (approx. May 2026, read in part). The poster dislikes an AI coach forced into the workout screen. Their Coach BETA only shows text saying it is "tailoring insight" on every exercise. Fitbod's staff replied that Coach is beta-only and that updating fixes it. Other replies say they never got any insight from it.
- Also seen in search snippets only, not read: https://www.reddit.com/r/fitbod/comments/1s0ldpk/chatgpt_tool_that_turns_your_fitbod_export_into/ (a third-party tool that builds plans from a Fitbod export) and https://www.reddit.com/r/fitbod/comments/1plkodh/developer_request_stretch_injuries/ (request for stretching and injury handling).

Vote and comment counts for the Fitbod threads were not captured.

## Topic 4: Voice logging requests

No thread found in the four subreddits about voice logging.

## Topic 5: One-handed use mid-set

No thread found in the four subreddits about one-handed use.

## Topic 6: Warm-up and plate calculators

No thread found in the four subreddits about warm-up or plate calculators. Hevy Trainer's roadmap lists "warm-up / cool-down / cardio management" as planned (see Topic 9), which is the only related signal.

## Topic 7: Cardio machine logging and Bluetooth / heart rate

- https://www.reddit.com/r/Hevy/comments/1y09s39/new_in_hevy_heart_rate_over_bluetooth/ (approx. 6 days before 2026-11-26, about 20 Nov 2026, 259 votes, 66 comments, read in part). Hevy announced it can now connect a Bluetooth heart-rate strap or sensor and show live BPM during a workout, saved with the session. Setup is under Settings, Integrations, Wearable Sensor, or inside Workout Settings, and some devices need pairing again for each workout. Early replies report that a Fitbit device showed as connected and a green sensor dot appeared, but no heart-rate data was saved after the workout. Another user asks whether a Garmin watch can broadcast without a chest strap; the reply says it depends on the watch, and the user says the watch must be started manually to broadcast.
- https://www.reddit.com/r/Hevy/comments/1wo8fwn/as_a_apple_watch_series_3_user_im_sad/ (approx. Sep 2026, 143 votes, 28 comments, read in full). Hevy stopped updating its Apple Watch app for Series 3, because the current Apple tooling no longer supports watchOS 8. The official reply says lifetime memberships and data are safe and users can still log from the phone. Users say heart rate will no longer show in Hevy on that watch. One user says heart rate still arrives in Hevy when they run an Apple Fitness workout on the watch and sync Apple Health, though this is a single unverified report.
- https://www.reddit.com/r/strongapp/comments/1vnfmwu/feature_request_garmin_integration/ (approx. Aug 2026, 15 votes, 0 comments, snippet only). Requests Garmin integration.

## Topic 8: Weekly stats and per-muscle volume

- Fitbod's official post (Topic 3) says its exercise selection follows a muscle-freshness model, so a single muscle group can dominate if most others show as recently trained. Users are directed to the app's muscle recovery view.
- Hevy Trainer launch thread (Topic 9) lists "Deprioritizing or excluding muscle groups" as a planned improvement, and a commenter asks for a way to change programmed days and move exercises.

No thread found that explicitly asks for weekly stats or per-muscle volume dashboards.

## Topic 9: Trust issues with AI coaches changing weights

- https://www.reddit.com/r/Hevy/comments/1s3f9iv/hevy_trainer_is_now_live_and_available_with_hevy/ (approx. Mar 2026, 211 votes, 82 comments, read in part). Hevy Trainer gives guided workouts inside Hevy Pro. Hevy's post lists planned work on warm-up and cardio management, injury handling, muscle-group exclusion and rest-timer customization. Top replies ask to keep their own programs and have the app only suggest weights for the next session. A staff reply says this would likely be a separate feature. One user says they are glad it does not use AI and wants progression to use past workout data. Another asks whether the weight suggestions feel wrong. A user who has used Trainer for about six weeks reports good results and says it switched some lifts, while another asks whether it changes routines after a plateau.
- Fitbod threads in Topic 3 carry the same distrust pattern about weight targets.

## Topic 10: App-switching reasons

- https://www.reddit.com/r/strongapp/comments/1t75hi8/annoyed_with_apple_watch_integration/ (approx. Apr 2026, 11 votes, 9 comments, read in full). A three-year Strong user reports live sync failing, workouts missing from the watch, and sets becoming unchecked during live sync. Fixes offered include restarting both devices and logging out, and one user says version 6 has been stable. Two users say they switched to Liftin, and one notes that a workout still went missing after switching. The poster asks how custom exercises transfer between apps.
- https://www.reddit.com/r/fitbod/comments/1swb753/considering_leaving_this_app/ (Topic 3) has a reply saying the user moved to Hevy because it works for new and experienced lifters.
- https://www.reddit.com/r/fitbod/comments/1t6lvp0/so_long_fitbod/ (Topic 3) moves to Gravl.
- https://www.reddit.com/r/Hevy/comments/1wo8fwn/as_a_apple_watch_series_3_user_im_sad/ (Topic 7) shows a user leaving the watch app behind after support ends for their device.

## Other Hevy threads seen in search results (not read in full)

- https://www.reddit.com/r/Hevy/comments/1xg5xc1/hevy_community_update_2_better_notes_trainer/ (approx. Oct 2026, 807 votes, 331 comments). Title mentions better notes, Trainer updates and Hevy in ChatGPT. Body not read.
- https://www.reddit.com/r/Hevy/comments/1umaz02/hevy_community_update_1_trainer_native_redesign/ (approx. Jun 2026, 1K votes, 408 comments). Title mentions Trainer, native redesign and a faster app. Body not read.
- https://www.reddit.com/r/Hevy/comments/1w1qekz/we_should_have_an_option_to_reset_prs_changing/ (approx. Aug 2026, 211 votes, 38 comments). Request to reset PRs when changing gyms or machines. Body not read.
- https://www.reddit.com/r/Hevy/comments/1u57fu4/please_add_permanent_exercise_notes/ (approx. Jun 2026, 355 votes, 52 comments). Request for permanent exercise notes. Body not read.
- https://www.reddit.com/r/Hevy/comments/1uwayd5/why_would_you_do_this_to_me/ (approx. Jul 2026, 288 votes, 45 comments). Title only, body not read.
- https://www.reddit.com/r/Hevy/comments/1vvuigm/woah_new_ui/ (approx. Aug 2026, 205 votes, 49 comments). Reaction to a UI change. Body not read.

## What this means for Delt Arena

Live set screen with predictive tap mode. Users in these threads care about the screen that appears between sets. Strong users report timers covering the next set's targets, and Fitbod users report targets that feel wrong. The set screen should show the next set's target clearly and keep the timer from obscuring it. Predictive tap mode should prefill from the last session and make an override a single tap, which matches Fitbod's advice to log actual weights. Keep the prefill visible so users can see why a number appeared.

Optional voice mode. No thread in these four subreddits asked for voice logging. Treat voice as unvalidated by this research and keep it optional.

Rest timer. Threads show four needs: a sound that does not confuse with message alerts and can be changed, a timer that keeps running and stays visible when the user navigates or uses a watch, an inline option that still shows a timer rather than hiding it, and no full-screen overlay on watch. Background and Wear OS behavior were not verified because no thread covered them.

Coach screen. Trust problems in these threads come from prescriptions that appear arbitrary, plus vague AI text with no content. Delt Arena's coach should explain each suggested weight in a line, such as which logged sets it used and how recent they are. Users should be able to choose how much variation to allow, and keep their own program while receiving only weight suggestions, which Hevy Trainer users asked for. Logging RiR should be easy and optional to tune suggestions, since Fitbod says it improves early accuracy.

Cardio and heart rate. Bluetooth heart-rate pairing is now a visible Hevy feature, and early reports show the link can appear connected but save nothing. Delt Arena's cardio logging should show a clear saved-or-not state after each session.

## Still not reached

- Logging speed and tap counts: no thread found.
- Voice logging: no thread found.
- One-handed mid-set use: no thread found.
- Warm-up and plate calculators: no thread found.
- Wear OS and Android background rest timer: no Wear OS thread; one Android comment only.
- Weekly stats and per-muscle volume: no thread asking for these.
- r/weightroom: searches for "app", "tracking", and workout app or timer terms returned only program reviews and competition posts. No app-related thread found.
- Most Hevy threads listed above were seen only in search snippets and are not read in full.
- Fitbod vote and comment counts were not captured.
- Exact posting dates are approximate, converted from relative ages.
- Reddit's search index is thin for these subreddits, so absence of a thread here is not proof that no one raised the topic.
