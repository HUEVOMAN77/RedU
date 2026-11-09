# RedU

**New Super Mario Bros. U, recompiled natively for Android.**
RedU is the Android port maintained by **HUEVOMAN77**, built on top of the
[nsmbu-recomp](https://github.com/nsmbu-recomp/nsmbu-recomp) project (MPL-2.0).

It is **not an emulator**. The game's own code is recompiled for ARM processors and drawn with
Vulkan. The compilation happens on your phone, from your own legally dumped copy of the game.

> [!IMPORTANT]
> There is no Nintendo code, no assets and no game data in this repository or in its releases.
> You need your own legally dumped copy of *New Super Mario Bros. U* (Wii U).
> This repository, every release and the whole build process contain no Nintendo IP.

**Español:** [README.es.md](README.es.md) · **Compatibilidad:** [COMPATIBILITY.md](COMPATIBILITY.md) · **Créditos:** [CREDITS.md](CREDITS.md)

## Credits

**RedU is a fork.** The native port, the recompiler, the runtime and the graphics layer are the
work of the [nsmbu-recomp](https://github.com/nsmbu-recomp/nsmbu-recomp) project: **IrishBruse**
(Ethan Conneely), its creator and main author, **Lukas S** (`lschaupp`), who wrote the upstream
Android port, the Vulkan backend and the custom Adreno driver support, **rhemfur**, and every
other contributor of that project, under the **MPL-2.0** license. Their names, their commits and
their credits are kept intact.

What we did is take that source and work on the parts that did not fit phones: Android 10 and
newer instead of Android 13 only, the Spanish interface, the RedU branding, the heat and clock
work, and the link fix that made the on-device build finish.

Full credits: [CREDITS.md](CREDITS.md).

> **Compatibility so far:** everything is verified on **Snapdragon 778G class** hardware only
> (Adreno 642L, tested on a Huawei Nova 10). Other phones are not confirmed yet. That is what the
> [device reports](#report-your-device) are for, and the table in
> [COMPATIBILITY.md](COMPATIBILITY.md) grows with them.


## Downloads

| Version | File | Size | SHA-256 |
| --- | --- | --- | --- |
| **v1.0.5** (current) | `RedU-1.0.5-android-arm64.apk` | 132.2 MiB | `67fef4d4a52cdf0ae646f893e6e5b04d220744a37c386873f6027f514d92db35` |

Get it from the [Releases page](https://github.com/HUEVOMAN77/RedU/releases). Every release also
ships a `SHA256SUMS.txt`; check it if you want to be sure the download arrived intact.

The source code of the port lives in [HUEVOMAN77/nsmbu-recomp](https://github.com/HUEVOMAN77/nsmbu-recomp)
(branch `android`). This repository is the distribution point and the compatibility tracker.

## Requirements

| | Requirement | Notes |
| --- | --- | --- |
| Android | **10 or newer** (API 29+) | Built for API 36; tested on Android 10, 11, 12 |
| CPU | **64-bit ARM (arm64-v8a)** | No 32-bit or x86_64 APK in this release |
| GPU | **Vulkan 1.1 or newer** | Vulkan 1.3 is recommended (dynamic rendering) |
| Storage | A few GB free while setup runs | The built game plus its shader cache |
| Game | Your own *New Super Mario Bros. U* | See [Supported game versions](#supported-game-versions) |

A custom Vulkan driver (Mesa **Turnip**) is optional and recommended on Adreno phones whose
stock driver is old. See [Custom Vulkan driver](#custom-vulkan-driver-turnip).

### Supported game versions

| Region | Title ID | Title version | Status |
| --- | --- | --- | --- |
| USA | `00050000-10101d00` | 64 (1.3.0) | Supported |
| USA base disc | `00050000-10101d00` | 0 | Supported |
| Europe | `00050000-10101e00` | 80 (1.3.0) | Supported |
| Europe base disc | `00050000-10101e00` | 0 | Supported |
| USA (NSMBU + NSLU) | `00050000-1014b700` | 0 | Partially supported |
| Europe (NSMBU + NSLU) | `00050000-1014b800` | 0 | Partially supported |
| Japan | `00050000-10101c00` | — | Not supported yet |

## Install

1. **Install the APK.**
   Download it from the [Releases page](https://github.com/HUEVOMAN77/RedU/releases), then open
   it on the phone and allow installing from that source. Android 10+ is required; the phone may
   ask to allow installs from your browser or file manager.
2. **Open the app and tap _Choose your game_.** Pick what you have:
   - **Extracted game folder**: a folder of its own (for example `Download/NSMBU`) that contains
     `code`, `content` and `meta`. Android will not let you pick `Download` itself, the top of the
     internal storage or `Android/data`.
   - **Cemu archive (`.wua`)**: a single file, pickable from any folder. No keys needed.
   - **Disc image (`.wud` / `.wux`)**: a single file plus the disc key and the Wii U common key.
     A Cemu `keys.txt` with labelled `common =` and `disc =` lines covers both.
   - The optional **1.3.0 update folder** merges an update into the game.
3. **Tap _Start_.** The phone extracts, translates, compiles and links the game once. The screen
   shows the progress and you can leave the app while it runs. Setup pauses itself when the
   device gets too warm or the battery is low, and it can be paused safely by hand.
4. **When setup finishes, tap _Play_.**
   Later versions install over this one and keep your saves and settings. The app icon skips the
   installer once a game is ready; long-press the icon and choose *Game setup* to open it again.

## Playing

- **On-screen controls**: stick, D-pad, A B X Y, L R ZL ZR and + −. Hold the show/hide button to
  move or resize them; the layout is saved on the device.
- **Controllers**: Bluetooth or USB controllers work. The touch buttons hide while a controller
  is connected.
- **Settings**: the Back button or the gesture opens and closes the settings menu
  (F12 / R3 also work). Every option is in Spanish by default, English as a fallback.
- **Save states**: five slots for a course or the world map (Shift+F1–F5 to save, F1–F5 to load).

## Frame rate and refresh rate

The game logic always runs at 60 steps per second. **Settings → Graphics → Frame rate** controls
how many pictures are drawn:

| Mode | What it does |
| --- | --- |
| 30 fps | Half the draws, two logic steps per picture. The game keeps its speed. |
| 60 fps | The native rate of the game. |
| 120 / 144 / 165 / 240 fps | Present caps: extra pictures between the fixed 60 Hz logic steps, blended from wall-clock time. |
| Custom | Any rate from 60 to 1000. |
| Unlocked | Draws as fast as the device can while the logic stays at 60 steps per second. |

**Your screen decides how many of those pictures you ever see.** A 60 Hz panel shows 60 fps, and
everything above that is drawn, never shown, and takes GPU away from the game — the settings warn
you when that happens. A **120 Hz panel** shows the 120 fps mode properly; that is the mode worth
using on those phones.

The frame rate number is the render rate, even when the display cannot show every picture.

### Heat guard

Higher frame rates make the device work harder. **Settings → Graphics → Heat guard**:

- **Normal** (default): the limit for your kind of device (a phone or a fan-cooled handheld).
- **Relaxed**: waits longer before it pauses.
- **Off**: never pauses for heat.

When the phone says it is close to getting too hot, the in-between frames pause and the game keeps
60 fps. When it cools down, the higher rate comes back by itself. On phones that do not report
thermal headroom, RedU reads the thermal status instead.

### Clock at 100%

**Settings → Android → Lock the clock at 100%** asks the phone to run every core and the GPU at
their maximum frequency, and tells you exactly what the phone allowed.

Android only lets an ordinary app change the clock on a rooted phone. Without root, use the
phone's game mode (Game Space, Game Booster) or run this once with a cable:

```sh
adb shell cmd power set-fixed-performance-mode-enabled true
```

## Custom Vulkan driver (Turnip)

Some Adreno drivers are old enough that the game shows graphical errors or misses features.
Mesa **Turnip** is a replacement Vulkan driver that fixes that, and it often runs faster too.

**Settings → Graphics → Install driver ZIP...**, then pick the installed driver and restart the
game. The app accepts a ZIP with an AdrenoTools-style manifest (`schemaVersion` 1, with
`libraryName`, `name`, `driverVersion` or `packageVersion` and `minApi`) and a root-level **arm64**
ELF shared library. The driver is kept in the app's private storage and loaded at start-up; if it
fails to load, the game falls back to the system driver and says so.

## What we measured on the reference device

Reference device: **HUAWEI NCO-LX3 (Nova 10)**, Snapdragon 778G, Adreno 642L, Android 12,
Vulkan 1.1.128, driver 512.530.0, 60 Hz panel. The game is built, linked, booted and played
on it.

| Measurement | Value |
| --- | --- |
| Game logic | 28.2–58.6 steps/s (median 35.2) against a 60 Hz target |
| Logic pass | median 16.9 ms against a 16.67 ms budget |
| GPU busy | 72.2–95.3 % (median 82.3 %) with the GPU clock already at its maximum |
| Big CPU cores | 691–1229 MHz of 2400 MHz — the CPU is the bottleneck, not the GPU |
| Texture compression | No native BC on this GPU: BC blocks are decoded by a compute shader |
| Performance hints | Not available on this device (the API needs Android 13) |
| Thermal headroom | Not reported by this phone: RedU uses the thermal status instead |

That is why the game can feel like slow motion even though the GPU is busy: the phone keeps the big
cores below their maximum frequency. The clock control and the phone's game mode are the way to
address it.

## Report your device

RedU is tuned for the hardware it was tested on, and every other phone is a guess until it reports.

- **Open an issue with the [_Device compatibility report_](https://github.com/HUEVOMAN77/RedU/issues/new/choose)
  template** to tell us your model, your Android version, your GPU, whether the game runs, how well
  it runs (a rating from 1 to 5) and how many frames per second you get. It takes two minutes.
- **Discussions → Show and tell** is where to write a full review, ask for a phone or share a tip.
  A review that says "it works on my phone", with the model, is the most useful thing you can leave.
- **Bugs** have their own template; attach the log that the app offers to share (long-press the
  icon, or *Share log* in the setup screen).

Reports are what makes the next version better on your phone. The compatibility table in
[COMPATIBILITY.md](COMPATIBILITY.md) is built from them.

## Fair play

- Use your own copy of the game, dumped from your own disc or console.
- If someone offers you a ready-made APK with the game inside, it does not come from this project.
- This is a fan project, not affiliated with or endorsed by Nintendo.
  *New Super Mario Bros. U* is a trademark of Nintendo.

## Credits and license

- The native port, the recompiler, the runtime and the graphics layer are the work of the
  original [nsmbu-recomp](https://github.com/nsmbu-recomp/nsmbu-recomp) authors — **IrishBruse**,
  **Lukas S**, **rhemfur** and the rest — under **MPL-2.0**. Their names and the license of that
  project are kept intact. See [CREDITS.md](CREDITS.md).
- The Android port for phones, the RedU branding, the Spanish interface and the work on this
  repository are by **HUEVOMAN77**.
- Third-party components bundled in the APK are listed in
  [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).


## Version history

See [CHANGELOG.md](CHANGELOG.md).
