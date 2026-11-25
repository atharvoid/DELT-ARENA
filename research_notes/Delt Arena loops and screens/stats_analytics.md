# Training statistics catalogue for a gym + machine-cardio app (Flutter, Android-first)

Research note. Date: 2026-11-25. Tooling limits: several vendor help-centre hosts (help.hevyapp.com, help.macrofactorapp.com, fitbod.me) did not resolve from this session, so vendor details come from search-result summaries, not full-page reads. Items marked [UNVERIFIED] are from my own background knowledge or a secondary source and should be checked.

## 1. Strength stats: which formulas are standard and what are their accuracy limits?

### Takeaway
Epley and Brzycki are the de-facto e1RM formulas. They agree at about 10 reps, diverge at low and high reps, and are only trustworthy for roughly 2-10 rep sets on common lifts. Weekly hard sets per muscle is the best-supported volume metric, and set-counting method (direct vs fractional) changes the answer.

### Cited Findings
- Epley: 1RM = w x (1 + r/30). Brzycki: 1RM = w / (1.0278 - 0.0278 x r), equal to 36/(37 - r) for w in weight, r in reps. Both give identical results at 10 reps; below 10 reps Epley returns a slightly higher estimate. — [Wikipedia 1RM](https://www.Wikipedia.org/wiki/1RM); [topendsports](https://www.topendsports.com/testing/calculators/1repmax.htm)
- Epley and Brzycki originated from a poundage chart / not a formal empirical study. — [Wikipedia 1RM](https://www.Wikipedia.org/wiki/1RM)
- Sweet spot is about 2-10 reps; accuracy falls above about 15 reps due to endurance factors. These claims come from calculator/blog sites, not primary studies. — [topendsports](https://www.topendsports.com/testing/calculators/1repmax.htm); [DEV Community](https://dev.to/ffmicheck/the-two-1rm-formulas-that-give-different-answers-and-which-one-to-trust-8ib)
- A 2026 arXiv preprint (not peer reviewed) argues the equations were derived from small samples on mainly bench press yet are applied to hundreds of exercises; 5RM-based prediction was most accurate in its comparison and accuracy fell at higher reps. — [arXiv 2603.17495](https://arxiv.org/pdf/2603.17495v1.pdf)
- No single formula wins across all scenarios; averaging several formulas is a common suggestion. — [fitnessvolt e1RM comparison](https://fitnessvolt.com/rpe-training/compare/e1rm-formulas/)
- Novices may find their true 1RM is much lower than formula output. — [Wikipedia 1RM](https://www.Wikipedia.org/wiki/1RM)
- RIR-adjusted e1RM (treat reps = reps performed + RIR, then apply Epley/Brzycki): I found no study validating RIR-adjusted 1RM specifically. Related evidence: self-reported RIR is usually within about one rep — [Stronger by Science RIR](https://www.strongerbyscience.com/reps-in-reserve); velocity-based RIR estimates were inaccurate for 69.1% of reps in a bench/prone-row study — [Eur J Sport Sci 2023 (citation page)](https://informahealthcare.com/doi/full/10.1080/17461391.2023.2235314); individualized RIR-velocity models predicted RIR with mean error under 2 reps in a back squat study, general models did not — [Physiol Rep 2024, PMC10901726](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10901726/).
- Weekly sets dose-response: Schoenfeld, Ogborn and Krieger meta-analysis (34 groups, 15 studies) found graded dose-response for hypertrophy; the three-category test (<5, 5-9, 10+ sets) was only a trend (P = 0.074). — [Schoenfeld 2017 via ResearchGate](https://researchgate.net/profile/Brad-Schoenfeld/publication/305455324_Dose-response_relationship_between_weekly_resistance_training_volume_and_increases_in_muscle_mass_A_systematic_review_and_meta-analysis/links/59dc0269458515e9ab4527d6/Dose-response-relationship-between-weekly-resistance-training-volume-and-increases-in-muscle-mass-A-systematic-review-and-meta-analysis.pdf); [PubMed 28755103 (strength, Ralston)](https://pubmed.ncbi.nlm.nih.gov/28755103/)
- Hevy's own guidance is 10-20 weekly sets per muscle (vendor claim, not independent). — [Hevy sets per muscle per week](https://www.hevyapp.com/features/sets-per-muscle-group-per-week/)
- Hevy shows: set count per muscle group (week/month/year), muscle distribution chart (30 days / 3 months / year / all, longer ranges Pro only), volume load = sets x reps x weight, workouts, duration, set counts. — [Hevy features](https://www.hevyapp.com/features/muscle-group-workout-chart/); [Hevy sets per muscle](https://www.hevyapp.com/features/sets-per-muscle-group-per-week/)
- Fitbod: per-muscle recovery 0-100%, "fully recovered" after about 6 days (other pages say up to 7), computed from sets, reps and load, includes cardio. — [Fitbod muscle recovery help](https://help.fitbod.me/hc/en-us/articles/360006269014-Muscle-Recovery)

### Inferences
- Ship e1RM as Epley by default (simple, monotone, extends to 1 rep as identity), cap input reps at about 10-12 for PR/trend purposes, and label every e1RM "estimate". Offer a RIR-adjusted variant only as a toggle, flagged unvalidated.
- Other stats (formulas from standard practice, [UNVERIFIED] as to citation): tonnage = sum(weight x reps) per exercise/session/week; relative intensity = weight / e1RM (or top set / best e1RM); density = tonnage / session minutes; PR types = weight PR, rep-at-weight PR, e1RM PR, volume PR (set and session); frequency = sessions touching a muscle per week; consistency = sessions per week vs target and week-streaks (streak by weeks hit, not days, to avoid punishing rest); progression rate = slope of e1RM (e.g. 8-12 week linear regression, kg/week or %/month); plateau = no new e1RM PR and non-positive slope over N weeks (N=4-6) on a lift with >= M exposures.
- Tonnage is misleading across exercises (leg press vs curl), so compare it only within an exercise; across muscles use hard sets.

### Gaps
- No primary-source validation for RIR-adjusted e1RM found.
- Plateau-detection thresholds have no authoritative source found; treat N weeks as a design choice.
- Hevy/Strong exact e1RM formula not confirmed (help pages unreachable). Fitbod's Estimated Strength method page was unreachable.

## 2. Muscle balance: ratios and fractional sets

### Takeaway
Recent meta-regression evidence favours counting secondary-muscle sets at 0.5 for hypertrophy. Apps disagree on the method (Fitbod docs are internally inconsistent). Ratios (push/pull, quad/hamstring) are computed from the same weekly set counts; left/right needs per-side data only for unilateral movements.

### Cited Findings
- A SportRxiv meta-regression (Remmert and colleagues, preprint, not yet peer reviewed) weighted indirect sets as 1 (total), 0.5 (fractional) or 0 (direct only). Fractional counting fit hypertrophy best (gains levelled off around 11 fractional sets per session); direct counting fit strength best (about 2 direct sets per session). — [SportRxiv 537](https://sportrxiv.org/index.php/server/preprint/view/537); [SportRxiv 460](https://sportrxiv.org/index.php/server/preprint/view/460). Sources disagree on per-session vs weekly framing (BarBend says weekly) — [BarBend](https://barbend.com/news/scientifically-correct-number-sets-per-workout/)
- Boostcamp credits bench press as 1 set chest + 0.5 set triceps. — [Boostcamp muscle tracker](https://www.boostcamp.app/features/muscle-tracker)
- Fitbod's Weekly Set Targets page conflicts with itself (one line says secondary sets count as 0.5, another says secondary muscles do not contribute). — [Fitbod weekly set targets](https://help.fitbod.me/hc/en-us/articles/24739986755223-Weekly-Set-Targets)
- Alpha Progression: could not find documentation on whether indirect sets are counted. — [Alpha Progression blog](https://alphaprogression.com/en/blog/set-progression-maximum-muscle-growth)
- Pelland et al. cited as 2025 / 67 studies in some summaries and as 220 effects / 35 studies in a 2026 preprint; counts conflict, so verify before citing. — [SportRxiv 460](https://sportrxiv.org/index.php/server/preprint/view/460); [Preprints.org 202610.1022](https://www.preprints.org/manuscript/202610.1022)

### Inferences
- Exercise library should store per-exercise muscle weights: primary 1.0, secondary 0.5 (user-editable, default per above); show both "direct" and "fractional" totals with a toggle; default fractional.
- Balance ratios [UNVERIFIED, standard practice]: push:pull = fractional sets (chest, shoulders-front, triceps) : (back, rear delts, biceps); quad:hamstring from weekly sets; anterior:posterior chain likewise; L/R only from unilateral exercises logged with side. Display as a diverging bar or a paired bar with target band (e.g. 1:1 to 1:1.5 pull-weighted is common gym advice, no citation found).

### Gaps
- No peer-reviewed evidence found for ideal push:pull or quad:hamstring ratios; no app documentation found for L/R computation.

## 3. Cardio machine stats (no GPS)

### Takeaway
Show time, distance, and machine-native pace/power, plus HR-derived zones and load only when heart rate is available. Machine calorie figures are overestimates, worst on ellipticals; label as "machine estimate".

### Cited Findings
- Concept2: watts = 2.80 / (pace per metre)^3, i.e. 2.8/(split/500)^3; a 2:00/500m split is about 202 W. Calories/hour = 4 x watts x 0.8604 + 300, based on a 175 lb person (another site gives +350, so constant is inconsistent). — [Concept2 watts calculator (archived)](https://archived.concept2.com/training/calculators/watts); [Concept2 units](https://www.concept2.com/products/understanding-and-changing-units); [topendsports rowing](https://www.topendsports.com/testing/tests/rowing-ergo-2km.htm)
- No independent accuracy test of Concept2 power found; Oxford page suggests the constant is an approximation. — [Oxford ergometer physics](https://eodg.atm.ox.ac.uk/user/dudhia/rowing/physics/ergometer.html)
- Machine calorie overestimates: elliptical about 100 kcal per 30 min at moderate intensity (34 adults vs indirect calorimetry) — [Exercise Medicine 2018 (DOAJ)](https://doaj.org/article/37d08913b6004a4f901ea440279679ef); 2010 ABC test: treadmill +13%, bike +7%, stair climber +12%, elliptical +42% (single older test, rough) — [GMA](https://www.goodmorningamerica.com/wellness/story/accuracy-exercise-machines-18559149). Machines typically use only sex, age, weight — [Fox News](https://www.foxnews.com/health/how-accurate-are-cardio-machines-calorie-counters.amp)
- TRIMP: Banister = duration x HR-reserve fraction x exponential weight (b = 1.92 men, 1.67 women); Edwards = sum of minutes in five %HRmax zones x linear weights 1-5. Both are internal-load metrics with known limits on interval work. — [Hull repository PDF](https://hull-repository.worktribe.com/OutputFile/443111); [Eur J Sport Sci](https://informahealthcare.com/doi/full/10.1080/17461391.2014.922621)
- Health Connect types usable for machine cardio: ExerciseSession (types include RUNNING_TREADMILL, BIKING_STATIONARY, ROWING_MACHINE, STAIR_CLIMBING_MACHINE, ELLIPTICAL), HeartRate (series), Power (series), Speed, Distance, CyclingPedalingCadence, FloorsClimbed, ActiveCaloriesBurned, TotalCaloriesBurned, Vo2Max, ElevationGained. — [Health Connect data types](https://developer.android.com/health-and-fitness/health-connect/data-types)

### Inferences
- Per machine (display set; METs/formulas [UNVERIFIED] beyond cited): treadmill: time, distance, avg speed or pace/km, incline, (grade-adjusted pace = derived, flag as estimate); stair climber: time, floors, steps/min, level; rower: time, distance, avg split/500m, watts, SPM, stroke count, calories; bike: time, distance, avg watts, RPM, resistance; elliptical: time, distance, resistance, SPM; ski erg: split/500m, watts (same Concept2 formula family). Plus HR avg/max, time in zone, Edwards TRIMP (simplest to explain; zones from %HRmax).
- Compute own calories from MET x weight x time only as fallback, and show machine value alongside with disclaimer; trend per machine, not across machines.
- No GPS means no elevation/route; treadmill incline can substitute for climb.

### Gaps
- Ski erg, stair climber (floors/min), elliptical-specific metric definitions: no vendor documentation retrieved. MET compendium values not retrieved (cite Compendium of Physical Activities before use).
- Concept2 FIT/CSV export schema not checked.

## 4. Body stats

### Takeaway
Trend weight uses an exponentially weighted average; the classic constant is 0.1. MacroFactor documents a recency-weighted trend that tolerates gaps but publishes no constant.

### Cited Findings
- Hacker's Diet: Trend_n = Trend_(n-1) + 0.1 x (Weight_n - Trend_(n-1)); lags true change. — [Fourmilab Hacker's Diet](https://fourmilab.ch/hackdiet/www/subsection1_4_1_0_8.html); [Wikipedia](https://en.wikipedia.org/wiki/The_Hacker%27s_Diet)
- MacroFactor: trend is a moving average weighting newer entries more, resilient to gaps; expenditure and targets derive from trend, not scale weight. Exact constant not published in what I found. — [MacroFactor weight trend](https://help.macrofactorapp.com/en/articles/278-weight-trend); [MacroFactor algorithms](https://macrofactor.com/macrofactors-algorithms-and-core-philosophy/)
- Health Connect: Weight, BodyFat, LeanBodyMass, BodyWaterMass, BoneMass, Height types exist. — [Health Connect data types](https://developer.android.com/health-and-fitness/health-connect/data-types)

### Inferences
- Plot raw weigh-ins as dots (low emphasis) plus trend line; handle gaps by applying the EWMA over elapsed days (alpha scaled by gap) [UNVERIFIED implementation choice]. Show weekly rate of change as % bodyweight from trend.
- Measurements (waist, arm, etc.): small line per site with latest delta; photos: side-by-side slider with date labels, stored locally. No citations found on photo UX.

### Gaps
- No Libra source retrieved; no research on measurement or photo UX.

## 5. Recovery/readiness inputs via Health Connect

### Takeaway
Sleep, resting HR, HRV (RMSSD), steps, respiratory rate, SpO2, skin temp are readable; scores are proprietary and unvalidated, so present inputs and baseline deviations rather than a single opaque score.

### Cited Findings
- Types: SleepSession (stages), RestingHeartRate, HeartRateVariabilityRmssd, Steps, RespiratoryRate, OxygenSaturation, SkinTemperature, each with its own READ_ permission; background and history (>30 days) need separate permissions. — [Health Connect data types](https://developer.android.com/health-and-fitness/health-connect/data-types); [Sleep guide](https://developer.android.com/health-and-fitness/health-connect/experiences/sleep)
- Whoop Recovery 0-100% from HRV, resting HR, respiratory rate, SpO2, sleep performance, skin temperature. — [Whoop](https://www.whoop.com/de/en/the-data/)
- Garmin Body Battery: HRV-based stress, sleep, rest and activity via Firstbeat; secondary sources only. Weights unpublished for both. — [Runner's Picks](https://www.runnerspicks.com/blog/garmin-body-battery-vs-whoop-recovery-score/); [the5krunner on Altini critique ("made up scores")](https://the5krunner.com/2025/08/19/garmin-body-battery-slammed-indirectly-by-altini-made-up-scores/)

### Inferences
- Readiness = z-score of last-night HRV and RHR vs the user's own 28-day baseline, plus sleep duration vs need; show as three small deltas, not a composite. Data availability depends on the user's wearable writing to Health Connect; build graceful empty states.

### Gaps
- No peer-reviewed validation of composite readiness scores retrieved.

## 6. What users say is useful versus confusing; competitor criticism

### Takeaway
Evidence here is weak: no direct forum/review threads were retrieved. Indirect sources suggest users like quick logging and per-exercise progress charts, and want deeper filtering, export and insight rather than raw data.

### Cited Findings
- Strong: praised for fast logging and reliable progression tracking; complaints about advanced programming; offers CSV export. Hevy: charts per exercise and volume trends; limited advanced filtering and custom charting; export weaker. These are from competitor blog Setgraph and a review site, so treat as biased. — [Setgraph Hevy vs Strong](https://setgraph.app/ai-blog/hevy-vs-strong); [Hevy review](https://repreturn.com/?p=1625)
- Third-party dashboard LiftShift exists to turn Hevy/Strong exports into analytics, signalling unmet demand. — [Product Hunt LiftShift](https://www.producthunt.com/p/liftshift-app/liftshift)
- Fitbod shows "Estimated Strength" as its main progress metric (page not readable). — [Fitbod blog](https://fitbod.me/blog/estimated-strength?fitbodUser=1)
- Garmin Body Battery and Whoop scores criticised as opaque. — [the5krunner](https://the5krunner.com/2025/08/19/garmin-body-battery-slammed-indirectly-by-altini-made-up-scores/)

### Inferences
- Opportunity: explain every number (tap for formula and data used), allow export, offer insight sentences next to charts.

### Gaps
- No Reddit/Play Store review text retrieved; no Strava, Garmin Connect, or Whoop UI criticism beyond the above. No UX research on stats screens found. Recommend a follow-up pass with Reddit/Play Store access.

## 7. Small-screen data visualization and accessibility

### Takeaway
Material treats accessibility as a starting constraint: colour-blind-safe palettes, patterns or labels beyond colour, text summaries and data tables for screen readers, no hover-only information.

### Cited Findings
- Material team guidance: accessibility-first chart design; respect different needs for depth, complexity and modality. — [Material blog](https://m2.material.io/blog/data-visualization-accessibility); [Smashing Magazine (Material team)](https://smashingmagazine.com/2022/07/accessibility-first-approach-chart-visual-design/)
- Use colour-blind-safe palettes, offer pattern fills; alt text states chart type and key takeaways; provide a data table; do not rely on hover for labels. — [Smashing 2024](https://www.smashingmagazine.com/2024/02/accessibility-standards-empower-better-chart-visual-design); [Mass.gov](https://www.mass.gov/info-details/data-visualization-accessibility); [Morningstar](https://design.morningstar.com/systems/data-visualization/guidelines/accessibility)
- I did not open the Material 3 chart guidance pages themselves.

### Inferences (design recommendations, not cited)
- Trends over time: line (e1RM, bodyweight trend with dots); weekly totals: bar; distribution across muscles: horizontal bars sorted, with target band (avoid radar); comparisons within a week: bullet bar vs target; consistency: calendar heat strip; sparklines for list rows. Tap-to-scrub (touch targets >= 48dp) instead of hover. Provide Semantics label per chart ("e1RM bench press rose from 80 to 90 kg over 12 weeks") and a "view as table" option in Flutter.

### Gaps
- No small-screen-specific empirical study retrieved; Flutter chart library accessibility (fl_chart, etc.) not checked.
