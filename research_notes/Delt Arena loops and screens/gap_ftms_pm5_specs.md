# Gap research: FTMS, Heart Rate, and Concept2 PM5 byte-level specs

Date of research: 2026-11-26. Read-only. No spec files were saved by this research.

## Source status

The primary PDFs could not be read with the tools available. The Bluetooth SIG pages were reachable, but the PDFs are binary and the text extraction returned only PDF object syntax. The Concept2 PM5 Bluetooth Smart Interface Definition was not found at its expected URL and was not readable in any form.

The tables below therefore come from two secondary sources:

1. The Bluetooth SIG GATT XML characteristic definitions, mirrored in the oesmith/gatt-xml repo. These are the SIG-derived machine-readable definitions. The text was read through a summarising fetch, so verify each field against the raw XML before coding.
2. The ronanb96/bluetooth-sig-python library, which is generated from the SIG YAML and contains the FTMS enum values.

Any row without a clear primary source is marked uncertain.

Files that the WebFetch tool saved automatically into the session tool-results folder while attempting PDF extraction (not intentional downloads, nothing written to the project):
C:\Users\SLAT\.claude\projects\C--Users-SLAT-Documents-Projects-DELT-DELT-ARENA\f424424c-08cd-4719-8f97-54cc8138119f\tool-results\webfetch-1795641437729-wz2ecd.pdf (FTMS spec, 1.3 MB)
C:\Users\SLAT\.claude\projects\C--Users-SLAT-Documents-Projects-DELT-DELT-ARENA\f424424c-08cd-4719-8f97-54cc8138119f\tool-results\webfetch-1795641534817-s93mq4.pdf (Concept2 CSAFE definition, 2.4 MB)

## 1. Fitness Machine Service (FTMS)

### Service and characteristic UUIDs

| Item | UUID | Source |
|---|---|---|
| Fitness Machine service | 0x1826 | https://raw.githubusercontent.com/NordicSemiconductor/bluetooth-numbers-database/master/v1/service_uuids.json (also https://www.bluetooth.com/specifications/specs/fitness-machine-service-1-0/ lists the service as Adopted, with Errata 23224 mandatory) |
| Fitness Machine Feature | 0x2ACC | https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.fitness_machine_feature.xml |
| Treadmill Data | 0x2ACD | https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.treadmill_data.xml |
| Cross Trainer Data | 0x2ACE | https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.cross_trainer_data.xml |
| Step Climber Data | 0x2ACF | https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.step_climber_data.xml |
| Stair Climber Data | 0x2AD0 | https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.stair_climber_data.xml |
| Rower Data | 0x2AD1 | https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.rower_data.xml |
| Indoor Bike Data | 0x2AD2 | https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.indoor_bike_data.xml |
| Training Status | 0x2AD3 | https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.training_status.xml |
| Fitness Machine Control Point | 0x2AD9 | https://raw.githubusercontent.com/ronanb96/bluetooth-sig-python/main/src/bluetooth_sig/gatt/characteristics/fitness_machine_control_point.py |
| Fitness Machine Status | 0x2ADA | https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.fitness_machine_status.xml |

Supported range characteristics (0x2AD4 to 0x2AD8) were not reached. The values are not confirmed here.

### Fitness Machine Feature (0x2ACC), 8 bytes, two uint32 little-endian

Offset 0 is Fitness Machine Features. Offset 4 is Target Setting Features. Source: https://raw.githubusercontent.com/ronanb96/bluetooth-sig-python/main/src/bluetooth_sig/gatt/characteristics/fitness_machine_feature.py (secondary, generated from SIG YAML).

