# Compatibility

What RedU needs from a phone, what we measured on the reference device, and what happens on the
hardware we could not test.

**Español:** [COMPATIBILITY.es.md](COMPATIBILITY.es.md)

## Status labels

| Label | Meaning |
| --- | --- |
| **Verified** | We ran it on this hardware and recorded the result. |
| **Reported** | A user ran it and filed a [device report](https://github.com/HUEVOMAN77/RedU/issues/new/choose). |
| **Expected** | The hardware matches a verified device in the parts that matter. Not tested yet. |
| **Unsupported** | It will not run, and we say why. |

## Reference device (Verified)

| | |
| --- | --- |
| Model | HUAWEI NCO-LX3 (Nova 10) |
| SoC | Snapdragon 778G (Adreno 642L, ARMv8.2-A cores) |
| GPU | Adreno 642L, Vulkan 1.1.128, driver 512.530.0 |
| OS | Android 12 (API 31) |
| Panel | 60 Hz |
| ABI | arm64-v8a |
| Result | Setup completes (extract → translate → compile → link), the game boots, plays, saves and loads save states. |

### Measurements taken on it

| Measurement | Value |
| --- | --- |
| Game logic rate | 28.2–58.6 steps/s (median 35.2, mean 37.1) against a 60 Hz target |
| Logic pass | median 16.9 ms against a 16.67 ms budget |
| GPU busy | 72.2–95.3 % (median 82.3 %), GPU clock already at its maximum |
| Big cores | 691–1229 MHz of 2400 MHz |
| Texture compression | No native BC on this GPU: BC1–BC5 blocks are decoded by a compute shader into RGBA8 |
| Performance hint session | Unavailable (the Android API needs level 33; this phone is level 31) |
| Thermal headroom | The phone returns NaN (no thermal headroom HAL): RedU reads the thermal status instead |

The bottleneck on this phone is the CPU, not the GPU: the big cores stay well below their maximum
frequency while the GPU is already saturated. That is the reason the game can look like slow motion
even when the picture is smooth.

## Requirements in detail

| Requirement | Minimum | Why |
| --- | --- | --- |
| Android | 10 (API 29) | The build and the on-device toolchain use APIs from level 29 up. |
| ABI | arm64-v8a | The APK carries a 64-bit toolchain, the Python runtime and the compiler driver for ARM64. There is no 32-bit or x86_64 APK. |
| Vulkan | 1.1 | The renderer needs Vulkan 1.1 or newer; with 1.3 it uses dynamic rendering, below that it falls back to render passes. |
| GPU family | Any | The renderer is written against Vulkan, not against a vendor. Adreno, Mali and PowerVR all work in principle. |
| Free storage | A few GB | The built game and its shader cache live on the device. |
| Thermal API | Optional | Without headroom, RedU uses the thermal status. Neither is required to run the game. |
| Game | Own dump | Extracted folder, Cemu `.wua`, or `.wud`/`.wux` with keys. |

### What the screen rate means

| Panel | Recommended frame rate mode | Notes |
| --- | --- | --- |
| 60 Hz | 60 fps | Anything above 60 is drawn and never shown. The settings warn you. |
| 90 Hz | 60 fps | 90 is not a preset; 60 is the safe choice. |
| 120 Hz | 120 fps | The 120 fps mode shows properly on a 120 Hz panel. |
| 144 Hz / 165 Hz | 120 or 144 fps | Use the preset closest to the panel rate. |
| 240 Hz | 240 fps | Only on devices whose CPU and GPU can carry it. |

## Device classes (Expected)

These are expectations derived from the verified device and from the hardware specifications. They
are **not** measurements. If you own one of these, please file a
[device report](https://github.com/HUEVOMAN77/RedU/issues/new/choose) so the row can be corrected.

| Class | Examples | Expected result | Main risk |
| --- | --- | --- | --- |
| Snapdragon 7 Gen / 778G class | Nova 10, Redmi Note 12 Pro | Same as the reference device: runs, 60 fps logic with room to spare | CPU frequency scaling keeps the logic rate near 35 steps/s |
| Snapdragon 8 Gen 2 / 3 | flagship 2023 and later | Runs; more headroom for 120 fps | Heat on long sessions |
| Snapdragon 8 Gen 1 | 2022 flagships | Runs; expect the same CPU-limited behaviour as the reference | — |
| Adreno 6xx/7xx with an old stock driver | many 2020–2022 phones | Runs with the stock driver, but the driver may be Vulkan 1.1 with old features | Install **Turnip** for Vulkan 1.3 and better compatibility |
| Mali G57 / G68 / G77 | budget and mid-range 2021+ | Runs; the BC compute fallback costs some upload time | — |
| PowerVR | older iPhone-derived Androids | Not tested | — |

## Known limits and workarounds

| Symptom | Cause | What to do |
| --- | --- | --- |
| The app installs but the game does not start | The system Vulkan driver is older than 1.1, or too old for the features the renderer needs | Install a custom driver (Turnip) in **Settings → Graphics** and restart |
| The game feels slower than 60 fps | The phone keeps the big CPU cores below their maximum frequency | **Settings → Android → Lock the clock at 100%** (needs root), or the phone's game mode, or `adb shell cmd power set-fixed-performance-mode-enabled true` |
| Above 60 fps the picture does not feel faster | The panel is 60 Hz: the extra pictures are drawn and never shown | Use a 60 fps preset on a 60 Hz screen; use 120 fps on a 120 Hz panel |
| The game pauses by itself at high frame rates | The heat guard: the phone is close to its thermal limit | Wait for it to cool, or set the heat guard to *Relaxed* (or *Off* if you accept the stutter) |
| The setup is very slow | The game is compiled on the phone | Let it finish; it can be paused and resumed safely |
| No thermal information in the log | The phone does not expose the thermal headroom HAL | Since v1.0.5 the thermal status is used instead |
| A 32-bit or x86_64 phone cannot install the APK | There is only an arm64-v8a build | Use an arm64 device |

## Compatibility table

This table is filled from the reports users file. Fill in your own row: open an issue with the
[_Device compatibility report_](https://github.com/HUEVOMAN77/RedU/issues/new/choose) template.

| Device | Android | GPU / driver | Runs | Rating | fps | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| HUAWEI NCO-LX3 (Nova 10) | 12 | Adreno 642L, Vulkan 1.1.128, 512.530.0 | Yes | 4/5 | 60 (120 capped) | Verified. CPU-limited at high frame rates. |

## How the ratings work

| Rating | Meaning |
| --- | --- |
| 5/5 | Runs perfectly: correct picture, no errors, full speed for the device. |
| 4/5 | Runs well; a minor limitation (frame rate, a small graphical glitch). |
| 3/5 | Runs, but noticeably limited (slow logic, missing effects). |
| 2/5 | Runs only with a custom driver, or with visible errors. |
| 1/5 | Does not run. |

The rating is about the experience on that device, not about the phone's price or power.
