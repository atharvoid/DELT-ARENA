# Tap-only agentic AI coach: design patterns, trust, safety (Delt Arena "Coach" screen)

Method note: WebSearch worked (results are search-engine summaries of pages). WebFetch only worked for microsoft.com; pair.withgoogle.com, fda.gov, nngroup.com, support.google.com, research.google all failed DNS ("outside allowed network domains"). So most claims below rest on search summaries, not full-page reads; marked [search-summary]. Nothing was reconstructed from memory. Date context: Nov 2026.

## 1. Non-text AI interaction patterns (chips, decision cards, generative UI, approval queues, undo)

### Takeaway
The only primary-source-verified guidance is Microsoft HAX (dismiss/correct/scope-when-in-doubt/explain). Real products (Whoop, Oura) are chat-first; no researched fitness product is verified tap-only, so a tap-only Coach is largely a design synthesis. Generative UI exists (Google) but is slow and occasionally inaccurate, which argues for a fixed, typed card catalogue rendered natively in Flutter.

### Cited Findings
- Microsoft's 18 guidelines (CHI 2019) are directly applicable: 07 Support efficient invocation, 08 Support efficient dismissal, 09 Support efficient correction ("easy to edit, refine, or recover when the AI system is wrong"), 10 Scope services when in doubt ("disambiguation or gracefully degrade"), 11 Make clear why the system did what it did, 15 Encourage granular feedback, 16 Convey consequences of user actions, 17 Provide global controls, 18 Notify users about changes — [Microsoft Research blog](https://www.microsoft.com/en-us/research/blog/guidelines-for-human-ai-interaction-design/) (full page read)
- Guidelines were derived from 150+ candidate guidelines and tested with 49 practitioners across 20 AI products; authors say they are not a simple checklist — [search-summary of Microsoft pages](https://www.microsoft.com/en-us/research/publication/guidelines-for-human-ai-interaction/)
- NN/g: prompt suggestions come in three types (use-case, prompt-autocomplete, follow-up); users often ignore suggestions when badly placed or not useful; well-designed ones set accurate expectations — [NN/g Prompt Suggestions](https://www.nngroup.com/articles/prompt-suggestions/) [search-summary only; page fetch blocked]
- Google generative UI: Gemini app "dynamic view" and "visual layout" experiments; Gemini 3 Pro generates HTML/CSS/JS per prompt; human-expert-built sites preferred most, generative UI second; can take a minute or more and has occasional inaccuracies — [Google Research blog](https://research.google/blog/generative-ui-a-rich-custom-visual-interactive-user-experience-for-any-prompt/) [search-summary]
- Whoop Coach (Sept 2023, GPT-4): opened via home-screen action button, user types question; uses biometrics + Journal; can be turned off in Settings — [Whoop press](https://www.whoop.com/us/en/press-center/whoop-unveils-the-new-whoop-coach-powered-by-openai/) [search-summary]
- Oura Advisor (rolled out to all members March 2025): opt-in LLM using sleep/activity/readiness/stress; user-reviewable and deletable "Memories"; choice of conversational vs direct tone and check-in frequency; says it can make mistakes — [Oura blog](https://ouraring.com/blog/oura-advisor), [BusinessWire](https://www.businesswire.com/news/home/20250331565896/en/Oura-Advisor-an-AI-powered-Personal-Health-Companion-Now-Rolling-Out-to-All-Oura-Members) [search-summary]
- Strava Athlete Intelligence: generates per-activity summary and comments on sections of a workout (push-style insight, no chat); out of beta — [TechRadar](https://techradar.com/health-fitness/i-used-stravas-new-athlete-intelligence-ai-feature-for-a-week-heres-what-happened), [Android Central](https://www.androidcentral.com/wearables/strava-announces-stable-athlete-intelligence-anti-cheating-and-flyover-sharing) [search-summary]
- Fitbod: adjusts rep ranges/weights from logged workouts, "learns from your edits", and has a Recovery view where users can edit which muscle groups are marked fresh (a tap-based user override) — [Apple App Store listing](https://apps.apple.com/au/app/id1041517543?l=en-au), [Garage Gym Reviews](https://www.garagegymreviews.com/fitbod-review) [search-summary; many pages are affiliate]

### Inferences
- Strava's push-insight model and Fitbod's edit-the-recovery-state model are the closest precedents to tap-only; Whoop/Oura show the chat-first norm the Coach screen deliberately departs from.
- Because generative UI is slow/occasionally wrong, have the LLM emit structured JSON for a closed set of native card types (proposal card, question card, info card, pain card) rather than free-form UI. (Design inference, not sourced.)
- Map HAX 08/09/11 to every card: Dismiss, Edit (stepper) and Why. (Inference.)

### Gaps
- Could not verify: Material 3 Expressive guidance (search returned nothing), Apple Intelligence suggestions, Copilot "proposed changes"/agent-inbox patterns, any tap-only AI coach in market. No sourced pattern for undo of agent actions was retrieved.

## 2. Trust in AI recommendations (explainability, confidence, control, autonomy)

### Takeaway
Guidance converges on calibrated trust: show why, show confidence only where it changes the decision, keep user in control, and prefer suggest-then-confirm for high-stakes (body/injury) actions.

### Cited Findings
- PAIR Guidebook (Explainability + Trust): explanations central to trust; goal is calibrated trust (users trust in some situations, verify in others); how/when confidence is shown affects user action; suggested tactics include prompting verification in low-confidence or high-stakes cases and not showing a "what" without a "why" in high-stakes cases — [PAIR chapter](https://pair.withgoogle.com/chapter/explainability-trust/), [Codelab](https://codelabs.developers.google.com/codelabs/pair-guidebook) [search-summary; page fetch blocked]
- Microsoft HAX 02 "Make clear how well the system can do what it can do" (how often it may be wrong) and 17 "Provide global controls" — [Microsoft](https://www.microsoft.com/en-us/research/blog/guidelines-for-human-ai-interaction-design/)
- Oura exposes controls (memory review/delete, tone, frequency) — [Oura blog](https://ouraring.com/blog/oura-advisor) [search-summary]

### Inferences
- Autonomy ladder suggestion: auto-apply only reversible, low-load changes (e.g. +/-2.5 kg next set within a user-set band); require a tap-confirm for program structure, deloads, exercise swaps; pain-related changes always confirmed. (Inference.)
- "Show the math" = one-line evidence chip (e.g. "3 sessions at RPE 9+"), expandable. (Inference.)

### Gaps
- No quantitative studies on confidence display or autonomy levels in fitness retrieved; no Nielsen Norman study text retrieved (blocked).

## 3. Tap-only clarifying questions (pain map, scales, question count)

### Takeaway
No sourced research on body-map pain input or question-fatigue limits was retrieved. Only HAX 10 (disambiguate or degrade gracefully when uncertain) and 15 (granular feedback) are verified.

### Cited Findings
- HAX 10 "Scope services when in doubt" and 15 "Encourage granular feedback" — [Microsoft](https://www.microsoft.com/en-us/research/blog/guidelines-for-human-ai-interaction-design/)
- NN/g notes follow-up suggestions exist to keep users engaged and that suggestions get ignored when poorly placed — [NN/g](https://www.nngroup.com/articles/prompt-suggestions/) [search-summary]

### Inferences
- Unsourced design heuristics to validate in testing: max 1 question per card, 3-5 options plus "Skip"; ask only when the answer changes the proposal; remember answers; cap daily questions. Body map -> severity 0-10 or 3-level -> onset (during/after/at rest) -> "sharp vs ache" is a plausible pain flow.

### Gaps
- No peer-reviewed or industry source on question counts/survey fatigue, body-map UX, or pain scales (NRS) was found in this pass.

## 4. Showing and reverting automatic actions

### Takeaway
Only principle-level support found: HAX 09 (recover), 16 (convey consequences), 18 (notify of changes). No product example of an agent activity log with revert was retrieved.

### Cited Findings
- HAX 09, 16, 18 — [Microsoft](https://www.microsoft.com/en-us/research/blog/guidelines-for-human-ai-interaction-design/)
- Fitbod lets users edit its recovery state and says it learns from edits — [App Store listing](https://apps.apple.com/au/app/id1041517543?l=en-au) [search-summary]

### Inferences
- Treat every agent action as a versioned program diff (before/after, reason, timestamp) with one-tap "Undo"; keep log on the Coach screen. (Design inference.)

### Gaps
- No sourced examples of Copilot-style proposed-change diffs, agent inbox, or undo timeouts; Material/Android snackbar-undo guidance not researched.

## 5. Safety, regulation, store policy

### Takeaway
Stay in "general wellness" claims, avoid diagnosis/treatment language, disclose AI, escalate pain red flags to professionals, and complete Google Play health declarations. Details must be confirmed against primary pages that were not retrievable.

### Cited Findings
- FDA reissued "General Wellness: Policy for Low Risk Devices" as final guidance Jan 6, 2026 (replacing 2019): FDA does not intend to regulate low-risk general-wellness products intended solely for wellness; 2026 update clarifies noninvasive products estimating physiologic measures can qualify; claims must avoid references to disease — [FDA guidance page](https://fda.gov/regulatory-information/search-fda-guidance-documents/general-wellness-policy-low-risk-devices), [Loeb & Loeb](https://www.loeb.com/en/insights/passle/2026/01/fda-updates-its-general-wellness-device-frameworkwhat-companies-need-to-know), [Troutman](https://www.troutman.com/insights/fdas-2026-guidance-on-general-wellness-devices-policy-for-low-risk-devices/) [search-summary; law-firm secondary sources]
- Google Play: health apps must complete the Health apps declaration and have a privacy policy; Health Connect data is sensitive user data (Health Connect questions in declaration since Aug 31, 2024); apps must not be misleading about health and must remind users to consult a professional; apps doing diagnosis/treatment recommendation/clinical monitoring may be SaMD; non-health apps with health features still in scope — [Play policy](https://support.google.com/googleplay/android-developer/answer/16679511?hl=en), [Health Connect FAQ](https://support.google.com/googleplay/android-developer/answer/12991134) [search-summary; may be outdated]
- EU AI Act Art. 50: AI systems interacting directly with people must disclose AI nature (before/at start); applies from 2 Aug 2026; applies regardless of high-risk status; emotion-recognition deployers must inform exposed people. Sources conflict on whether Commission Art. 50 guidelines are final (Stibbe says adopted 20 July 2026; another describes draft) — [Commission FAQ](https://digital-strategy.ec.europa.eu/en/faqs/transparency-obligations-under-article-50-ai-act), [Stibbe](https://www.stibbe.com/publications-and-insights/the-ai-acts-transparency-obligations-rules-scope-and-timeline), [artificialintelligenceact.eu](https://artificialintelligenceact.eu/transparency-rules-article-50/) [search-summary]

### Inferences
- A tap-only coach has no chat, but still "interacts directly" with people; a persistent "AI-generated" label on cards is the cheap compliant move. (Inference; legal review needed.)
- Pain handling: never diagnose; red-flag answers (numbness, chest pain, night pain, trauma) route to "see a professional" and stop progressive-load proposals. (Design inference.)

### Gaps
- Primary text of Play policy, FDA guidance and EU AI Act not read (blocked); no sourced disclaimer wording or red-flag list; no evidence on how wellness-claim wording interacts with injury advice.

## 6. Useful vs gimmicky AI coaches

### Takeaway
Evidence is thin and mostly vendor-reported or affiliate reviews; usefulness comes from translating existing data into actions, gimmickiness from generic or overly positive output.

### Cited Findings
- Oura (company survey of Labs testers): 60% said Advisor helped understand metrics, 56% said it helped turn insights into actions — [Oura blog](https://ouraring.com/blog/oura-advisor) [search-summary; vendor claim]
- Strava: company says 80%+ of polled subscribers find Athlete Intelligence very helpful (vendor claim); T3 reviewer found comments upbeat/positive-focused, suiting beginners; one reader comment says it feels like statistical analysis after a few workouts (anecdotal) — [T3](https://t3.com/active/strava-athlete-intelligence-i-tried), [TechRadar](https://techradar.com/health-fitness/i-used-stravas-new-athlete-intelligence-ai-feature-for-a-week-heres-what-happened) [search-summary]
- Fitbod: reviews praise adaptation to logged results; user complaints include lost logged sets and poor support — [Trustpilot](https://www.trustpilot.com/review/fitbod.me?page=2), [Garage Gym Reviews](https://www.garagegymreviews.com/fitbod-review) [search-summary]
- Reviewers of Oura Advisor note it is not a doctor — [Tom's Guide](https://www.tomsguide.com/wellness/fitness/ouras-ai-powered-advisor-is-rolling-out-heres-what-it-means-for-you) [search-summary]

### Inferences
- Data-grounded, specific, actionable proposals (with a number change) are the differentiator; generic praise is the gimmick risk. Reliability of core logging matters more than AI polish (Fitbod complaint).

### Gaps
- No independent usability studies or large-scale user-review analysis of AI fitness coaches; Whoop Coach user reception (e.g. 9to5Google hands-on) not read; Reddit/app-store sentiment not sampled.