| Bit (value) | Fitness Machine Features (offset 0) |
|---|---|
| 0 (0x0001) | Average Speed supported |
| 1 (0x0002) | Cadence supported |
| 2 (0x0004) | Total Distance supported |
| 3 (0x0008) | Inclination supported |
| 4 (0x0010) | Elevation Gain supported |
| 5 (0x0020) | Pace supported |
| 6 (0x0040) | Step Count supported |
| 7 (0x0080) | Resistance Level supported |
| 8 (0x0100) | Stride Count supported |
| 9 (0x0200) | Expended Energy supported |
| 10 (0x0400) | Heart Rate Measurement supported |
| 11 (0x0800) | Metabolic Equivalent supported |
| 12 (0x1000) | Elapsed Time supported |
| 13 (0x2000) | Remaining Time supported |
| 14 (0x4000) | Power Measurement supported |
| 15 (0x8000) | Force on Belt and Power Output supported |
| 16 (0x10000) | User Data Retention supported |

| Bit (value) | Target Setting Features (offset 4) |
|---|---|
| 0 (0x0001) | Speed target setting |
| 1 (0x0002) | Inclination target setting |
| 2 (0x0004) | Resistance target setting |
| 3 (0x0008) | Power target setting |
| 4 (0x0010) | Heart rate target setting |
| 5 (0x0020) | Targeted expended energy |
| 6 (0x0040) | Targeted steps |
| 7 (0x0080) | Targeted strides |
| 8 (0x0100) | Targeted distance |
| 9 (0x0200) | Targeted training time |
| 10 (0x0400) | Targeted time in two HR zones |
| 11 (0x0800) | Targeted time in three HR zones |
| 12 (0x1000) | Targeted time in five HR zones |
| 13 (0x2000) | Indoor bike simulation parameters |

### Treadmill Data (0x2ACD)

Source: https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.treadmill_data.xml

Flags are 16-bit. Bit 0 "More Data" is inverted: 0 means Instantaneous Speed is present.

| Bit | Field present when set |
|---|---|
| 0 | More Data (0 = Instantaneous Speed present) |
| 1 | Average Speed |
| 2 | Total Distance |
| 3 | Inclination and Ramp Angle Setting |
| 4 | Elevation Gain |
| 5 | Instantaneous Pace |
| 6 | Average Pace |
| 7 | Expended Energy |
| 8 | Heart Rate |
| 9 | Metabolic Equivalent |
| 10 | Elapsed Time |
| 11 | Remaining Time |
| 12 | Force on Belt and Power Output |
| 13 to 15 | Reserved |

Field order after flags (little-endian):

| Field | Type | Unit and resolution |
|---|---|---|
| Instantaneous Speed | uint16 | km/h, 0.01 |
| Average Speed | uint16 | km/h, 0.01 |
| Total Distance | uint24 | metres, 1 |
| Inclination | sint16 | percent, 0.1 |
| Ramp Angle Setting | sint16 | degrees, 0.1 |
| Positive Elevation Gain | uint16 | metres, 0.1 |
| Negative Elevation Gain | uint16 | metres, 0.1 |
| Instantaneous Pace | uint8 | km/min, 0.1 |
| Average Pace | uint8 | km/min, 0.1 |
| Total Energy | uint16 | kcal, 1 |
| Energy Per Hour | uint16 | kcal, 1 |
| Energy Per Minute | uint8 | kcal, 1 |
| Heart Rate | uint8 | bpm, 1 |
| Metabolic Equivalent | uint8 | MET, 0.1 |
| Elapsed Time | uint16 | seconds |
| Remaining Time | uint16 | seconds |
| Force on Belt | sint16 | newtons, 1 |
| Power Output | sint16 | watts, 1 |

Caution: the Force on Belt and Power Output field pair is described under one flag in the XML, so the pair is sent together.

### Cross Trainer Data (0x2ACE)

Source: https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.cross_trainer_data.xml

Flags are 24-bit.

| Bit | Field present when set |
|---|---|
| 0 | More Data (0 = Instantaneous Speed present) |
| 1 | Average Speed |
| 2 | Total Distance |
| 3 | Step Count (Step Per Minute and Average Step Rate) |
| 4 | Stride Count |
| 5 | Elevation Gain (positive and negative) |
| 6 | Inclination and Ramp Angle Setting |
| 7 | Resistance Level |
| 8 | Instantaneous Power |
| 9 | Average Power |
| 10 | Expended Energy |
| 11 | Heart Rate |
| 12 | Metabolic Equivalent |
| 13 | Elapsed Time |
| 14 | Remaining Time |
| 15 | Movement Direction (0 = forward, 1 = backward) |
| 16 to 23 | Reserved |

