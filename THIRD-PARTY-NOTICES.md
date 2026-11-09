# Third-party notices

The APK published in this repository bundles the runtime and tools of the
[nsmbu-recomp](https://github.com/nsmbu-recomp/nsmbu-recomp) project together with the components
below. The full license texts travel inside the APK (`assets/licenses` and
`assets/extractor-licenses`).

| Component | License | Where |
| --- | --- | --- |
| [nsmbu-recomp](https://github.com/nsmbu-recomp/nsmbu-recomp) runtime, tools and installer | MPL-2.0 | The whole APK |
| [SDL3](https://github.com/libsdl-org/SDL) | zlib | `lib/arm64-v8a` |
| [Dear ImGui](https://github.com/ocornut/imgui) | MIT | `lib/arm64-v8a` |
| [fmt](https://github.com/fmtlib/fmt) | MIT | `lib/arm64-v8a` |
| [LuaJIT](https://github.com/LuaJIT/LuaJIT) | MIT | `lib/arm64-v8a` |
| [xxHash](https://github.com/Cyan4973/xxHash) | BSD-2-Clause | `lib/arm64-v8a` |
| [metal-cpp](https://github.com/apple/metal-cpp) | Apache-2.0 | `lib/arm64-v8a` |
| [libadrenotools](https://github.com/libadrenotools/libadrenotools) | BSD-2-Clause | `assets/licenses/libadrenotools-BSD-2-Clause.txt` |
| [liblinkernsbypass](https://github.com/libadrenotools/liblinkernsbypass) | BSD-2-Clause | `assets/licenses/liblinkernsbypass-BSD-2-Clause.txt` |
| [zstd](https://github.com/facebook/zstd) | BSD / GPL-2.0 (dual) | `assets/extractor-licenses/zstd.txt` |
| Python (the runtime bundled for the on-device setup) | PSF License Agreement | `assets/python-home.zip`, `assets/python-source.zip` |
| Nintendo-File-Formats / Cemu extractor tools | See the project's own terms | `assets/extractor-licenses/project.txt` |

The port also builds on [ZeldaWWHDRecomp](https://github.com/ZeldaWWHDRecomp/ZeldaWWHDRecomp) and
uses the collision viewer of [Tsuru](https://github.com/Zenith-Team/Tsuru). Their licenses apply to
the parts that come from them.

The names and logos of the projects above belong to their respective owners. *New Super Mario Bros.
U* is a trademark of Nintendo; no Nintendo code, assets or game data are contained in this
repository or in its releases.
