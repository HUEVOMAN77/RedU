# Changelog

Todos los cambios visibles de **RedU**, el port para Android de *New Super Mario Bros. U* mantenido
por HUEVOMAN77 a partir de [nsmbu-recomp](https://github.com/nsmbu-recomp/nsmbu-recomp).

El formato sigue [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/). Los cambios del
proyecto original están en su propio historial.

## [1.0.5] - 2026-11-09

Primera versión publicada en este repositorio, y la primera pública que incluye el arreglo del
enlace en el teléfono.

### Added

- Los ajustes tienen un botón nuevo para poner el reloj del teléfono al 100%, y explican cómo
  dejarlo así en un teléfono sin root (modo de juego del teléfono o
  `adb shell cmd power set-fixed-performance-mode-enabled true`).

### Changed

- Los ajustes avisan cuando los cuadros por segundo están por encima de los de la pantalla: esas
  imágenes nunca se ven y le roban la GPU al juego.
- Los ajustes explican que se puede instalar un driver Vulkan propio (Turnip) para el Adreno, que
  arregla errores gráficos y puede ir más rápido.
- La guardia de calor ahora lee el estado térmico del teléfono cuando este no informa cuánto
  margen térmico queda: antes no pausaba nunca.

### Fixed

- La preparación ya no se cae al enlazar el juego en el teléfono: la app le pasaba al enlazador una
  opción vieja de Android y el proceso moría al final de la compilación.

## [1.0.4] - 2026-11-08

Versión de prueba interna, nunca publicada. Sus cambios están en la 1.0.5.

### Fixed

- La preparación ya no se cae al enlazar el juego en el teléfono.

## [1.0.3] - 2026-11-08

### Fixed

- La preparación ya no se cierra sola al empezar: la app usaba funciones que solo existen en
  Android 11 y en Android 13, así que en Android 10, 11 y 12 el proceso se caía al abrir el juego y
  la app se quedaba sin poder volver a entrar.

### Changed

- La compilación del juego usa hasta cuatro compiladores a la vez en vez de dos, así que el
  teléfono termina antes.

## [1.0.2] - 2026-11-08

### Fixed

- El compilador que instala la app ya arranca en Android 10, 11 y 12: usaba una función que solo
  existe en Android 13, y el sistema lo cerraba al abrirlo.

## [1.0.1] - 2026-11-08

### Fixed

- La app ya se instala en Android 10 y superior. Antes pedía Android 13, así que el teléfono
  rechazaba el paquete con un error al analizarlo.
- El juego ya se puede instalar en un teléfono con Vulkan 1.1: la app no lo bloquea al instalarse,
  aunque para correr el juego hace falta el driver con Vulkan 1.3 (Ajustes → Gráficos →
  Controlador de GPU).
- La preparación ya no se reinicia una y otra vez: cuando Android termina el proceso, la app retoma
  la compilación desde lo que ya estaba compilado y el avance vuelve al porcentaje real, en vez de
  arrancar de nuevo en 1 %.
- La compilación usa menos compiladores a la vez, para que el teléfono no se quede sin memoria a
  mitad del trabajo.
- Cuando la preparación no puede terminar, la app dice el motivo del fallo y cuántas veces se
  interrumpió.

## [1.0.0] - 2026-11-08

Primera versión de **RedU**, el port del juego a Android hecho por HUEVOMAN77.

### Added

- La app para Android en español latinoamericano por defecto: el asistente de preparación, los
  diálogos, los avisos, las notificaciones y los mensajes de error. El inglés queda como respaldo.
- El menú del juego (la superposición de ajustes) en español: pestañas, botones, textos de ayuda,
  la tabla de controles, los nombres de teclas y de botones, y los avisos de guardado y de carga.
- Un ícono propio de **RedU**, con su versión adaptable y las imágenes para todas las densidades de
  pantalla. Es un diseño provisional.

### Changed

- La app ahora se llama **RedU**. Es una app distinta de la anterior, así que se instala al lado y
  no la reemplaza.
- En Android el mezclado de sonido ya no compite con el juego por los núcleos rápidos: en los
  teléfonos con núcleos grandes y chicos (como el Snapdragon 778G del Huawei Nova 10) el juego va
  más fluido.
- El juego se compila para la arquitectura del teléfono (ARMv8.2-A, los núcleos A78) en vez de la
  versión genérica de 64 bits: rinde un poco más en los teléfonos de 2020 en adelante.
