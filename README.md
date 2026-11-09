# RedU

**New Super Mario Bros. U, recompilado de forma nativa para Android.**
RedU es el port para Android que mantiene **HUEVOMAN77**, construido sobre el proyecto
[nsmbu-recomp](https://github.com/nsmbu-recomp/nsmbu-recomp) (MPL-2.0).

No es un emulador. El código del juego se recompila para procesadores ARM y se dibuja con
Vulkan. La compilación ocurre en tu teléfono, a partir de tu propia copia del juego extraída
legalmente.

> [!IMPORTANT]
> En este repositorio y en todas sus versiones no hay código, imágenes ni datos del juego de
> Nintendo. Necesitas tu propia copia legal de *New Super Mario Bros. U* (Wii U).
> Ni el repositorio, ni las versiones, ni el proceso de compilación contienen propiedad intelectual
> de Nintendo.

**Compatibilidad:** [COMPATIBILITY.md](COMPATIBILITY.md) · **Créditos:** [CREDITS.md](CREDITS.md) ·
**Historial:** [CHANGELOG.md](CHANGELOG.md)

## Créditos

**RedU es un fork.** El port nativo, el recompilador, el runtime y la capa gráfica son obra del
proyecto [nsmbu-recomp](https://github.com/nsmbu-recomp/nsmbu-recomp): **IrishBruse**
(Ethan Conneely), su creador y autor principal, **Lukas S** (`lschaupp`), que escribió el port
para Android del proyecto original, el backend de Vulkan y el soporte de drivers propios de Adreno,
**rhemfur**, y todos los demás contribuyentes, bajo la licencia **MPL-2.0**. Sus nombres, sus
commits y sus créditos quedan intactos.

Lo que hicimos nosotros fue tomar ese código y trabajar en las partes que no encajaban con los
teléfonos: Android 10 o superior en vez de solo Android 13, la interfaz en español, la marca RedU,
el trabajo de calor y de reloj, y el arreglo del enlace que hizo que la compilación dentro del
teléfono terminara.

Créditos completos: [CREDITS.md](CREDITS.md).

> **Compatibilidad por ahora:** todo está verificado solo en hardware de la clase **Snapdragon
> 778G** (Adreno 642L, probado en un Huawei Nova 10). Otros teléfonos aún no están confirmados.
> Para eso sirven los [informes de dispositivo](#cuenta-cómo-te-fue), y la tabla de
> [COMPATIBILITY.md](COMPATIBILITY.md) crece con ellos.

## Descargas

| Versión | Archivo | Tamaño | SHA-256 |
| --- | --- | --- | --- |
| **v1.0.5** (actual) | `RedU-1.0.5-android-arm64.apk` | 132,2 MiB | `67fef4d4a52cdf0ae646f893e6e5b04d220744a37c386873f6027f514d92db35` |

Descárgalo de la [página de versiones](https://github.com/HUEVOMAN77/RedU/releases). Cada versión
incluye además un `SHA256SUMS.txt` para comprobar que la descarga llegó intacta.

El código fuente del port es privado (es un fork propio de
[nsmbu-recomp](https://github.com/nsmbu-recomp/nsmbu-recomp), en la rama `android`). Si lo quieres
para compilarlo o estudiarlo, pídelo en las discusiones. Este repositorio es el punto de
distribución y el registro de compatibilidad.

## Requisitos

| | Requisito | Notas |
| --- | --- | --- |
| Android | **10 o superior** (API 29+) | Compilado para API 36; probado en Android 10, 11 y 12 |
| CPU | **ARM de 64 bits (arm64-v8a)** | En esta versión no hay APK de 32 bits ni de x86_64 |
| GPU | **Vulkan 1.1 o superior** | Se recomienda Vulkan 1.3 (renderizado dinámico) |
| Espacio | Unos cuantos GB libres durante la preparación | El juego compilado más su caché de sombreadores |
| Juego | Tu propio *New Super Mario Bros. U* | Mira [versiones del juego compatibles](#versiones-del-juego-compatibles) |

Un driver Vulkan propio (Mesa **Turnip**) es opcional y muy recomendable en teléfonos Adreno con
el driver de fábrica viejo. Mira [Driver Vulkan propio (Turnip)](#driver-vulkan-propio-turnip).

### Versiones del juego compatibles

| Región | Title ID | Versión de título | Estado |
| --- | --- | --- | --- |
| USA | `00050000-10101d00` | 64 (1.3.0) | Compatible |
| Disco base USA | `00050000-10101d00` | 0 | Compatible |
| Europa | `00050000-10101e00` | 80 (1.3.0) | Compatible |
| Disco base Europa | `00050000-10101e00` | 0 | Compatible |
| USA (NSMBU + NSLU) | `00050000-1014b700` | 0 | Parcialmente compatible |
| Europa (NSMBU + NSLU) | `00050000-1014b800` | 0 | Parcialmente compatible |
| Japón | `00050000-10101c00` | — | Todavía no compatible |

## Instalación

1. **Instala el APK.**
   Descárgalo de la [página de versiones](https://github.com/HUEVOMAN77/RedU/releases), ábrelo en
   el teléfono y permite instalar desde esa fuente. Hace falta Android 10 o superior; el sistema
   puede pedir permiso para instalar desde el navegador o el explorador de archivos.
2. **Abre la app y toca _Elegir tu juego_.** Escoge lo que tengas:
   - **Carpeta del juego extraída**: una carpeta propia (por ejemplo `Download/NSMBU`) que contenga
     `code`, `content` y `meta`. Android no deja elegir `Download` mismo, la raíz del
     almacenamiento interno ni `Android/data`.
   - **Archivo de Cemu (`.wua`)**: un solo archivo, que se puede elegir desde cualquier carpeta.
     No necesita claves.
   - **Imagen de disco (`.wud` / `.wux`)**: un solo archivo más la clave del disco y la clave común
     de Wii U. Un `keys.txt` de Cemu con las líneas `common =` y `disc =` cubre las dos.
   - La **carpeta de actualización 1.3.0** es opcional y se integra en el juego.
3. **Toca _Comenzar_.** El teléfono extrae, traduce, compila y enlaza el juego una vez. La pantalla
   muestra el avance y puedes salir de la app mientras trabaja. La preparación se pausa sola si el
   teléfono se calienta demasiado o si la batería está baja, y también se puede pausar a mano.
4. **Cuando termine, toca _Jugar_.**
   Las versiones siguientes se instalan encima de esta y conservan tus partidas y ajustes. El icono
   de la app salta el instalador cuando el juego ya está listo; mantén presionado el ícono y elige
   _Game setup_ para abrirlo de nuevo.

## Cómo se juega

- **Controles en pantalla**: joystick, cruceta, A B X Y, L R ZL ZR y + −. Mantén presionado el botón
  que muestra y esconde los controles para moverlos o cambiarles el tamaño; la distribución se
  guarda en el teléfono.
- **Mandos**: funcionan los mandos de Bluetooth y los USB. Los controles táctiles se esconden
  mientras hay un mando conectado.
- **Ajustes**: el botón Atrás o el gesto abre y cierra el menú de ajustes (también F12 / R3). Todo
  está en español por defecto, con el inglés como respaldo.
- **Partidas guardadas**: cinco espacios para un nivel o para el mapa del mundo (Shift+F1–F5 para
  guardar, F1–F5 para cargar).

## Cuadros por segundo y tasa de refresco

La lógica del juego corre siempre a 60 pasos por segundo. **Ajustes → Gráficos → Cuadros por
segundo** decide cuántos cuadros se dibujan:

| Modo | Qué hace |
| --- | --- |
| 30 fps | Dibuja la mitad de las veces: dos pasos de lógica por cuadro. El juego mantiene su velocidad. |
| 60 fps | La tasa nativa del juego. |
| 120 / 144 / 165 / 240 fps | Tope de presentación: cuadros extra entre los pasos fijos de 60 Hz, mezclados con el reloj real. |
| Personalizado | Cualquier tasa de 60 a 1000. |
| Desbloqueado | Dibuja tan rápido como el dispositivo aguante, con la lógica siempre en 60 pasos por segundo. |

**Tu pantalla decide cuántos de esos cuadros llegas a ver.** Una pantalla de 60 Hz muestra 60 fps, y
todo lo de arriba se dibuja, no se ve, y le roba GPU al juego: los ajustes te avisan cuando pasa.
Una pantalla de **120 Hz** muestra bien el modo de 120 fps; ese es el modo que vale en esos
teléfonos.

El número de fps es la tasa de dibujo, aunque la pantalla no pueda mostrar cada cuadro.

### Guardia de calor

Subir los cuadros por segundo hace trabajar más al teléfono. **Ajustes → Gráficos → Guardia de
calor**:

- **Normal** (por defecto): el límite para tu tipo de dispositivo (teléfono o consola portátil con
  ventilador).
- **Relajada**: espera más antes de pausar.
- **Apagada**: nunca pausa por calor.

Cuando el teléfono avisa de que está cerca de calentarse demasiado, los cuadros intermedios se
pausan y el juego se queda en 60 fps. Cuando se enfría, la tasa más alta vuelve sola. En los
teléfonos que no informan el margen térmico, RedU lee el estado térmico.

### Reloj al 100%

**Ajustes → Android → Poner el reloj al 100%** le pide al teléfono que corra todos los núcleos y la
GPU a su frecuencia máxima, y te dice exactamente qué permitió el teléfono.

Android solo deja que una app normal cambie el reloj en un teléfono con root. Sin root, usa el modo
de juego del teléfono (Game Space, Game Booster) o ejecuta esto una vez con cable:

```sh
adb shell cmd power set-fixed-performance-mode-enabled true
```

## Driver Vulkan propio (Turnip)

Algunos drivers de Adreno son tan viejos que el juego muestra errores gráficos o le faltan
funciones. Mesa **Turnip** es un driver Vulkan de reemplazo que lo arregla, y a menudo también corre
más rápido.

**Ajustes → Gráficos → Instalar ZIP del driver...**, elige el driver instalado y reinicia el juego.
La app acepta un ZIP con un manifiesto al estilo de AdrenoTools (`schemaVersion` 1, con
`libraryName`, `name`, `driverVersion` o `packageVersion` y `minApi`) y una biblioteca compartida ELF
**arm64** en la raíz. El driver se guarda en el almacenamiento privado de la app y se carga al
arrancar; si falla la carga, el juego vuelve al driver del sistema y lo dice.

## Lo que medimos en el dispositivo de referencia

Dispositivo de referencia: **HUAWEI NCO-LX3 (Nova 10)**, Snapdragon 778G, Adreno 642L, Android 12,
Vulkan 1.1.128, driver 512.530.0, pantalla de 60 Hz. El juego se compila, se enlaza, arranca y se
juega en él.

| Medición | Valor |
| --- | --- |
| Lógica del juego | 28,2–58,6 pasos/s (mediana 35,2) frente a una meta de 60 Hz |
| Pase de lógica | mediana 16,9 ms frente a un presupuesto de 16,67 ms |
| GPU ocupada | 72,2–95,3 % (mediana 82,3 %) con el reloj de la GPU ya en su máximo |
| Núcleos grandes | 691–1229 MHz de 2400 MHz: el cuello de botella es la CPU, no la GPU |
| Compresión de texturas | Sin BC nativo en esta GPU: los bloques BC los decodifica un shader de cómputo |
| Consejos de rendimiento | No disponibles en este dispositivo (la API pide Android 13) |
| Margen térmico | Este teléfono no lo informa: RedU usa el estado térmico |

Por eso el juego puede sentirse como en cámara lenta aunque la GPU esté ocupada: el teléfono
mantiene los núcleos grandes por debajo de su frecuencia máxima. El control del reloj y el modo de
juego del teléfono son la manera de atacar eso.

## Cuenta cómo te fue

RedU está afinado para el hardware en el que se probó, y cualquier otro teléfono es una suposición
hasta que lo reporte.

- **Abre un issue con la plantilla de [_Informe de compatibilidad_](https://github.com/HUEVOMAN77/RedU/issues/new/choose)**
  para decirnos tu modelo, tu versión de Android, tu GPU, si el juego funciona, qué tan bien funciona
  (una calificación del 1 al 5) y cuántos cuadros por segundo obtienes. Son dos minutos.
- **Discusiones → Show and tell** es para escribir una reseña completa, pedir un teléfono o compartir
  un consejo. Una reseña que diga "en mi teléfono funciona", con el modelo, es lo más útil que
  puedes dejar.
- **Los errores** tienen su propia plantilla; adjunta el log que la app ofrece para compartir
  (mantén presionado el ícono, o _Compartir log_ en la pantalla de preparación).

Los reportes son los que hacen que la próxima versión esté mejor en tu teléfono. La tabla de
compatibilidad de [COMPATIBILITY.md](COMPATIBILITY.md) sale de ellos.

## Juego limpio

- Usa tu propia copia del juego, extraída de tu propio disco o consola.
- Si alguien te ofrece un APK ya hecho con el juego dentro, no viene de este proyecto.
- Esto es un proyecto de fans, sin afiliación ni respaldo de Nintendo.
  *New Super Mario Bros. U* es una marca registrada de Nintendo.

## Créditos y licencia

- El port nativo, el recompilador, el runtime y la capa gráfica son obra de los autores del
  proyecto original [nsmbu-recomp](https://github.com/nsmbu-recomp/nsmbu-recomp) — **IrishBruse**,
  **Lukas S**, **rhemfur** y el resto — bajo **MPL-2.0**. Sus nombres y la licencia de ese
  proyecto quedan intactos. Mira [CREDITS.md](CREDITS.md).
- El port para teléfonos, la marca RedU, la interfaz en español y el trabajo en este repositorio
  son de **HUEVOMAN77**.
- Los componentes de terceros que van dentro del APK están en
  [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).
