# How to make your arrays 100x Faster

Segundo tema de **UEFN-Optimization**. Esta carpeta es hermana de `Ticks per seconds/`, con conocimiento, recursos gráficos y trazabilidad independientes.

**Documentación:**

- [Guía técnica completa para agentes](knowledge/Arrays_100x_Faster.md) — 10 secciones, código, mediciones atribuidas, checklist y 13 capturas descritas.
- [Diagramas editoriales](assets/README.md) — cuatro SVG enlazados desde el Markdown.
- [Fuentes y limitaciones](sources/README.md) — documentación oficial de Epic y límites del material.
- [Índice general](../README.md).

> El Word premium (14 páginas), el documento fuente y las 13 capturas PNG están en el ZIP completo entregado al usuario. Los archivos binarios no se han transferido al repositorio. El Markdown conserva la descripción de cada captura para que el agente pueda comprender la demostración sin necesidad de interpretar los píxeles.

## Hallazgos

1. La comprensión `for` genera un array final sin concatenaciones por elemento.
2. El `Slice` repetido para un pool grande puede ser caro en el caso medido.
3. Un cursor lógico `FreeIndex` evita reconstrucciones repetitivas si el pool tiene invariantes de seguridad.
4. **100× es el título de una prueba concreta**, no una garantía universal de rendimiento.

## Estado

Documentación: publicada. Pruebas dentro del Aim Trainer: pendientes. Código completo del retorno final del pool: no disponible en el archivo recibido.
