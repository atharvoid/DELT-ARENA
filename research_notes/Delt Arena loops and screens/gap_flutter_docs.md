# Flutter facts behind the Delt Arena plan

Checked against api.flutter.dev, docs.flutter.dev and pub.dev. The Flutter docs footers show Flutter 3.50.1 as the current stable release. Each row below is a claim from the plan, what the page says, and the page that says it.

| Claim | Verified result | URL |
|---|---|---|
| Semantics widget exposes liveRegion, sortKey, customSemanticsActions, onTap, onLongPress, excludeSemantics, container and explicitChildNodes | Confirmed as parameters. Behaviour of sortKey was not read. | https://api.flutter.dev/flutter/widgets/Semantics-class.html |
| MergeSemantics merges a subtree into one semantics node | Confirmed. The page warns that conflicting child semantics, such as a checked and an unchecked checkbox, produce a misleading merged result. | https://api.flutter.dev/flutter/widgets/MergeSemantics-class.html |
| ExcludeSemantics drops the semantics of descendants when excluding is true | Confirmed. The page describes it for decorative content. | https://api.flutter.dev/flutter/widgets/ExcludeSemantics-class.html |
| CustomSemanticsAction has a label and a hint, and maps to a custom action | Confirmed for label and hint. The page says Android shows these in the local context menu. It does not name TalkBack. | https://api.flutter.dev/flutter/semantics/CustomSemanticsAction-class.html |
| MediaQueryData.disableAnimations is the reduced-animation flag | Confirmed. It corresponds to Android's Remove animations setting, is read from the engine, and drives AnimationController. A MediaQuery override does not change framework animations. | https://api.flutter.dev/flutter/widgets/MediaQueryData/disableAnimations.html |
| MediaQueryData.accessibleNavigation is true when a screen reader is in use | Confirmed. The page says it is true when TalkBack or VoiceOver is in use. | https://api.flutter.dev/flutter/widgets/MediaQueryData-class.html |
| textScaler is the text scaling property, replacing the deprecated textScaleFactor | Confirmed. TextScaler.clamp limits scaling to a minimum and maximum factor. Layout behaviour at 200 percent was not read. | https://api.flutter.dev/flutter/painting/TextScaler-class.html |
| HapticFeedback has lightImpact, mediumImpact, heavyImpact, selectionClick and vibrate, plus success, warning and error notifications | Confirmed. vibrate takes no duration or pattern argument. The Android primitive behind each method is not on this page. | https://api.flutter.dev/flutter/services/HapticFeedback-class.html |
| kLongPressTimeout | 500 milliseconds. | https://api.flutter.dev/flutter/gestures/kLongPressTimeout-constant.html |
| Long press recognition and gesture arena | A long press must stay within its start position for 500 milliseconds by default. The recognizer takes a duration parameter. It competes in the gesture arena only when at least one callback is set. | https://api.flutter.dev/flutter/gestures/LongPressGestureRecognizer-class.html |
| SpringDescription and spring simulation | SpringDescription has mass, stiffness and damping constructors, plus withDampingRatio and withDurationAndBounce (default 500 milliseconds). SpringSimulation is in the physics library. | https://api.flutter.dev/flutter/physics/SpringDescription-class.html |
| Platform channels | Channel names need a unique domain prefix. invokeMethod must run on the platform main thread. The docs recommend Pigeon for new projects. | https://docs.flutter.dev/platform-integration/platform-channels |
| Pigeon 30.0.4 | Generates Kotlin and Java for Android. Uses @HostApi and @FlutterApi annotations. @async gives coroutine-style Kotlin methods. Native interop for Android and iOS is in preview. | https://pub.dev/packages/pigeon |
| speech_to_text 7.5.0 | Targets commands and short phrases, not continuous dictation. Android needs RECORD_AUDIO, INTERNET and Bluetooth permissions. The page says INTERNET is needed because recognition may use remote services. Android has a short pause timeout that cannot be changed, a start and stop beep that cannot be disabled, and no recording while recognition runs. Version 5.2.0 and later need compileSdk 31. On-device support is not stated. A user-reported fix installs offline recognition in Google settings. | https://pub.dev/packages/speech_to_text |
| health 14.0.0 | Needs Flutter 3.44 or later and Dart 3.12 or later. Android minimum API 26. Build needs compileSdk 37 and AGP 9.1.0 or later. MainActivity must extend FlutterFragmentActivity. Each data type needs READ and WRITE permissions in the manifest. Reading history older than 30 days needs READ_HEALTH_DATA_HISTORY. Android 13 and lower need the separate Health Connect app. On iOS a denied read returns only the app's own data, with no error. | https://pub.dev/packages/health |
| Accessibility checklist | Tap targets at least 48 by 48 pixels. Contrast at least 4.5 to 1. Test with TalkBack and VoiceOver. Test colour vision deficiency and large scale factors. | https://docs.flutter.dev/ui/accessibility |
| Large screens | Column count should follow window size through MediaQuery, not device type. Use GridView with a SliverGridDelegate. Switch between BottomNavigationBar and NavigationRail by space. Use the Display API for physical size when letterboxing occurs on folding devices. | https://docs.flutter.dev/ui/adaptive-responsive/large-screens |
| Edge-to-edge on Android 15 and 16 | Apps targeting Android 15 (SDK 35) or later display edge-to-edge by default. Android 16 removes the opt-out. Opting out on Android 15 uses windowOptOutEdgeToEdgeEnforcement in a version-specific style. Flutter 3.27 and later target Android 15 by default. | https://docs.flutter.dev/release/breaking-changes/default-systemuimode-edge-to-edge |