Field order after flags (little-endian):

| Field | Type | Unit and resolution |
|---|---|---|
| Instantaneous Speed | uint16 | km/h, 0.01 |
| Average Speed | uint16 | km/h, 0.01 |
| Total Distance | uint24 | metres |
| Step Per Minute | uint16 | steps/min |
| Average Step Rate | uint16 | steps/min |
| Stride Count | uint16 | 0.1 |
| Positive Elevation Gain | uint16 | metres |
| Negative Elevation Gain | uint16 | metres |
| Inclination | sint16 | percent, 0.1 |
| Ramp Angle Setting | sint16 | degrees, 0.1 |
| Resistance Level | sint16 | 0.1 |
| Instantaneous Power | sint16 | watts |
| Average Power | sint16 | watts |
| Total Energy | uint16 | kcal |
| Energy Per Hour | uint16 | kcal |
| Energy Per Minute | uint8 | kcal |
| Heart Rate | uint8 | bpm |
| Metabolic Equivalent | uint8 | MET, 0.1 |
| Elapsed Time | uint16 | seconds |
| Remaining Time | uint16 | seconds |

### Step Climber Data (0x2ACF)

Source: https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.step_climber_data.xml

Flags are 16-bit. Bits 9 to 15 are reserved.

| Bit | Field present when set |
|---|---|
| 0 | More Data (0 = Floors and Step Count present) |
| 1 | Step Per Minute |
| 2 | Average Step Rate |
| 3 | Positive Elevation Gain |
| 4 | Expended Energy |
| 5 | Heart Rate |
| 6 | Metabolic Equivalent |
| 7 | Elapsed Time |
| 8 | Remaining Time |

Field order after flags (little-endian): Floors uint16, Step Count uint16, Step Per Minute uint16, Average Step Rate uint16, Positive Elevation Gain uint16 (m), Total Energy uint16 (kcal), Energy Per Hour uint16 (kcal), Energy Per Minute uint8 (kcal), Heart Rate uint8 (bpm), Metabolic Equivalent uint8 (0.1 MET), Elapsed Time uint16 (s), Remaining Time uint16 (s).

Uncertain: the XML marks Floors and Step Count under the same condition (C1). The fetch summary may have mislabelled the Floors/Step Count condition. Verify against the raw XML.

### Stair Climber Data (0x2AD0)

Source: https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.stair_climber_data.xml

Flags are 16-bit. Bits 10 to 15 are reserved.

| Bit | Field present when set |
|---|---|
| 0 | More Data (0 = Floors present) |
| 1 | Step Per Minute |
| 2 | Average Step Rate |
| 3 | Positive Elevation Gain |
| 4 | Stride Count |
| 5 | Expended Energy |
| 6 | Heart Rate |
| 7 | Metabolic Equivalent |
| 8 | Elapsed Time |
| 9 | Remaining Time |

Field order after flags (little-endian): Floors uint16, Step Per Minute uint16, Average Step Rate uint16, Positive Elevation Gain uint16 (m), Stride Count uint16, Total Energy uint16 (kcal), Energy Per Hour uint16 (kcal), Energy Per Minute uint8 (kcal), Heart Rate uint8 (bpm), Metabolic Equivalent uint8 (0.1 MET), Elapsed Time uint16 (s), Remaining Time uint16 (s).

Note: the Stair Climber and Step Climber flag tables differ at bit 4 (Stride Count versus Expended Energy). Both come from the same secondary source; verify against the SIG FTMS spec before coding either.

### Rower Data (0x2AD1)

Source: https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.rower_data.xml. The XML date is 2017-02-14 and the summary marks it as not approved, so treat with care.

Flags are 16-bit. Bits 13 to 15 are reserved.

