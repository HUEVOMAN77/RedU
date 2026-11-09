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
