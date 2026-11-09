# Credits

**RedU is a fork. The original port is not ours, and this repository says so everywhere it matters.**

The native recompilation of *New Super Mario Bros. U* is the work of the
[nsmbu-recomp](https://github.com/nsmbu-recomp/nsmbu-recomp) project and its authors, published
under the **MPL-2.0** license. We took that source, studied it, and worked on the parts that did
not fit phones.

## The original authors

| Who | What they did |
| --- | --- |
| **IrishBruse** (Ethan Conneely) | Creator and main author of the native port: the recompiler, the runtime, the graphics layer and the desktop installers. |
| **Lukas S** (`lschaupp`) | The Android port upstream: the on-device build, the Vulkan backend, the BC texture decoder and the custom Adreno driver support. |
| **rhemfur** | The Android device checklist and the on-device validation work. |
| **Sean13128, alayhayali, resadent, arcadematicas, depende3000** and the rest of the upstream contributors | Fixes, tools and reports. |

The full list is on the
[upstream contributors page](https://github.com/nsmbu-recomp/nsmbu-recomp/graphs/contributors),
and every commit keeps its original author.

## What RedU changed (HUEVOMAN77)

RedU is our fork of that project. The upstream port was built with desktop and high-end Android
devices in mind; its Android app asked for **Android 13** and a **Vulkan 1.3** driver, which left
a lot of phones out. Our work is about the phones that were left out:

- The app installs and runs on **Android 10 and newer** (API 29+), with the toolchain and the
  on-device setup fixed for those API levels.
- **Spanish** interface by default (Latin American Spanish, with English as a fallback).
- The **RedU** branding: name, icon and app identity.
- The **performance work for phones**: a working heat guard on devices that do not report thermal
  headroom, a clock control for the settings, warnings when the frame rate is above the screen rate,
  and an explanation of what a custom Vulkan driver does.
- The **link fix** that made the on-device build finish on a phone.

None of that replaces the original work: the recompiler, the runtime and the renderer are theirs,
under MPL-2.0, with their credits intact.

## Other projects this one stands on

| Project | Role | License |
| --- | --- | --- |
| [nsmbu-recomp](https://github.com/nsmbu-recomp/nsmbu-recomp) | The native port this one is forked from | MPL-2.0 |
| [ZeldaWWHDRecomp](https://github.com/ZeldaWWHDRecomp/ZeldaWWHDRecomp) | The recompilation project the original port was forked from | See the upstream repository |
| [Tsuru](https://github.com/Zenith-Team/Tsuru) | The collision viewer the original port's viewer is based on | See the upstream repository |
| [Cemu](https://github.com/celsobianchi/celsobianchi) and the [Nintendo-File-Formats](https://github.com/Gcenx/Nintendo-File-Formats) tools | Used to read the game formats | See the upstream repository |

The components bundled inside the APK are listed in
[THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).

---

# Créditos

**RedU es un fork. El port original no es nuestro, y este repositorio lo dice en todas partes.**

La recompilación nativa de *New Super Mario Bros. U* es obra del proyecto
[nsmbu-recomp](https://github.com/nsmbu-recomp/nsmbu-recomp) y de sus autores, bajo la licencia
**MPL-2.0**. Nosotros tomamos ese código, lo estudiamos y trabajamos en las partes que no encajaban
con los teléfonos.

## Los autores originales

| Quién | Qué hizo |
| --- | --- |
| **IrishBruse** (Ethan Conneely) | Creador y autor principal del port nativo: el recompilador, el runtime, la capa gráfica y los instaladores de escritorio. |
| **Lukas S** (`lschaupp`) | El port para Android en el proyecto original: la compilación dentro del teléfono, el backend de Vulkan, el decodificador de texturas BC y el soporte de drivers propios de Adreno. |
| **rhemfur** | La lista de pruebas en dispositivos Android y el trabajo de validación en el teléfono. |
| **Sean13128, alayhayali, resadent, arcadematicas, depende3000** y el resto de quienes contribuyeron al proyecto original | Arreglos, herramientas y reportes. |

La lista completa está en la
[página de contribuyentes del proyecto original](https://github.com/nsmbu-recomp/nsmbu-recomp/graphs/contributors),
y cada commit conserva su autor original.

## Qué cambió RedU (HUEVOMAN77)

RedU es nuestro fork de ese proyecto. El port original estaba pensado primero para el escritorio
y para Android de gama alta: su app para Android pedía **Android 13** y un driver con **Vulkan
1.3**, lo que dejaba fuera a muchos teléfonos. Nuestro trabajo es sobre los teléfonos que quedaron
afuera:

- La app se instala y corre en **Android 10 o superior** (API 29+), con el toolchain y la
  preparación dentro del teléfono corregidos para esos niveles de API.
- Interfaz **en español** por defecto (español latinoamericano, con el inglés como respaldo).
- La marca **RedU**: nombre, ícono e identidad de la app.
- El **trabajo de rendimiento en teléfonos**: una guardia de calor que funciona en dispositivos que
  no informan margen térmico, un control del reloj en los ajustes, el aviso cuando los cuadros por
  segundo están por encima de los de la pantalla, y la explicación de qué hace un driver Vulkan
  propio.
- El **arreglo del enlace** que hizo que la compilación dentro del teléfono terminara.

Nada de eso sustituye el trabajo original: el recompilador, el runtime y el renderizador son
suyos, bajo MPL-2.0, con sus créditos intactos.

## Otros proyectos en los que se apoya este

| Proyecto | Papel | Licencia |
| --- | --- | --- |
| [nsmbu-recomp](https://github.com/nsmbu-recomp/nsmbu-recomp) | El port nativo del que este proyecto es fork | MPL-2.0 |
| [ZeldaWWHDRecomp](https://github.com/ZeldaWWHDRecomp/ZeldaWWHDRecomp) | El proyecto de recompilación del que el port original es fork | Ver el repositorio original |
| [Tsuru](https://github.com/Zenith-Team/Tsuru) | El visor de colisiones en el que se basa el del port original | Ver el repositorio original |
| [Cemu](https://github.com/celsobianchi/celsobianchi) y las herramientas [Nintendo-File-Formats](https://github.com/Gcenx/Nintendo-File-Formats) | Se usan para leer los formatos del juego | Ver el repositorio original |

Los componentes que van dentro del APK están listados en
[THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).