| Bit | Field present when set |
|---|---|
| 0 | More Data (0 = Stroke Rate and Stroke Count present) |
| 1 | Average Stroke Rate |
| 2 | Total Distance |
| 3 | Instantaneous Pace |
| 4 | Average Pace |
| 5 | Instantaneous Power |
| 6 | Average Power |
| 7 | Resistance Level |
| 8 | Expended Energy |
| 9 | Heart Rate |
| 10 | Metabolic Equivalent |
| 11 | Elapsed Time |
| 12 | Remaining Time |

Field order after flags (little-endian): Stroke Rate uint8 (0.5 strokes/min), Stroke Count uint16, Average Stroke Rate uint8 (0.5), Total Distance uint24 (m), Instantaneous Pace uint16 (s), Average Pace uint16 (s), Instantaneous Power sint16 (W), Average Power sint16 (W), Resistance Level sint16, Total Energy uint16 (kcal), Energy Per Hour uint16 (kcal), Energy Per Minute uint8 (kcal), Heart Rate uint8 (bpm), Metabolic Equivalent uint8 (0.1 MET), Elapsed Time uint16 (s), Remaining Time uint16 (s).

### Indoor Bike Data (0x2AD2)

Source: https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.indoor_bike_data.xml

Flags are 16-bit. Bits 13 to 15 are reserved. Bit 0 is inverted: 0 means Instantaneous Speed present.

| Bit | Field present when set |
|---|---|
| 0 | More Data (0 = Instantaneous Speed present) |
| 1 | Instantaneous Cadence |
| 2 | Average Speed |
| 3 | Average Cadence |
| 4 | Total Distance |
| 5 | Resistance Level |
| 6 | Instantaneous Power |
| 7 | Average Power |
| 8 | Expended Energy |
| 9 | Heart Rate |
| 10 | Metabolic Equivalent |
| 11 | Elapsed Time |
| 12 | Remaining Time |

Field order after flags (little-endian): Instantaneous Speed uint16 (km/h, 0.01), Instantaneous Cadence uint16 (rpm, 0.5), Average Speed uint16 (km/h, 0.01), Average Cadence uint16 (rpm, 0.5), Total Distance uint24 (m), Resistance Level sint16 (unitless), Instantaneous Power sint16 (W), Average Power sint16 (W), Total Energy uint16 (kcal), Energy Per Hour uint16 (kcal), Energy Per Minute uint8 (kcal), Heart Rate uint8 (bpm), Metabolic Equivalent uint8 (0.1 MET), Elapsed Time uint16 (s), Remaining Time uint16 (s).

Uncertain: Resistance Level is typed sint16 in this XML summary. Some implementations treat it as uint8. Verify against the SIG FTMS spec.

### Training Status (0x2AD3)

Source: https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.training_status.xml. Layout not reached. The XML page only defers to the FTMS spec.

### Fitness Machine Status (0x2ADA)

Source: https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.fitness_machine_status.xml. Opcode and value table not reached. Unverified from memory: 0x01 reset, 0x02 stopped or paused by user, 0x03 stopped by safety key, 0x04 started or resumed. Do not code from this without the spec.

### Control Point (0x2AD9) opcodes

Source: https://raw.githubusercontent.com/ronanb96/bluetooth-sig-python/main/src/bluetooth_sig/gatt/characteristics/fitness_machine_control_point.py (secondary, generated from SIG YAML).

| Opcode | Name |
|---|---|
| 0x00 | Request Control |
| 0x01 | Reset |
| 0x02 | Set Target Speed |
| 0x03 | Set Target Inclination |
| 0x04 | Set Target Resistance Level |
| 0x05 | Set Target Power |
| 0x06 | Set Target Heart Rate |
| 0x07 | Start or Resume |
| 0x08 | Stop or Pause |
| 0x09 | Set Targeted Expended Energy |
| 0x0A | Set Targeted Number of Steps |
| 0x0B | Set Targeted Number of Strides |
| 0x0C | Set Targeted Distance |
| 0x0D | Set Targeted Training Time |
| 0x0E | Set Targeted Time in Two HR Zones |
| 0x0F | Set Targeted Time in Three HR Zones |
| 0x10 | Set Targeted Time in Five HR Zones |
| 0x11 | Set Indoor Bike Simulation Parameters |
| 0x12 | Set Wheel Circumference |
| 0x13 | Spin Down Control |
| 0x14 | Set Targeted Cadence |
| 0x80 | Response Code (opcode, request opcode, result) |

