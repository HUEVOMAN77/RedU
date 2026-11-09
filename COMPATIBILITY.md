# Compatibilidad

Qué necesita RedU de un teléfono, qué medimos en el dispositivo de referencia y qué pasa con el
hardware que no pudimos probar.

## Etiquetas de estado

| Etiqueta | Significado |
| --- | --- |
| **Verificado** | Lo corrimos en ese hardware y anotamos el resultado. |
| **Reportado** | Un usuario lo corrió y dejó un [informe de dispositivo](https://github.com/HUEVOMAN77/RedU/issues/new/choose). |
| **Esperado** | El hardware coincide con un dispositivo verificado en lo que importa. Aún sin probar. |
| **No compatible** | No va a funcionar, y decimos por qué. |

## Dispositivo de referencia (Verificado)

| | |
| --- | --- |
| Modelo | HUAWEI NCO-LX3 (Nova 10) |
| SoC | Snapdragon 778G (Adreno 642L, núcleos ARMv8.2-A) |
| GPU | Adreno 642L, Vulkan 1.1.128, driver 512.530.0 |
| Sistema | Android 12 (API 31) |
| Pantalla | 60 Hz |
| ABI | arm64-v8a |
| Resultado | La preparación termina (extrae → traduce → compila → enlaza), el juego arranca, se juega, guarda y carga partidas guardadas. |

### Mediciones hechas en él

| Medición | Valor |
| --- | --- |
| Tasa de la lógica | 28,2–58,6 pasos/s (mediana 35,2, media 37,1) frente a una meta de 60 Hz |
| Pase de lógica | mediana 16,9 ms frente a un presupuesto de 16,67 ms |
| GPU ocupada | 72,2–95,3 % (mediana 82,3 %), con el reloj de la GPU ya en su máximo |
| Núcleos grandes | 691–1229 MHz de 2400 MHz |
| Compresión de texturas | Sin BC nativo en esta GPU: los bloques BC1–BC5 los decodifica un shader de cómputo a RGBA8 |
| Sesión de consejos de rendimiento | No disponible (la API de Android pide nivel 33; este teléfono es nivel 31) |
| Margen térmico | El teléfono devuelve NaN (no tiene HAL de margen térmico): RedU lee el estado térmico |

El cuello de botella en este teléfono es la CPU, no la GPU: los núcleos grandes se quedan muy por
debajo de su frecuencia máxima mientras la GPU ya está saturada. Esa es la razón de que el juego
pueda verse como en cámara lenta aunque la imagen sea fluida.

## Requisitos en detalle

| Requisito | Mínimo | Por qué |
| --- | --- | --- |
| Android | 10 (API 29) | La compilación y el toolchain dentro del teléfono usan APIs del nivel 29 en adelante. |
| ABI | arm64-v8a | El APK trae el toolchain de 64 bits, el runtime de Python y el compilador para ARM64. No hay APK de 32 bits ni de x86_64. |
| Vulkan | 1.1 | El renderizador necesita Vulkan 1.1 o superior; con 1.3 usa renderizado dinámico y por debajo cae a render passes. |
| Familia de GPU | Cualquiera | El renderizador está escrito contra Vulkan, no contra un fabricante. Adreno, Mali y PowerVR sirven en principio. |
| Espacio libre | Unos cuantos GB | El juego compilado y su caché de sombreadores viven en el teléfono. |
| API térmica | Opcional | Sin margen térmico, RedU usa el estado térmico. Ninguna de las dos hace falta para jugar. |
| Juego | Tu propio dump | Carpeta extraída, `.wua` de Cemu, o `.wud`/`.wux` con claves. |

### Qué significa la tasa de la pantalla

| Pantalla | Modo recomendado | Notas |
| --- | --- | --- |
| 60 Hz | 60 fps | Todo lo que pase de 60 se dibuja y no se ve. Los ajustes te avisan. |
| 90 Hz | 60 fps | 90 no es un valor predeterminado; 60 es la opción segura. |
| 120 Hz | 120 fps | El modo de 120 fps se ve bien en una pantalla de 120 Hz. |
| 144 Hz / 165 Hz | 120 o 144 fps | Usa el valor predeterminado más cercano a la tasa de la pantalla. |
| 240 Hz | 240 fps | Solo en dispositivos cuya CPU y GPU den la talla. |

## Clases de dispositivos (Esperado)

Estas expectativas salen del dispositivo verificado y de las especificaciones del hardware. **No**
son mediciones. Si tienes uno de estos, deja un
[informe de dispositivo](https://github.com/HUEVOMAN77/RedU/issues/new/choose) para que la fila
se pueda corregir.

| Clase | Ejemplos | Resultado esperado | Riesgo principal |
| --- | --- | --- | --- |
| Snapdragon 7 Gen / 778G | Nova 10, Redmi Note 12 Pro | Igual que el dispositivo de referencia: corre, con la lógica de 60 fps con margen | El escalado de frecuencia de la CPU deja la lógica cerca de 35 pasos/s |
| Snapdragon 8 Gen 2 / 3 | gama alta de 2023 en adelante | Corre; más margen para 120 fps | Calor en sesiones largas |
| Snapdragon 8 Gen 1 | gama alta de 2022 | Corre; mismo comportamiento limitado por CPU que el dispositivo de referencia | — |
| Adreno 6xx/7xx con driver de fábrica viejo | muchos teléfonos de 2020–2022 | Corre con el driver de fábrica, pero puede ser Vulkan 1.1 con funciones antiguas | Instala **Turnip** para tener Vulkan 1.3 y mejor compatibilidad |
| Mali G57 / G68 / G77 | gama de entrada y media de 2021 en adelante | Corre; el decodificador BC por cómputo cuesta algo de tiempo de subida | — |
| PowerVR | Android antiguos derivados de iPhone | Sin probar | — |

## Límites conocidos y soluciones

| Síntoma | Causa | Qué hacer |
| --- | --- | --- |
| La app se instala pero el juego no arranca | El driver Vulkan del sistema es anterior a 1.1, o demasiado viejo para las funciones que pide el renderizador | Instala un driver propio (Turnip) en **Ajustes → Gráficos** y reinicia |
| El juego se siente más lento que 60 fps | El teléfono mantiene los núcleos grandes de la CPU por debajo de su frecuencia máxima | **Ajustes → Android → Poner el reloj al 100%** (necesita root), o el modo de juego del teléfono, o `adb shell cmd power set-fixed-performance-mode-enabled true` |
| Por encima de 60 fps la imagen no se siente más rápida | La pantalla es de 60 Hz: los cuadros extra se dibujan y no se ven | Usa un valor de 60 fps en una pantalla de 60 Hz; usa 120 fps en una de 120 Hz |
| El juego se pausa solo con cuadros altos | La guardia de calor: el teléfono está cerca de su límite térmico | Déjalo enfriar, o pon la guardia en *Relajada* (o *Apagada* si aceptas que dé tirones) |
| La preparación va muy lenta | El juego se compila en el teléfono | Déjala terminar; se puede pausar y reanudar sin riesgo |
| En el log no hay información térmica | El teléfono no expone el HAL de margen térmico | Desde la v1.0.5 se usa el estado térmico |
| Un teléfono de 32 bits o x86_64 no puede instalar el APK | Solo hay una compilación arm64-v8a | Usa un dispositivo arm64 |

## Tabla de compatibilidad

Esta tabla se llena con los informes que dejan los usuarios. Completa tu fila: abre un issue con
la plantilla de [_Informe de compatibilidad_](https://github.com/HUEVOMAN77/RedU/issues/new/choose).

| Dispositivo | Android | GPU / driver | Funciona | Calificación | fps | Notas |
| --- | --- | --- | --- | --- | --- | --- |
| HUAWEI NCO-LX3 (Nova 10) | 12 | Adreno 642L, Vulkan 1.1.128, 512.530.0 | Sí | 4/5 | 60 (120 con tope) | Verificado. Limitado por la CPU a cuadros altos. |

## Cómo funciona la calificación

| Calificación | Significado |
| --- | --- |
| 5/5 | Funciona perfecto: imagen correcta, sin errores, a la velocidad completa del dispositivo. |
| 4/5 | Funciona bien; una limitación menor (tasa de cuadros, un glitch gráfico pequeño). |
| 3/5 | Funciona, pero se nota limitado (lógica lenta, efectos que faltan). |
| 2/5 | Solo funciona con un driver propio, o con errores visibles. |
| 1/5 | No funciona. |

La calificación es sobre la experiencia en ese dispositivo, no sobre el precio o la potencia del
teléfono.
