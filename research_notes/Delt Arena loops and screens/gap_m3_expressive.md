# Material 3 Expressive: spec gap research

Date of research: 2026-11-26. Method: m3.material.io read through the user's browser (Tether), Compose source and docs fetched with WebFetch, pub.dev and the Flutter issue fetched with WebFetch. Where a source was fetched through WebFetch, the numbers came through a summarising model reading the raw file. They match the file's structure but should be checked against the raw file before code is written.

## Motion: springs

Source: [M3 motion specs](https://m3.material.io/styles/motion/overview/specs) and [M3 motion how it works](https://m3.material.io/styles/motion/overview/how-it-works).

The motion system has two schemes, expressive and standard. Each scheme has spatial and effects springs at fast, default and slow speeds. Spatial springs move, resize, rotate or round corners, and they overshoot. Effects springs change colour or opacity and do not overshoot. The spec says fast suits small elements such as switches and buttons, default suits partly covering surfaces such as bottom sheets, and slow suits full-screen animations.

Spring values (stiffness, damping), from the Compose source files:

Source: [ExpressiveMotionTokens.kt](https://raw.githubusercontent.com/androidx/androidx/androidx-main/compose/material3/material3/src/commonMain/kotlin/androidx/compose/material3/tokens/ExpressiveMotionTokens.kt)
- Expressive spatial fast: stiffness 800, damping 0.6
- Expressive spatial default: stiffness 380, damping 0.8
- Expressive spatial slow: stiffness 200, damping 0.8
- Expressive effects fast: stiffness 3800, damping 1.0
- Expressive effects default: stiffness 1600, damping 1.0
- Expressive effects slow: stiffness 800, damping 1.0

Source: [StandardMotionTokens.kt](https://raw.githubusercontent.com/androidx/androidx/androidx-main/compose/material3/material3/src/commonMain/kotlin/androidx/compose/material3/tokens/StandardMotionTokens.kt)
- Standard spatial fast: stiffness 1400, damping 0.9
- Standard spatial default: stiffness 700, damping 0.9
- Standard spatial slow: stiffness 300, damping 0.9
- Standard effects fast, default, slow: stiffness 3800, 1600, 800, damping 1.0

The Compose MotionScheme API names the six specs (fastSpatialSpec, defaultSpatialSpec, slowSpatialSpec and the three effects equivalents) and documents expressive() as the scheme for prominent elements and hero interactions. Source: [MotionScheme reference](https://developer.android.com/reference/kotlin/androidx/compose/material3/MotionScheme). The API was added in Material3 1.5.0. Source: same page.

The Views library (MDC-Android) lists one set of six spring tokens with the standard numbers above, without naming a scheme. Source: [MDC Motion.md](https://raw.githubusercontent.com/material-components/material-components-android/master/docs/theming/Motion.md).

Web conversion, from the spec page. These are cubic-bezier curves with durations, for Web only:
- Expressive fast spatial: 0.42, 1.67, 0.21, 0.90, 350 ms
- Expressive default spatial: 0.38, 1.21, 0.22, 1.00, 500 ms
- Expressive slow spatial: 0.39, 1.29, 0.35, 0.98, 650 ms
- Expressive fast effects: 0.31, 0.94, 0.34, 1.00, 150 ms
- Expressive default effects: 0.34, 0.80, 0.34, 1.00, 200 ms
- Expressive slow effects: 0.34, 0.88, 0.34, 1.00, 300 ms

Source: [M3 motion specs](https://m3.material.io/styles/motion/overview/specs). Flutter has no spring tokens from the spec, so these curves are the only Web-side values.

Component coverage: the spec says 21 Material components use the motion system by default on Compose. Source: [M3 motion how it works](https://m3.material.io/styles/motion/overview/how-it-works).

## Shape

Source: [M3 shape corner radius scale](https://m3.material.io/styles/shape/corner-radius-scale) and [M3 shape overview](https://m3.material.io/styles/shape/overview-principles).

Corner scale, in dp: none 0, extra small 4, small 8, medium 12, large 16, large increased 20, extra large 28, extra large increased 32, extra extra large 48, full (fully rounded). The Compose ShapeTokens file gives the same numbers. Source: [ShapeTokens.kt](https://raw.githubusercontent.com/androidx/androidx/androidx-main/compose/material3/material3/src/commonMain/kotlin/androidx/compose/material3/tokens/ShapeTokens.kt).

Button corners, from the button specs (extra small, small, medium, large, extra large): round button full for all sizes; square button 12, 12, 16, 28, 28; pressed state 8, 8, 12, 16, 16. Source: [M3 buttons specs](https://m3.material.io/components/buttons/specs).

Shape morph: the spec says shapes should morph in response to interaction states, actions in progress and environment changes. It says the morph should respond to tap, swipe, scroll, release and long press. Source: [M3 shape overview](https://m3.material.io/styles/shape/overview-principles).

Pressed buttons morph to square; toggles change resting shape from round to square when selected. Source: [M3 buttons specs](https://m3.material.io/components/buttons/specs).

Inner corners: closely grouped items such as menus and split buttons use asymmetric inner corners. The inner corner space is always 2dp. Source: [M3 corner radius scale](https://m3.material.io/styles/shape/corner-radius-scale) and [M3 split button specs](https://m3.material.io/components/split-button/specs).

Optical roundness: nested rounded objects use radii that differ by the padding, using outer radius minus padding for the inner radius. Source: [M3 corner radius scale](https://m3.material.io/styles/shape/corner-radius-scale).

Warning: the spec advises against large or full corners on information-dense components such as cards. Source: same page.

Shape library: 35 shapes and shape morphing were added in the May 2025 M3 Expressive update. Source: [M3 shape overview](https://m3.material.io/styles/shape/overview-principles).

## Type

Source: [M3 type scale and tokens](https://m3.material.io/styles/typography/type-scale-tokens).

The M3 scale has 15 baseline styles and 15 emphasized styles, from Display Large to Label Small. Emphasized styles have higher weight and minor adjustments. The spec recommends them for selection, actions, headlines and bold text. Material components do not use them by default. Emphasized and baseline should be used together.

Baseline sizes and line heights, from the Compose TypeScaleTokens file: Display Large 57/64; Display Medium 45/52; Display Small 36/44; Headline Large 32/40; Headline Medium 28/36; Headline Small 24/32; Title Large 22/28; Title Medium 16/24; Title Small 14/20; Body Large 16/24; Body Medium 14/20; Body Small 12/16; Label Large 14/20; Label Medium 12/16; Label Small 11/16. Source: [TypeScaleTokens.kt](https://raw.githubusercontent.com/androidx/androidx/androidx-main/compose/material3/material3/src/commonMain/kotlin/androidx/compose/material3/tokens/TypeScaleTokens.kt).

The emphasized sizes in the same file equal the baseline sizes. The file marks them with a TODO to update once generated tokens exist. Emphasized weight is not in the text I could read. Source: same file.

Font sizes are in sp on Android. Letter spacing is in em. Source: [M3 type scale and tokens](https://m3.material.io/styles/typography/type-scale-tokens).

Brand typeface is for large styles and plain typeface for small styles. Roboto is the default for both. Roboto Flex is named as a replacement example. Source: same page.

Language height: medium is recommended as default. Components with fixed heights may not adapt. Source: same page.

Spec advice: avoid changing type sizes of M3 styles, because it affects component reflow. Customising the scale may stop token updates. Source: same page.

## Touch targets and sizes

Source: [M3 button groups specs](https://m3.material.io/components/button-groups/specs).
- Standard button groups pad between buttons so each button reaches a 48dp minimum target. Inner padding: XS 18dp, S 12dp, M 8dp, L 8dp, XL 8dp.
- Connected button groups use 2dp padding at all sizes. Extra small and small connected groups have 48dp target areas and a 48dp minimum width.

Source: [M3 buttons specs](https://m3.material.io/components/buttons/specs): extra small and small icon buttons must have a 48x48dp target or larger.

Source: [M3 FAB menu specs](https://m3.material.io/components/fab-menu/specs): FAB menu items use medium button measurements. Close button is 56dp. FAB margin is 16dp. The gap between FAB and menu is 4dp on Web. Large FAB places the menu with 56dp margin from the bottom.

Source: [M3 loading indicator specs](https://m3.material.io/components/loading-indicator/specs): size 48dp, shape container 38dp.

Source: [M3 progress indicators specs](https://m3.material.io/components/progress-indicators/specs): linear indicator inset 4dp from screen edge. Track thickness default 4dp. Wavy indicators use amplitude and wavelength; the numbers are in images and were not read.

Source: [M3 toolbars specs](https://m3.material.io/components/toolbars/specs): toolbars are 64dp high by default, with minimum outside padding of 16dp. The baseline bottom app bar is not recommended. Use the docked toolbar instead. The floating toolbar is separate from the docked toolbar on Compose.

Source: [M3 split button specs](https://m3.material.io/components/split-button/specs): trailing menu icon offset by size (XS to XL: -1, -1, -2, -3, -6 dp). Inner corner radius by size: 4, 4, 4, 8, 12 dp. Sizes: XS, S, M, L, XL. Colours: elevated, filled, tonal, outlined. Selection changes the trailing icon centring, not the colour.

## New components (summary)

Source: [M3 button groups overview](https://m3.material.io/components/button-groups/overview). Button groups replace the segmented button, which is no longer recommended. Standard and connected variants. All sizes XS to XL. Single-select, multi-select and selection-required.

FAB menu: one variant, up to six items, three colour sets (primary, secondary, tertiary). Source: [M3 FAB menu specs](https://m3.material.io/components/fab-menu/specs).

Split button: leading and trailing buttons, sizes XS to XL, four colour styles. Source: [M3 split button specs](https://m3.material.io/components/split-button/specs).

Loading indicator: indeterminate, with a default and contained form. Source: [M3 loading indicator specs](https://m3.material.io/components/loading-indicator/specs).

Progress indicators: linear and circular; determinate and indeterminate; flat and wavy. Source: [M3 progress indicators specs](https://m3.material.io/components/progress-indicators/specs).

Toolbars: docked and floating, with a vertical floating option and an optional FAB slot. Source: [M3 toolbars specs](https://m3.material.io/components/toolbars/specs).

Compose: the Compose Material3 M3 Expressive page is not reachable at the URL I tried (404). Source: [Compose Material3 page](https://developer.android.com/develop/ui/compose/designsystems/material3-expressive). The main Compose Material3 page says M3 Expressive "complements the Android 16 visual style and system UI." Source: [Compose Material3](https://developer.android.com/develop/ui/compose/designsystems/material3).

## Wear OS

Source: [Introducing M3 Expressive for Wear OS](https://android-developers.googleblog.com/2025/08/introducing-material-3-expressive-for-wear-os.html?hl=en). The post gives no numeric values. It covers a round-form edge-hugging button, a TransformingLazyColumn that shrinks edge items, a ScrollIndicator, a three-slot tile layout, tertiary colours with dynamic colour from the watch face, variable fonts and springy shape morphs. Not relevant to a phone-only build except the motion idea.

## Flutter status

Source: [flutter/flutter#168813](https://github.com/flutter/flutter/issues/168813). Open, feature request, labels include p: material_ui and team-design. Timeline: May 2025 the team paused Expressive work. June 2025 the team reviewed the design library strategy. July 2025 the team said Material and Cupertino are being split into separate packages, and Expressive work would follow. June 2026 a team member said decoupling is the first step and a rollout plan would follow. No firm date given.

Source: [material_ui on pub.dev](https://pub.dev/packages/material_ui). Version 1.11.1, published by flutter.dev (a verified publisher). The listing does not mention Expressive.

Source: [material_3_expressive on pub.dev](https://pub.dev/packages/material_3_expressive). Version 1.2.3, requires Flutter 3.47.0 or newer and Dart 3.13.0 or newer. Depends on material_ui and cupertino_ui. Covers button groups, FAB menu, split button, loading indicator, progress indicators, toolbars, shapes and springs (from the motor package). Publisher is listed as an unverified uploader. The listing does not use the word community.

## Plan check: Shape, Motion, Type

Plan source: reports/Delt Arena loops and screens.md, lines 61 to 71.

Shape. The plan sets data containers to a 4dp corner. This matches the extra small step of the scale. Confirmed. The plan uses one full pill (Signal) that morphs to a square when it completes. The spec's button pattern is full resting, square when pressed, so the idea is consistent. The spec's morph sizes are per button size and do not cover custom components, so the plan's Signal morph size is the team's own choice. The plan cites a codelab listing for the shape library. The M3 shape overview page is the direct source and should replace it. The plan's claim that Expressive introduces a shape library with built-in morphing is confirmed.

Motion. The plan says Flutter does not ship Expressive. Confirmed by the issue and pub.dev. The plan says "community packages such as material_3_expressive ... require a replacement material_ui package." The package depends on material_ui, which is confirmed. The word community is not stated by the listing, which says unverified uploader. The plan's sheet spring (settle) matches the spec's default speed for partly covering surfaces. The plan's stamp and toggle spring (snappy) fits the spec's fast speed for small elements. The plan's values are not yet set, and the spec gives the numbers above. The plan's rule that every interaction gets at most one motion is a design choice; the spec does not state it. Reduced motion: the plan relies on the system setting. The spec and the sources read did not cover reduced motion, so this is unverified.

Type. The plan uses Roboto Flex. The spec names Roboto as the default and Roboto Flex as a replacement example, so the choice is allowed. The plan cites the Wear OS post for Roboto Flex. That post does not name Roboto Flex; it says variable fonts let developers adjust weight and width. The M3 type page is the right citation. The plan's Display numerals at 64 to 96sp go above the largest M3 style (57sp). The spec advises against changing M3 type sizes because of reflow, so a custom numeral style should be treated as a custom component. The plan uses sp throughout, which matches the spec. The plan does not use emphasized styles. The spec recommends them for selected and action text, so the plan could use them for the selected set and the Signal label. The plan's width-axis idea for editing numbers fits the spec's advice to adjust variable axes such as weight and width.

Touch and thumb-first. The spec's floor is a 48dp target. The plan's thumb keypad keys at 64dp meet it. The plan's primary action in the bottom third is consistent with the spec's 16dp FAB margin and 16dp minimum outside padding for toolbars, but the spec does not prescribe a thumb zone.

## Still not reached

- The M3 Expressive overview page. The blog URL returned 404, and a second blog URL returned only a title.
- The Compose Material3 expressive developer page (URL returned 404).
- Pixel measurements in images: button size padding and heights, FAB menu sizes, progress indicator sizes, wavy amplitude and wavelength, toolbar paddings beyond the 64dp and 16dp given in text.
- Emphasized type weights and whether any emphasized size differs from baseline in the live token set.
- Expressive colour role tables beyond the per-component mappings given in text.
- Reduced motion guidance from M3 or Android.
- Haptic guidance from M3 or Android.
- Android 16 phone-specific motion docs beyond the Compose page sentence.
- Verification of the Compose spring numbers against the raw source. They came through a summarising model.
