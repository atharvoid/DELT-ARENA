# Logging Indoor Gym Cardio Machines Without GPS (Research Notes)

Scope: indoor cardio machines only, no GPS. Feeds the cardio logging screens of a Flutter, Android-first app.

Verification status: about 15 tool calls. Two fetches failed: the Bluetooth SIG FTMS spec page (www.bluetooth.com did not resolve in this session, so the FTMS byte-level field layouts were NOT verified) and the Concept2 PM5 interface PDF (never opened). Everything below marked "unverified" is either from background knowledge or from search snippets only.

---

## 1. Bluetooth FTMS: which data fields per machine type, and brand support

### Takeaway
FTMS (Fitness Machine Service) defines separate optional data characteristics for each machine type (treadmill, cross trainer, step climber, stair climber, rower, indoor bike). Brand support is real for some vendors (Matrix, Life Fitness, Technogym's Mywellness integration) but unverified for most. Exact per-machine field lists could not be verified in this session.

### Cited Findings
- FTMS 1.0 was adopted by the Bluetooth SIG Board in February 2017. The current revision is v1.0.1, dated 2024-10-01. Errata 23224 is mandatory for compliance claims. Source: search index of the Bluetooth SIG spec pages, https://www.bluetooth.com/specifications/specs/fitness-machine-service-1-0/ (search snippet only; page not fetched, and the host did not resolve when fetched directly).
- The FTMS Implementation Conformance Statement says Fitness Machine Features and Target Setting Features are mandatory. The machine-type data characteristics are all optional: Treadmill Data, Cross Trainer Data, Step Climber Data, Stair Climber Data, Rower Data, Indoor Bike Data. Training Status is also optional. Source: the FTMS ICS document index, https://files.bluetooth.com/download/ftms-ics-p4-pdf (search snippet only; not fetched).
- The spec allows one data record to be split across several notifications. A flag marks which fields are mandatory in each part, and Elapsed Time must be present when a record is split. Source: an unofficial MIT-hosted copy, https://community.appinventor.mit.edu/uploads/short-url/yTLhgjXECIekyCgPg0GOBz1k4Bh.pdf (unofficial; check against the official v1.0.1 PDF at https://files.bluetooth.com/download/ftms_v1-0-1).
- A Bluetooth SIG test suite includes test cases for Rower Data and Cross Trainer Data characteristics. Source: https://files.bluetooth.com/download/ftms-ts-p5-pdf (search snippet only).
- Matrix consumer treadmills, bikes and ellipticals state FTMS support and say they connect to FTMS-enabled apps (Zwift, Kinomap, etc.). Source: https://matrixhomefitness.com/pages/never-a-dull-workout (vendor marketing page).
- Life Fitness Track Connect 2.0 console spec lists "Enhanced Bluetooth Proximity, NFC, FTMS capability." Source: https://www.lifefitness.com/en-eu/catalog/cardio/consoles/track-connect-2-0-console
- Technogym's Mywellness can run on equipment from other makers that uses the Bluetooth Fitness Machine protocol. Brands named in the press coverage: Life Fitness, Matrix, Precor. Source: https://www.healthclubmanagement.co.uk/health-club-management-news/Technogym-opens-up-its-Mywellness-ecosystem-will-integrate-with-equipment-from-other-manufacturers/351148 (trade press, secondhand; date and scope not verified).
- Mywellness integrations page says it tracks cardio and strength machines that support FTMS, whatever the brand. Source: https://www.mywellness.com/de-DE/integrations
- Virtuagym has integrated with Matrix and Life Fitness cardio equipment. Source: same trade press coverage as above (secondhand).

### Inferences
- FTMS is a plausible primary read path for treadmills, ellipticals (cross trainer), and bikes on newer Matrix and Life Fitness units. Support for StairMaster, Peloton, Echelon, Keiser and Concept2 is NOT established by these sources.
- Because each machine type has its own optional characteristic, the app should parse per characteristic, not assume one universal record format.

### Gaps
- Byte-level field layouts for Treadmill, Cross Trainer, Step Climber, Stair Climber, Rower, and Indoor Bike data: NOT verified. Fetch the official v1.0.1 PDF (https://files.bluetooth.com/download/ftms_v1-0-1) from an allowed network before coding parsers.
- FTMS support for Technogym, Precor, StairMaster, Keiser, Peloton, Echelon: NOT verified. Only Matrix and Life Fitness have vendor-side claims above. Precor and Technogym evidence is secondhand press.
- Whether machines broadcast the standard Bluetooth Heart Rate Service separately from FTMS: NOT verified (see section 4).

---

## 2. Flutter / Android implementation: BLE, permissions, background limits

### Takeaway
flutter_blue_plus is a current, maintained package (2.3.15 on pub.dev at time of fetch) that supports Android 12+ scanning with BLUETOOTH_SCAN and BLUETOOTH_CONNECT and no location permission if the app does not derive location from BLE. Background operation on Android needs a foreground service or WorkManager, and the package docs say background use is an advanced case that may need a fork.

### Cited Findings
- flutter_blue_plus 2.3.15 supports Android, iOS, Linux, macOS, Web, Windows (Windows needs a separate winrt package). Source: https://pub.dev/packages/flutter_blue_plus
- Android 12+ permissions per the package docs: BLUETOOTH_SCAN (declare with usesPermissionFlags="neverForLocation" if you do not use BLE for location), BLUETOOTH_CONNECT, and ACCESS_FINE_LOCATION only if you use location or iBeacons (in that case also pass androidUsesFineLocation: true to startScan). Android 11 and lower need the legacy BLUETOOTH, BLUETOOTH_ADMIN and ACCESS_FINE_LOCATION permissions. Location services must be enabled for scanning on Android. Source: https://pub.dev/packages/flutter_blue_plus
- Android official guidance on BLUETOOTH_SCAN and neverForLocation: https://developer.android.com/develop/connectivity/bluetooth/bt-permissions
- Background: the package docs say background operation is an advanced use case and may need a fork. On Android the docs suggest flutter_foreground_task or workmanager. iOS uses bluetooth-central and restoreState. Source: https://pub.dev/packages/flutter_blue_plus
- Subscribing: listen to characteristic.onValueReceived, then call setNotifyValue(true). Cancel on disconnect with device.cancelWhenDisconnected(subscription). Source: https://pub.dev/packages/flutter_blue_plus
- A third-party plugin, bg_ble_scanner, keeps BLE scans running with a foreground service, per its pub.dev page: https://pub.dev/documentation/bg_ble_scanner/1.3.0/ (not evaluated in depth).

### Inferences
- A live workout session that must keep notifications flowing while the screen is off needs a foreground service with a visible notification on Android. Plan for this in the cardio session design.
- Because the app does not need location, request BLUETOOTH_SCAN with neverForLocation and avoid ACCESS_FINE_LOCATION. This is an inference from the package and Android docs; confirm on a device.

### Gaps
- Developer-reported reliability issues (dropped notifications, scan failures on specific Android OEMs, bond or reconnect loops): NOT researched. The search returned only old plugin versions and no issue threads. Check the flutter_blue_plus GitHub issue tracker before committing.
- Battery and OEM background restrictions (Samsung, Xiaomi): NOT researched.

---

## 3. Concept2 PM5 Bluetooth protocol and Concept2 Logbook API

### Takeaway
The PM5 exposes Bluetooth Smart (BLE) data, and Concept2 publishes a PM5 Bluetooth Smart Interface Definition PDF. An open-source library, c2bluetooth (OpenRowingCommunity), implements that spec. The Logbook API exists with a dev server, an approval gate for live use, and a stroke-level endpoint. The Logbook API is a strong option for reading results after a workout.

### Cited Findings
- The PM5 Bluetooth Smart Interface Definition PDF exists. The search found it only via a link in a TrainerRoad forum post, and the PDF itself was not opened. Forum post: https://www.trainerroad.com/forum/t/concept2-bikerg-connection/17004/21?page=2 . Concept2 software development page: https://www.concept2.com/support/software-development
- The c2bluetooth library references interface spec revision 1.27 and describes the link as low bandwidth, about 1000 bytes/s on Android and 640 bytes/s on iOS. Source: https://github.com/OpenRowingCommunity/c2bluetooth (README snippet; the API.md page fetched did not list fields or byte sizes, and points to docs/internals.md, not fetched).
- ErgData connects to the PM5 over Bluetooth only, per the App Store listing: https://apps.apple.com/ca/app/ergdata/id561716382
- Concept2 says it maintains an SDK for third-party developers and encourages third-party PM5 apps: https://www.concept2.com/support/software-development
- Logbook API docs: https://log.concept2.com/developers/documentation . Per search snippets: an API key is required from the developer portal; apps needing write access should use the dev server log-dev.concept2.com; live use requires approval (contact ranking@concept2.com); no rate limit currently, but abuse may lead to limits. Snippets also list status codes 422, 500, 503 and a workout validator on the dev site.
- Secondhand (unverified) endpoint notes from a third-party skill: GET /api/users/me/results and GET /api/users/me/results/{id}/strokes, Bearer token auth, default per_page 50 and max 250, Accept header application/vnd.c2logbook.v1+json. Source for the claim: https://clawhub.ai/katla50/concept2 . Verify against the official doc page before use.

### Inferences
- For PM5 logging, two routes exist: live BLE (for live metrics on screen) and post-workout Logbook pull (for authoritative totals and stroke data). A reasonable design is live BLE during the session, then the Logbook for reconciliation if the user has an account.
- The PM5 likely reports Erg metrics (distance, pace, stroke rate, calories, heart rate if a strap is paired), but the field list was NOT verified. Read the PM5 interface PDF before designing the screen.

### Gaps
- PM5 BLE service and characteristic UUIDs, field byte layout, and update rate: NOT verified. Requires the Concept2 PDF (not opened; host reachability not tested).
- Whether the Logbook API requires approval for a read-only personal app: NOT verified.

---

## 4. Heart-rate straps, armbands, watches (BLE Heart Rate Profile, Health Connect)

### Takeaway
Health Connect supports heart rate as a standard data type with its own read and write permissions, and workouts are commonly written as an exercise session with heart rate attached. The BLE Heart Rate Profile route (straps and armbands) was NOT researched in this session; it is listed as a gap.

### Cited Findings
- Health Connect covers heart rate as a vital type. Source: https://developer.android.com/health-connect and https://android-developers.googleblog.com/2022/05/introducing-health-connect.html
- Heart rate permissions: android.permission.health.READ_HEART_RATE and android.permission.health.WRITE_HEART_RATE. Data is stored as HeartRateRecord. Source: search snippet from https://developer.android.com/health-connect (permission names quoted from the snippet; not fetched; verify against current docs).
- Heart rate is commonly written alongside exercise sessions (ExerciseSessionRecord). Source: https://developer.android.com/health-and-fitness/health-connect/experiences/workouts (snippet only; not fetched).
- Health Connect supports Android SDK 28 and higher. Jetpack library 1.1.0 is stable; 1.2.0-alpha02 is a pre-release. Source: https://developer.android.com/jetpack/androidx/releases/health-connect (snippet).

### Inferences
- Using Health Connect as the single watch/strap ingestion path would cover Wear OS, Galaxy Watch and Fitbit only if those vendors sync to Health Connect. Not verified per vendor.

### Gaps
- BLE Heart Rate Profile (service 0x180D, characteristic 0x2A37) support details, straps and armbands: NOT researched in this session. Unverified background knowledge: the standard HR profile is widely used by chest straps and many armbands. Confirm with the Bluetooth SIG Heart Rate Profile spec before relying on it.
- Which gym machines broadcast HR over BLE: NOT verified. Search returned no evidence.
- Galaxy Watch, Wear OS and Fitbit to Health Connect specifics: NOT verified.

---

## 5. Calorie estimation: machine accuracy and formulas

### Takeaway
Console calorie numbers are an overestimate with high variance, and the best-known validation (one thesis on one treadmill model) found the machine overestimated by 67 to 117 percent. A simple, documented formula (ACSM walking/running for treadmill, Compendium MET values for other machines) is more transparent than console numbers, but its accuracy was not validated in this session. Heart rate or user-entered profile data is a better basis for a personalized estimate.

### Cited Findings
- University of Wisconsin master's thesis: 55 volunteers walked or ran on a Woodway Curve treadmill at 2 to 8 mph, 5 minutes per speed, against a metabolic analyzer. Console calories overestimated by 67 to 117 percent. Single machine, not peer-reviewed multi-model. Source: https://minds.wisc.edu/items/bf175739-501d-4327-91e7-c7004b4474c3
- Consoles typically ask only for gender, age and weight, and ignore fitness level. Source: secondhand commentary at https://marathonhandbook.com/how-accurate-are-treadmill-calories/ and https://www.garagegymreviews.com/are-treadmill-calories-accurate (not validation studies).
- A Fox News piece citing a trainer reports overestimates of 13 percent (treadmill), 12 percent (stair climber), 7 percent (stationary bike). Source: https://www.foxnews.com/health/how-accurate-are-cardio-machines-calorie-counters . The original study was NOT found; treat as unverified.
- Lifefitness support page notes that the Quick Start estimate can vary significantly and that handrail use can distort results: https://support.lifefitness.com/hc/en-us/articles/360036927434-Cybex-Treadmill-Accuracy
- ACSM walking: VO2 = 0.1 x speed(m/min) + 1.8 x speed x grade + 3.5 ml/kg/min. Running: VO2 = 0.2 x speed + 0.9 x speed x grade + 3.5. Imperial variants exist. Sources (secondary worksheets, not the ACSM manual): https://edisciplinas.usp.br/mod/resource/view.php?id=5684487 , https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/10987006 , https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/12721533 , https://www.unm.edu/%7errobergs/478Steady%20State%20VO2%20Prediction%20Equations.doc
- ACSM walking equation is meant for roughly 1.9 to 4 mph; running applies above 5.0 mph (or 3.0 mph for jogging). Same sources as above.
- Caveat: ACSM equations were developed on a small group of adult men of average height (critic claim in a patent document), and a 2024 Frontiers paper notes walking and running equations give inconsistent values at 8 km/h on flat ground. Sources: https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/11857143 , https://frontiersin.org/journals/sports-and-active-living/articles/10.3389/fspor.2024.1522214/pdf
- Compendium of Physical Activities (2024 adult edition) MET values from search snippets: stationary cycling general 6.8, 151-199 W 10.3, over 325 W 16.3; rowing stationary 150-199 W vigorous 11.0, 200 W+ very vigorous 14.0; stair treadmill ergometer 9.3. The 2011 edition gives stationary bicycling 7.0, rowing vigorous 6.0, stair treadmill ergometer 9.0. Sources: https://pacompendium.com/wp-content/uploads/2024/01/2024-adult-compendium_1_2024.pdf and https://fitmum.ku.dk/2011_Compendium_of_Physical_Activities.pdf (snippet values; not opened). The Compendium states it was not designed to measure precise energy cost.
- Older Adult Compendium stair climbing: 4.0 (slow) and 6.5 (fast). Source: https://pacompendium.com/older-adult-compendium/ (snippet). Do not use for general adults.

### Inferences
- Use MET-based energy: kcal = MET x weight(kg) x hours, with edition and value documented per machine. Use watt-based or speed/grade-based refinement where the machine provides it.
- Treat all machine calorie numbers as a display value, and let the user choose "machine" vs "estimate" in the stats.
- Prefer HR-based estimates when a strap is present, but no validated HR-to-calorie equation was retrieved in this session.

### Gaps
- No validation study was found for stair climber, step mill, rower, elliptical, ski erg, air bike, or spin bike calorie accuracy. Fox News figures are unverified.
- ACSM equations for stepping and cycling: NOT retrieved (only walking and running). The step-mill and stair-climber ACSM equations were NOT verified.
- Heart-rate-based calorie equations (Keytel et al. and similar): NOT researched. Do not use without a source.

---

## 6. Reading a console from a photo with on-device OCR

### Takeaway
Google ML Kit's on-device text recognition is available on Android (API 21+) and works offline, which fits a photo-capture flow. Accuracy depends on image quality. Existing apps doing console OCR were NOT found in this session.

### Cited Findings
- ML Kit Text Recognition runs on-device on Android API 21 or higher and works offline. Input quality (resolution, focus) strongly affects accuracy. Source: https://developers.google.com/ml-kit/vision/text-recognition/android
- Two Android dependency routes: unbundled com.google.mlkit:text-recognition and Play services com.google.android.gms:play-services-mlkit-text-recognition. Script packs (Chinese, Japanese, Korean, Devanagari) are separate. Source: same page (snippet).
- Firebase comparison: on-device suits real-time camera use; cloud is for high-accuracy dense text. Source: https://firebase.google.com/docs/ml-kit/recognize-text (snippet).
- Some ML Kit features (for example Text Recognition v2) were labeled beta on at least one Google page. Verify current status. Source: https://developers.google.com/ml-kit/guides?authuser=0 (snippet).
- CameraX + ML Kit live-text codelab: https://codelabs.developers.google.com/codelabs/mlkit-android-translate

### Inferences
- Console displays are 7-segment or dot-matrix LED/LCD. ML Kit is trained on general text, so accuracy on seven-segment digits is likely weaker and needs testing. This is an inference, not verified. A user-confirm step (show the parsed value, let the user correct it) is essential.

### Gaps
- Benchmarks of ML Kit on LED/7-segment gym console digits: NOT found.
- Existing consumer apps that read gym consoles by camera: NOT found. Not searched further due to call budget.

---

## 7. Minimum manual-entry fields per machine (for useful stats)

### Takeaway
No source found in this session defines per-machine manual-entry minimums. The list below is a proposal grounded in the calorie findings above. It is not verified against sources and should be checked against user testing.

### Proposed (unverified, inference from findings in sections 1 to 5)
- Treadmill: duration, distance, average speed, incline (or grade). Calories are estimated from ACSM and user weight. Optional: average HR.
- Stair climber / step mill: duration, floors or steps (or distance), average speed or level. Calorie estimate from Compendium stair-treadmill MET (9.3 in 2024 edition) and user weight.
- Rower (PM5 or other): duration, distance, average split, stroke rate, calories from console. Compendium rowing MET by wattage if the console does not provide calories.
- Stationary or spin bike: duration, distance, resistance or watts. Calories from watts if available; otherwise Compendium stationary cycling MET by effort.
- Air bike: duration, calories (from console), average RPM or watts if the console gives them. No calorie formula validated.
- Elliptical (cross trainer): duration, distance, resistance, incline. Calories by console or MET (not verified for elliptical).
- Ski erg: duration, distance, split, stroke rate. Calories from console. No MET source checked.
- Incline trainer: duration, incline, speed, distance, calories from console. Calorie method not verified.
- Optional for all: average heart rate, RPE (1 to 10), notes.

### Gaps
- Per-machine MET values for elliptical, air bike, ski erg, incline trainer: NOT retrieved.

---

## Consolidated gaps and next steps

1. Fetch the official FTMS v1.0.1 PDF (https://files.bluetooth.com/download/ftms_v1-0-1) and the FTMS Test Suite PDF from an allowed network. Needed for treadmill, cross trainer, step/stair climber, rower, indoor bike parsers. Current host www.bluetooth.com does not resolve from this session.
2. Open the Concept2 PM5 Bluetooth Smart Interface Definition PDF (linked from https://www.trainerroad.com/forum/t/concept2-bikerg-connection/17004/21?page=2 ). Needed for UUIDs and field layout.
3. Read the official Logbook API doc (https://log.concept2.com/developers/documentation) before designing any sync.
4. Check flutter_blue_plus GitHub issues for Android reliability reports, and test a foreground-service session on a real Android 12+ device.
5. Retrieve the BLE Heart Rate Profile spec and test chest strap and armband pairing.
6. Test ML Kit on real console photos (LED, LCD, 7-segment). Search for existing consumer apps doing this.
7. Find ACSM stepping and cycling equations and any validation studies for elliptical, stair climber, rower calories.
8. Confirm which gym brands (StairMaster, Technogym, Precor, Keiser, Peloton, Echelon) support FTMS or BLE HR, from current product docs.

## Memory note
No memory content was used in this research. No facts in this file came from the user's memory store.
