# Training science for a rule-engine coaching app (partial: fetch tools blocked)

Method note: every WebFetch failed (getaddrinfo ENOTFOUND) for pubmed.ncbi.nlm.nih.gov, ncbi.nlm.nih.gov, pmc.ncbi.nlm.nih.gov, link.springer.com, jissn.biomedcentral.com, bjsm.bmj.com, sportrxiv.org and strongerbyscience.com. These hosts must be allowed in the session network settings before the missing items below can be verified. All findings come from WebSearch result summaries only, not full texts. Treat every number as "search-snippet level, verify against the primary paper before shipping". Nothing was reconstructed from memory; items I could not source are in Gaps.

## 1. Weekly volume, per-session limits, frequency

### Takeaway
More weekly sets produce more hypertrophy with diminishing returns; strength shows stronger diminishing returns than hypertrophy. Twice-weekly per-muscle training beats once weekly (volume-equated); the benefit of 3+ per week is unresolved. Exact set landmarks could not be verified from primary text.

### Cited Findings
- Schoenfeld, Ogborn and Krieger meta-regression: weekly sets had a significant graded effect on muscle size (P = 0.002) when treated continuously; the categorical <5 / 5-9 / 10+ comparison only trended (P = 0.074), and the data were insufficient to say whether more than 10 weekly sets per muscle adds benefit — [ResearchGate PDF of paper](https://researchgate.net/profile/Brad-Schoenfeld/publication/305455324_Dose-response_relationship_between_weekly_resistance_training_volume_and_increases_in_muscle_mass_A_systematic_review_and_meta-analysis/links/59dc0269458515e9ab4527d6/Dose-response-relationship-between-weekly-resistance-training-volume-and-increases-in-muscle-mass-A-systematic-review-and-meta-analysis.pdf) (via search summary)
- Pelland, Remmert, Robinson, Hinson, Zourdos (2024) meta-regression, a SportRxiv preprint (search result described it as not peer reviewed; a later peer-reviewed status is unverified): the volume-hypertrophy relationship differs from volume-strength, with strength showing more pronounced diminishing returns; frequency has consistently identifiable effects only on strength, not hypertrophy — [SportRxiv preprint 460](https://sportrxiv.org/index.php/server/preprint/view/460)
- Follow-up preprint on per-session volume (Remmert, Pelland et al.): more volume per session still had a positive slope for both strength and hypertrophy, with diminishing returns, stronger for strength — [SportRxiv preprint 537](https://sportrxiv.org/index.php/server/preprint/view/537)
- Frequency: Schoenfeld, Ogborn and Krieger 2016 concluded that, volume-equated, training a muscle twice weekly is superior to once weekly; whether three times beats twice is undetermined — [PubMed 27102172](https://pubmed.ncbi.nlm.nih.gov/27102172/). Counter-view: a 2019 review found that under volume-equated conditions frequency has no pronounced effect on muscle gain — [PubMed 30236847](https://pubmed.ncbi.nlm.nih.gov/30236847/)
- A different grouping in a later meta-analysis (six studies only) suggested 12-20 weekly sets per muscle may be a reasonable standard recommendation — same ResearchGate/search listing above (weak evidence, small k)
- Practitioner opinion (not peer reviewed): Schoenfeld in interviews suggests 10-20 sets per week per muscle, and that most gains come from relatively low volume — [FitnessVolt interview summary](https://fitnessvolt.com/dr-schoenfeld-examines-ideal-set-range-for-maximizing-hypertrophy/)
- Practitioner opinion: Henselmans argues productive volume tops out around 9-13 sets per muscle per workout — [Menno Henselmans](https://mennohenselmans.com/maximum-productive-training-volume-per-session/); a Biolayne write-up of a meta-regression reports about 11 fractional sets per session as a hypertrophy threshold and about 2 direct sets per session for strength — [Biolayne](https://biolayne.com/reps/issue-36/too-much-muscle-math-finding-the-ideal-training-volume-per-session/). Both are secondary interpretations.
- ACSM 2009 position stand frequency by training level: 2-3 d/wk novice, 3-4 intermediate, 4-5 advanced (whole-body or split not specified in the snippet) — [PubMed 19204579](https://pubmed.ncbi.nlm.nih.gov/19204579/)

### Inferences
- A defensible engine range, consistent with the sources but not directly stated by any single one: roughly 10-20 hard sets per muscle per week for hypertrophy goals, with lower (about 6-10) acceptable for beginners, maintenance or time-limited users. These cutoffs are my synthesis, not a cited number.
- Spread weekly sets over at least 2 sessions per muscle; cap per-session sets per muscle at roughly 10 as a soft warning (practitioner-sourced, low confidence).

### Gaps
- RP volume landmarks (MV/MEV/MAV/MRV) not retrieved; the RP site was not searched. Report as practitioner framework only once sourced.
- Baz-Valle 2022 review not retrieved. Pelland peer-reviewed numbers (e.g. effect sizes per set) not retrieved.
- Volume by training age: no source found.

## 2. Rep ranges, proximity to failure, progression, deloads

### Takeaway
Hypertrophy is similar across a wide load range if sets are hard; strength favors heavier loads. Training to failure gives at most a trivial hypertrophy advantage, so leaving some reps in reserve is defensible. Deloads are common practice with a consensus definition but little trial evidence.

### Cited Findings
- Low load (<=60% 1RM) vs high load: hypertrophy similar, 1RM strength greater with high load — Schoenfeld et al. 2017 meta-analysis, [PubMed 28834797](https://pubmed.ncbi.nlm.nih.gov/28834797/)
- Network meta-analysis (Lopez et al. 2021): no hypertrophy differences between low (>15RM), moderate (9-15RM) and high (<=8RM) loads when taken to failure; strength superior with high and moderate loads — [PubMed 33433148](https://pubmed.ncbi.nlm.nih.gov/33433148/)
- Refalo et al. 2023 (Sports Med, 15 studies): training to failure vs not had only a trivial hypertrophy advantage (ES 0.19, p = 0.045); no advantage when restricted to momentary muscular failure; authors suggest a non-linear relationship — [PubMed 36334240](https://pubmed.ncbi.nlm.nih.gov/36334240/)
- Robinson et al. 2024 meta-regression on RIR (exploratory): hypertrophy is meaningfully influenced by RIR, strength gain is not — [Abertay repository](https://rke.abertay.ac.uk/en/publications/exploring-the-dose-response-relationship-between-estimated-resist/)
- ACSM 2009: novices 8-12RM loads; intermediate/advanced eventually heavy loading (1-6RM) emphasis; 2-3 min rest between sets suggested (from a fragmentary secondary copy; verify) — [PubMed 19204579](https://pubmed.ncbi.nlm.nih.gov/19204579/)
- Deloading: a Delphi consensus (Bell et al. 2023, Sports Med Open) proposes a definition of a period of reduced training load to limit fatigue and improve readiness; coaches most often report a one-week deload, range one session to two weeks; no clear operational definition existed in the literature — [PMC10511399](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10511399/), [PMC9811819](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9811819/)

### Inferences
- Engine default: 5-30 rep range acceptable for hypertrophy; use 6-12 for compound lifts, 10-20 for isolation, 3-8 for strength goals, and 1-3 RIR on most sets. These specifics are my synthesis.
- Deload trigger: scheduled every 4-8 weeks or reactive on performance drops plus fatigue reports; one week at reduced sets/RIR. Timing numbers are not sourced.

### Gaps
- Double progression, linear progression and RIR-based autoregulation rules, plateau rules and specific load-increment percentages: no source retrieved (ACSM 2-10% rule could not be confirmed).
- Deload frequency and exact volume/intensity reduction not retrieved (Delphi paper full text blocked).

## 3. Program templates and onboarding inputs

### Takeaway
Not researched to a citable level.

### Cited Findings
- ACSM 2009 suggests 2-3 sessions/week novices, 3-4 intermediate, 4-5 advanced — [PubMed 19204579](https://pubmed.ncbi.nlm.nih.gov/19204579/)
- Twice-weekly per-muscle frequency is supported (section 1), which is the evidence-based constraint templates should meet.

### Inferences
- Templates meeting twice-per-week frequency: 2 days = full body x2; 3 = full body x3; 4 = upper/lower x2; 5 = upper/lower plus one body-part or PPL-hybrid; 6 = PPL x2. Common practice, not sourced here.
- Inputs likely to change the program: goal, days/week, session length, equipment, training age, injuries. Age, sex, height matter mainly for energy/protein estimates and recovery caution. Unsourced judgment.

### Gaps
- No sources found for template-by-goal fit, or for which onboarding inputs matter in evidence terms.

## 4. Concurrent training and cardio dosing

### Takeaway
Interference is mostly in power and explosive strength; effects on hypertrophy and maximal strength are small or absent in newer meta-analysis. WHO gives the health baseline.

### Cited Findings
- Wilson et al. 2012 (21 studies): concurrent training reduced hypertrophy, strength and especially power versus lifting alone, with running (not cycling) most detrimental; one summary gave hypertrophy ES 0.85 vs 1.23 and power ES 0.55 vs 0.91; snippets disagreed on strength figures — [bib record](https://bvbvf1.bib-bvb.de/vufind/PrimoRecord/cdi_proquest_miscellaneous_1027372546)
- A 2021 meta-analysis (43 studies) found no interference on maximal strength and hypertrophy regardless of aerobic mode, but possible attenuation of explosive strength — [Springer s40279-021-01587-7](https://link.springer.com/article/10.1007/s40279-021-01587-7)
- WHO 2020 adults: 150-300 min moderate or 75-150 min vigorous aerobic per week (or equivalent); muscle strengthening of all major groups at moderate or greater intensity on 2+ days/week; older adults add multicomponent balance/strength on 3+ days — [BJSM 2020;54:1451](https://bjsm.bmj.com/content/54/24/1451), [PMC7719906](https://pmc.ncbi.nlm.nih.gov/articles/PMC7719906/)

### Inferences
- Warn rather than block on cardio: put hard running away from lower-body lifting days; prefer cycling/low-impact for users prioritizing leg hypertrophy. Rule thresholds unsourced.

### Gaps
- Heart-rate zone definitions, cardio dose for fat loss, ACSM cardio guidelines, cardio-spike thresholds (e.g. weekly increase limits): not retrieved.

## 5. Energy and protein

### Takeaway
Protein of about 1.4-2.0 g/kg/day is the ISSN range; 1.6 g/kg is where muscle-gain benefit plateaus in a meta-regression; higher is used in deficits. Rate-of-change numbers conflict across authors' publications.

### Cited Findings
- ISSN 2017 position stand: 1.4-2.0 g/kg/day sufficient for most exercisers; 2.3-3.1 g/kg/day of may be needed to maximize lean mass retention in resistance-trained people in hypocaloric diets; about 0.25 g/kg or 20-40 g per dose — [PubMed 28642676](https://pubmed.ncbi.nlm.nih.gov/28642676/) (abstract-level; per-dose figure from a secondary summary)
- Morton et al. 2018 (49 studies, n=1863): protein beyond about 1.6 g/kg/day gave no further resistance-training-induced fat-free mass gains; age lowers and training experience raises supplementation efficacy — [PubMed 28698222](https://pubmed.ncbi.nlm.nih.gov/28698222/)
- Helms et al. 2014 (contest prep): protein 2.3-3.1 g/kg lean mass, loss 0.5-1% bodyweight/week; the 2020 update (Roberts et al.) revised to 1.8-2.7 g/kg and <=0.5%/week during competition — [PMC4033492](https://pmc.ncbi.nlm.nih.gov/articles/PMC4033492), [PMC7052702](https://pmc.ncbi.nlm.nih.gov/articles/PMC7052702). These are for physique athletes, not the general population.
- Iraki et al. 2019 off-season review: secondary sites attribute a 0.25-0.5% bodyweight/week gain rate to it; surplus size could not be verified (secondary sources said 5-10% or 300-500 kcal) — [PubMed 31247944](https://pubmed.ncbi.nlm.nih.gov/31247944/)
- Recomposition: a 2020 Barakat et al. review (Strength Cond J) is cited as supporting recomposition with resistance training, high protein and moderate deficit or maintenance calories; blog summary suggests 1.6-2.4 g/kg and novices/returners benefit most, unverified — [GetFitCraft summary](https://getfitcraft.com/science/body-recomposition-research)

### Inferences
- Default protein 1.6-2.2 g/kg for most goals, up to about 2.4 g/kg in deficits for lean users. Suggested mapping (weak sourcing): fat loss 0.5-1%/wk loss, bulk 0.25-0.5%/wk gain, recomp near maintenance for beginners/returners.

### Gaps
- General-population fat-loss deficit size and safe floor calories: not sourced. ISSN full text blocked.

## 6. Maintenance (reduced training)

### Takeaway
Muscle can be maintained on much less volume than gained it, more reliably in the young.

### Cited Findings
- Bickel et al. 2011: after 16 weeks of training, doses cut to one-third or one-ninth maintained hypertrophy in young but not older adults; strength was largely retained — [PubMed 21131862](https://pubmed.ncbi.nlm.nih.gov/21131862/)
- Secondary summary: 1-2 sessions/week at about one-ninth volume may maintain — [Examine](https://examine.com/conditions/muscle-size-and-strength/faq/what-happens-if-i-fall-off-the-gainz-train-how-much-exercise-is-needed-to-maintain-what-ive-built) (secondary; caution)

### Gaps
- Spiering 2021 review not searched or retrieved.

## 7. Warning thresholds for user-built programs

### Takeaway
No source gave tested warning thresholds. These must be derived from sections 1-4 and labelled app heuristics.

### Inferences
- Candidate flags: under about 6 weekly sets per target muscle (too few); over about 20-25 (high, practitioner-level); more than about 10 sets per muscle in one session; muscle trained only once per week at low volume; push:pull and quad:hamstring imbalance (no evidence-based ratio found); load jumps; fewer than 1-2 rest days; sudden cardio increases. All numeric cutoffs unsourced here.

### Gaps
- Imbalance ratios, load-increase caps, rest-day minimums, cardio spike thresholds (e.g. 10% rule) have no retrieved sources.

## 8. Pain, injury, red flags, disclaimers

### Takeaway
The Silbernagel pain-monitoring model gives a usable rule: keep pain at or below about 5/10 during/after loading and back to baseline by next morning. Red-flag symptoms warrant stopping and medical care.

### Cited Findings
- Silbernagel model (Achilles/patellar tendon): pain not above 5/10 on NPRS during or immediately after activity, returning to pre-activity levels by next morning; monitor pain and stiffness weekly to adjust dose; some clinicians use 3/10; the score does not measure structural healing — [BMC Musculoskelet Disord table](https://bmcmusculoskeletdisord.biomedcentral.com/articles/10.1186/s12891-021-04553-6/tables/1), [E3 Rehab](https://e3rehab.com/how-to-rehab-tendon-injuries-and-pain/) (practitioner site for 3/10 vs 5/10 point)
- ACSM materials: chest pain or pressure with exercise, plus symptoms at rest or in exercise, should prompt stopping and contacting a health provider; for professionals, symptomatic clients should obtain medical clearance — [ACSM brochure](https://acsm.org/docs/default-source/files-for-resource-library/cpi-who-needs-a-stress-test-before-exercising-brochure.pdf), [ACE screening form](https://Www.Acefitness.Org/images/webcontent/assets/certification/ace-answers/forms/pt/21_Exercise_Preparticipation_Health-Screening_Questionnaire_For_Exercise_Pros.pdf)
- Consumer/fitness-press guidance: chest pain/pressure, fainting, dizziness, sudden shortness of breath mean stop; call emergency services if chest symptoms persist — [WTOP](https://wtop.com/news/2024/03/9-signs-you-should-stop-exercising-immediately) (low-authority source)

### Inferences
- App flow: pain report -> ask location, severity 0-10, type (sharp/ache), onset (acute/chronic), neuro symptoms -> if <=3-5 and settling, swap exercise or reduce load/range; if sharp, worsening, night pain, numbness, trauma -> advise stopping that movement and seeing a clinician.

### Gaps
- Neurological red flags (cauda equina, saddle numbness, bladder/bowel change), fracture, DVT signs: no source retrieved.
- How other apps phrase disclaimers: not researched.
- Tendon-specific model generalization to muscle or joint pain is not established in retrieved sources.
