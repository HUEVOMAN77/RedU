# Avisos de terceros

El APK publicado en este repositorio incluye el runtime y las herramientas del proyecto
[nsmbu-recomp](https://github.com/nsmbu-recomp/nsmbu-recomp) junto con los componentes de abajo. Los
textos completos de las licencias viajan dentro del APK (`assets/licenses` y
`assets/extractor-licenses`).

| Componente | Licencia | Dónde está |
| --- | --- | --- |
| Runtime, herramientas e instalador de [nsmbu-recomp](https://github.com/nsmbu-recomp/nsmbu-recomp) | MPL-2.0 | Todo el APK |
| [SDL3](https://github.com/libsdl-org/SDL) | zlib | `lib/arm64-v8a` |
| [Dear ImGui](https://github.com/ocornut/imgui) | MIT | `lib/arm64-v8a` |
| [fmt](https://github.com/fmtlib/fmt) | MIT | `lib/arm64-v8a` |
| [LuaJIT](https://github.com/LuaJIT/LuaJIT) | MIT | `lib/arm64-v8a` |
| [xxHash](https://github.com/Cyan4973/xxHash) | BSD-2-Clause | `lib/arm64-v8a` |
| [metal-cpp](https://github.com/apple/metal-cpp) | Apache-2.0 | `lib/arm64-v8a` |
| [libadrenotools](https://github.com/libadrenotools/libadrenotools) | BSD-2-Clause | `assets/licenses/libadrenotools-BSD-2-Clause.txt` |
| [liblinkernsbypass](https://github.com/libadrenotools/liblinkernsbypass) | BSD-2-Clause | `assets/licenses/liblinkernsbypass-BSD-2-Clause.txt` |
| [zstd](https://github.com/facebook/zstd) | BSD / GPL-2.0 (dual) | `assets/extractor-licenses/zstd.txt` |
| Python (el runtime que se usa durante la preparación) | PSF License Agreement | `assets/python-home.zip`, `assets/python-source.zip` |
| Herramientas de extracción Nintendo-File-Formats / Cemu | Términos del propio proyecto | `assets/extractor-licenses/project.txt` |

Este port también se apoya en [ZeldaWWHDRecomp](https://github.com/ZeldaWWHDRecomp/ZeldaWWHDRecomp) y
usa el visor de colisiones de [Tsuru](https://github.com/Zenith-Team/Tsuru). Sus licencias se
aplican a las partes que provienen de ellos.

Los nombres y los logotipos de los proyectos anteriores pertenecen a sus respectivos dueños.
*New Super Mario Bros. U* es una marca de Nintendo; este repositorio y sus versiones no contienen
código, imágenes ni datos del juego.