## Corrections to the plan

Haptics. The plan says Stamp is a firm pulse and Bell is a double pulse. HapticFeedback has no pattern or duration argument, so a double pulse cannot be requested through it and needs a native call. Detent maps naturally to selectionClick. Stamp maps to mediumImpact or heavyImpact, and the choice belongs in the token layer. The plan left these constants open, and Flutter's API now answers that part.

Press and hold. The plan uses about 400 milliseconds. Flutter's default long press is 500 milliseconds. A 400 millisecond threshold needs an explicit duration on a LongPressGestureRecognizer, which the plan should state.

Reduced motion. The plan said the Flutter API was not verified. It is now: MediaQueryData.disableAnimations, and AnimationController honours it. The plan should read the flag through the engine value, since MediaQuery overrides do not reach framework animations.

Custom actions. The plan says CustomSemanticsAction maps to TalkBack custom actions. The Flutter page supports only the local context menu wording. The TalkBack mapping is still unverified.

Live Update bridge. The plan assumes a hand-written platform channel. Flutter now recommends Pigeon for new projects, and Pigeon generates typed Kotlin. The plan should specify Pigeon.

Edge-to-edge. The plan says the change is enforced from Android 15. Flutter's page adds that Android 16 removes the opt-out, so the insets work is mandatory on those devices.

Health. The plan's version and SDK requirements match the page. Missing from the plan: the FlutterFragmentActivity requirement, the per-type manifest permissions, the history permission for reads, and the iOS behaviour where a denied read looks like empty data.

Speech. The plan's claim of an Android 12 on-device recognizer is not on this page, and the speech_to_text page does not confirm on-device recognition. The short Android pause timeout the plan assumes is confirmed.

## Still not reached

The 200 percent text scale layout behaviour under textScaler.
How onTap and onLongPress interact on a standard GestureDetector. Only the long press recognizer was read.
The Android primitive behind each HapticFeedback method.
How TalkBack presents Flutter custom semantics actions beyond the context menu wording.
The sortKey ordering rules.
SpringSimulation method signatures and curve choices.
Health batch write limits, the rateLimitExceeded handling, and the 15-minute write guidance, which sit further down the health page.
On-device speech recognition on Android. The Android 12 on-device recognizer claim is an Android platform question, not a Flutter one.
The Live Update, Foreground service and Wear OS parts of the plan, which belong to Android documentation.
Mouse and stylus input guidance on the user input page.
