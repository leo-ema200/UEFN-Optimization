# Fuentes y trazabilidad

## Fuente primaria

- Documento facilitado por el usuario: **Ticks Per Seconds.docx**, 27 páginas, transcripción en inglés de los videos *Verse Boost* partes 1 y 2, con diez capturas del código y resultados.
- Programador identificado por su propia introducción: **Mikey Jensen**.
- No se suministró URL ni fecha de publicación original: no inventar enlaces, títulos exactos ni versión UEFN del video.

## Referencias de Epic Games

- [Sleep — API de Verse](https://dev.epicgames.com/documentation/fortnite/verse-api/versedotorg/simulation/sleep?lang=en-US)
- [Debugging and Troubleshooting in Verse](https://dev.epicgames.com/documentation/fortnite/debugging-and-troubleshooting-in-verse)
- [Technical Performance in Fortnite](https://dev.epicgames.com/documentation/fortnite/technical-performance-in-fortnite)
- [Simulation update](https://dev.epicgames.com/documentation/en-us/fortnite/simulation-update)

## Límites de interpretación

- Las métricas 500 operaciones `Distance`, ~3 TPS y los tiempos 9,9/1,2 segundos son observaciones presentadas por el autor, no nuestros benchmarks.
- El valor 30 FPS de servidor / 33,3 ms se usa como referencia de presupuesto de servidor de Epic, no como promesa de un TPS medible idéntico en todas las situaciones.
- No afirmar que `spawn` crea un hilo nativo.
- No copiar de forma automática `Sleep(0.0)` a cualquier función: requiere contexto suspendible y respetar sincronización de gameplay.
- Los diagramas SVG enlazados en la guía son reconstrucciones editoriales, no las capturas originales.

[Volver al tema](../README.md)
