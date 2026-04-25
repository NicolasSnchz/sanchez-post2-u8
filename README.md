# sanchez-post2-u8

## Unidad 8 - Rendimiento, Optimización y Experiencia Fluida

Proyecto Flutter desarrollado para analizar problemas de rendimiento en una aplicación móvil usando Flutter DevTools, aislar operaciones pesadas con `compute()` y registrar trazas personalizadas con Firebase Performance Monitoring.

## Objetivo

Identificar jank provocado por procesamiento pesado en el main thread, medirlo con DevTools Timeline, optimizar el procesamiento usando un Isolate secundario con `compute()` y validar la mejora mediante capturas comparativas y registros en Logcat.

## Tecnologías usadas

- Flutter
- Dart
- Flutter DevTools
- Timeline Performance
- Isolates con `compute()`
- Firebase Performance Monitoring
- Android Studio
- Logcat

## Implementación

La aplicación simula la carga de un catálogo de productos generado en formato JSON.  
Primero se implementó una versión bloqueante donde el procesamiento del JSON se ejecuta directamente en el main thread, generando jank visible en la interfaz.

Después se optimizó el procesamiento usando `compute()`, moviendo el parseo del JSON a un Isolate secundario para evitar bloquear la UI.

Finalmente, se integró Firebase Performance Monitoring para registrar una traza personalizada llamada `catalog_load`, incluyendo la métrica `product_count`.

## Evidencias

### 1. Timeline antes de la optimización

Captura de Flutter DevTools mostrando frames rojos o amarillos durante la carga bloqueante del catálogo.

![Timeline antes](screenshots/timeline-before.png)

### 2. Timeline después de usar compute()

Captura de Flutter DevTools mostrando frames verdes luego de mover el procesamiento pesado a un Isolate con `compute()`.

![Timeline después](screenshots/timeline-after-compute.png)

### 3. Logcat con Firebase Performance

Captura de Logcat mostrando el registro de la traza personalizada `catalog_load` y la métrica `product_count`.

![Logcat Firebase](screenshots/logcat-firebase-trace.png)

## Commits realizados

- Agrega catálogo bloqueante para baseline
- Migra parse a Isolate con compute
- Integra Firebase Performance con traza personalizada

## Conclusión

La optimización con `compute()` permitió reducir el bloqueo del main thread durante el procesamiento del JSON. En la versión inicial se observaron frames con jank en Flutter DevTools, mientras que en la versión optimizada los frames se mantuvieron estables. Además, Firebase Performance permitió registrar la operación mediante una traza personalizada para validar el comportamiento de la aplicación.