Response result codes: 0x01 Success, 0x02 Op Code Not Supported, 0x03 Invalid Parameter, 0x04 Operation Failed, 0x05 Control Not Permitted.

Uncertain: values from a library enum. Confirm the 0x00 to 0x14 list and result codes against the SIG FTMS spec, section on Control Point, before implementing commands.

## 2. Heart Rate Service and Heart Rate Measurement (0x2A37)

Service UUID 0x180D (https://raw.githubusercontent.com/NordicSemiconductor/bluetooth-numbers-database/master/v1/service_uuids.json). Characteristic UUID 0x2A37 (https://raw.githubusercontent.com/oesmith/gatt-xml/master/org.bluetooth.characteristic.heart_rate_measurement.xml).

Flags are 8-bit.

| Bit | Meaning |
|---|---|
| 0 | Heart Rate Value Format: 0 = uint8 bpm, 1 = uint16 bpm |
| 1 to 2 | Sensor Contact Status: 0 or 1 = unsupported, 2 = supported with no contact, 3 = supported with contact |
| 3 | Energy Expended present (1 = present) |
| 4 | RR-Interval present (1 = present) |
| 5 to 7 | Reserved |

Field order (little-endian): Flags uint8, Heart Rate Value (uint8 or uint16 per bit 0), Energy Expended uint16 (present if bit 3), RR-Interval uint16 values (present if bit 4, 1/1024 s each, oldest first).

Uncertain: the XML labels Energy Expended as joule while the description says kilojoules. Treat the unit as unresolved until checked against the Heart Rate Service spec. Also the Heart Rate Service spec itself was not reached.

## 3. Concept2 PM5 Bluetooth Smart

### Official spec status

The PM5 Bluetooth Smart Interface Definition PDF was not reachable. The Concept2 software development page (https://www.concept2.com/support/software-development) links only to a "PM CSAFE Communication Definition" PDF (https://cms.concept2.com/sites/default/files/2026-03/Concept2%20PM%20CSAFE%20Communication%20Definition.pdf), which is a 173-page PDF that could not be read. That page also says the spec "is subject to change without notice". The c2bluetooth README cites the Bluetooth Smart spec as rev 1.27, which is secondary and may be outdated.

### UUIDs

Source for all rows: https://raw.githubusercontent.com/OpenRowingCommunity/c2bluetooth/main/lib/constants.dart (secondary, Flutter code).

| Name in constants | UUID | Short | Notes |
|---|---|---|---|
| C2_ROWING_BASE_UUID | CE060000-43E5-11E4-916C-0800200C9A66 | base | |
| C2_DEVICE_INFO_SERVICE_UUID | CE060010-43E5-11E4-916C-0800200C9A66 | 0x0010 | |
| C2_ROWING_CONTROL_SERVICE_UUID | CE060020-43E5-11E4-916C-0800200C9A66 | 0x0020 | Control service |
| PM receive | CE060021-43E5-11E4-916C-0800200C9A66 | 0x0021 | CSAFE commands written here (per forum) |
| PM transmit | CE060022-43E5-11E4-916C-0800200C9A66 | 0x0022 | |
| C2_ROWING_PRIMARY_SERVICE_UUID | CE060030-43E5-11E4-916C-0800200C9A66 | 0x0030 | Rowing service |
| General Status | CE060031-43E5-11E4-916C-0800200C9A66 | 0x0031 | Named General Status in forum post |
| General Status 2 | CE060032-43E5-11E4-916C-0800200C9A66 | 0x0032 | Forum calls 0x0032 and 0x0033 "General" |
| Split/Interval data | CE060037-43E5-11E4-916C-0800200C9A66 | 0x0037 | Forum says updates after each stroke or interval |
| Split/Interval data 2 | CE060038-43E5-11E4-916C-0800200C9A66 | 0x0038 | Forum names 0x0038 "Interval" |
| End of workout summary | CE060039-43E5-11E4-916C-0800200C9A66 | 0x0039 | |
| End of workout summary 2 | CE06003A-43E5-11E4-916C-0800200C9A66 | 0x003A | |

Source for the forum mapping, which conflicts in places with the constants: https://c2forum.com/viewtopic.php?p=297951 (community post and replies, not the spec). The forum lists 0x0033 (general), 0x0034 (sets the sample rate for 0x0031 to 0x0033), 0x0035 (updates after each stroke or interval), 0x0036 (Stroke), and 0x0038 (Interval). The constants file does not define 0x0033, 0x0034, 0x0035, or 0x0036.

Additional status and additional status 2 characteristics: not identified with confidence. The forum post also mentions 0x0021 as the CSAFE write target.

### Update rates

General status (0x0031 to 0x0033): notify rate is set by writing to 0x0034, per the forum post. No numeric default was found. Source: https://c2forum.com/viewtopic.php?p=297951 (secondary).

Stroke, interval, and summary: event-driven. Source: forum post above. A reply says the summary may notify a second time about one minute later when a heart rate strap is active, which that poster had not tested.

### Stroke data field layout

Source: https://jiggermast.blogspot.com/2024/06 (third-party packet-sniffing write-up, secondary). The post names the UUID ending 0x0033 as the stroke characteristic, inferred from code, not from the spec. Byte offsets were not given, so the layout below is field and scaling only:

| Field | Size | Scaling |
|---|---|---|
| elapsedTime | uint24 | x10 |
| distance | uint24 | /10 |
| driveLength | uint8 | /100 |
| driveTime | uint8 | x10 |
| strokeRecoveryTime | uint8 LO + HI | (LO + HI x 256) x10 |
| strokeDistance | uint16 | /100 |
| peakDriveForce | uint16 | /10 |
| averageDriveForce | uint16 | /10 |
| workPerStroke | uint16 | /10 |
| strokeCount | uint8 LO + HI | LO + HI x 256 |

Uncertain: the forum says 0x0036 is Stroke, the blog says 0x0033 is stroke data. Resolve against the spec.

### Workout summary field list

Source: https://raw.githubusercontent.com/OpenRowingCommunity/c2bluetooth/main/lib/constants.dart for the characteristic, and https://github.com/OpenRowingCommunity/c2bluetooth (README) for the field list. Field names: timestamp, workTime, workDistance, avgSPM, endHeartRate, avgHeartRate, minHeartRate, maxHeartRate, avgDragFactor, recoveryHeartRate, workoutType, avgPace, intervalType, intervalSize, intervalCount, totalCalories, watts, totalRestDistance, intervalRestTime, avgCalories. Byte layout not reached.

### Concept2 Logbook API (log.concept2.com)

Source: http://log.concept2.com/developers/documentation/ (the https URL redirects to http).

The Logbook is an OAuth2 REST API for stored results, with webhooks, stroke data, and FIT/TCX/CSV exports. It is not a live BLE stream and the docs state no real-time or latency guarantees. Personal read-only use can use a long-lived token from the Logbook profile's Applications settings. Apps that write data must develop on log-dev.concept2.com first and must contact Concept2 for approval before using the live API. Access questions go to ranking@concept2.com. The docs say there is currently no rate limit but abuse may lead to limits.

## 4. Brand and machine FTMS evidence

These are search snippets only. The linked pages were not opened, so treat each row as a lead, not a verified claim.

| Brand | Evidence | Source |
|---|---|---|
| Matrix | Manufacturer marketing says smart treadmill, bike, or elliptical connects to FTMS apps such as Zwift and Kinomap | https://matrixhomefitness.com/pages/never-a-dull-workout |
| Life Fitness | Zwift forum says some Track Connect console treadmills work with Zwift, others (Track Plus, Go console) do not | https://forums.zwift.com/t/zwift-with-pro-from-smart-treadmills/121246.md (dated) |
| Technogym | Forum says MYRUN treadmill works with Zwift. Mywellness integrations page says it can read FTMS machines | https://www.mywellness.com/en-GB/integrations/ |
| Precor | Forum lists a Precor 966i treadmill with Zwift. No manufacturer statement found | https://forums.zwift.com/t/zwift-with-pro-from-smart-treadmills/121246.md |
| Horizon | Help article on connecting to Zwift or Peloton using FTMS | https://help.horizonfitness.com/hc/en-us/articles/47020136016276-How-Do-I-connect-to-Zwift-or-Peloton-Using-Bluetooth-FTMS-or-a-Bluetooth-Heart-Rate-Strap |
| Generic | QDomyos-Zwift supported-devices list | https://www.github.com/cagnulein/qdomyos-zwift/blob/master/docs/20_supported_devices_and_applications.md |
| StairMaster | No evidence found | none |
| Peloton (native hardware) | No FTMS evidence found. Third-party bridge (QZ) reads Peloton app classes for non-Peloton bikes | https://the5krunner.com/2026/05/07/qz-qdomyos-zwift-app/ |
| Wahoo Kickr | Not searched | none |

The dudanov pyftms documentation lists Treadmill, Cross Trainer, Rower, and Indoor Bike as supported machine types and states Step and Stair Climber are not supported: https://dudanov.github.io/python-pyftms/pyftms.html (secondary, library docs)

## Parser notes for Delt Arena

Mapping from the plan's cardio list to FTMS characteristics. Rows marked inferred have no direct spec statement.

| Plan machine | Characteristic | UUID | Notes |
|---|---|---|---|
| Treadmill | Treadmill Data | 0x2ACD | Direct |
| Incline trainer | Treadmill Data (inclination fields) or Cross Trainer Data | 0x2ACD or 0x2ACE | Inferred. Inclination exists in both. Check Fitness Machine Feature bit 3 |
| Stair climber | Stair Climber Data | 0x2AD0 | Direct, but table is secondary |
| Step mill | Step Climber Data | 0x2ACF | Inferred mapping |
| Rower | Rower Data | 0x2AD1 | Direct, but XML marked not approved |
| Bike | Indoor Bike Data | 0x2AD2 | Direct |
| Air bike | none defined | none | No FTMS type found. Treat as unknown. Likely not exposed |
| Elliptical | Cross Trainer Data | 0x2ACE | Direct |
| Ski erg | none defined | none | No FTMS type found. Concept2 SkiErg uses the PM5 BLE interface, not FTMS. Unverified |

Heart rate from any machine: use the 0x180D service (0x2A37) or the Heart Rate bit in the machine data (Treadmill bit 8, Cross Trainer bit 11, Step Climber bit 5, Stair Climber bit 6, Rower bit 9, Indoor Bike bit 9).

Always read the Fitness Machine Feature (0x2ACC) and check the relevant machine bits before subscribing. A machine can expose a data characteristic without every optional field.

## Still not reached

1. Official Bluetooth SIG FTMS 1.0.1 PDF, the byte-level source. Text extraction failed. Not verified against the spec.
2. Supported Speed, Inclination, Resistance, Heart Rate, and Power Range characteristics (0x2AD4 to 0x2AD8) and their byte layouts.
3. Training Status (0x2AD3) value table and string field rule.
4. Fitness Machine Status (0x2ADA) opcode table.
5. Official Heart Rate Service 1.0 PDF, to resolve the Energy Expended unit and bit 3 definition.
6. Concept2 PM5 Bluetooth Smart Interface Definition: general status, additional status, and additional status 2 byte layouts; numeric update rates; split and workout summary byte layouts; spec revision and minimum firmware. The PDF was not reachable.
7. Concept2 stroke-data offsets (the blog gives fields and scaling only).
8. Confirmation of which Concept2 characteristic is stroke (0x0033 vs 0x0036) and which is split (0x0035 vs 0x0037 vs 0x0038).
9. Ski erg and air bike FTMS support (none found).
10. Brand evidence for StairMaster, Peloton native hardware, and Wahoo Kickr. Search snippets only; no manufacturer pages were opened or verified.
11. Real device testing. No hardware was used.
