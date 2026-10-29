# Ticks per seconds — Verse Boost
**Tema:** rendimiento de simulación, concurrencia cooperativa y reparto de trabajo en Verse.

> Documentación de las partes 1 y 2 de *Verse Boost* (Mikey Jensen) basada en la transcripción y capturas facilitadas. Las propuestas de aplicación al Aim Trainer son hipótesis de ingeniería, no implementaciones verificadas.

## Navegación

| Recurso | Función |
|---|---|
| **[Guía principal para agentes](knowledge/Ticks_Per_Second.md)** | Explicación, código conceptual, citas de origen, pruebas y reglas de implementación |
| [Diagramas técnicos](assets/README.md) | Cinco diagramas SVG explicados y enlazados desde la guía |
| [Inventario de capturas](assets/capture-notes.md) | Descripción, transcripción conceptual y ubicación de evidencias visuales |
| [Fuentes y trazabilidad](sources/README.md) | Material primario y documentación oficial de Epic |

## Conceptos esenciales

- `spawn` inicia tareas lógicas asíncronas: no es equivalente a crear hilos del sistema operativo.
- Las expresiones inmediatas muy costosas pueden bloquear otras tareas en el mismo contexto.
- `Sleep(0.0)` cede hasta la siguiente actualización, con semántica y restricciones de contexto suspendible.
- Repartir carga mediante lotes puede reducir picos, **pero no reduce automáticamente** el costo total.
- Los ~500 cálculos `Distance`, ~3 TPS y tiempos de la prueba son **observaciones del autor**, no límites universales.

## Uso sugerido para agentes

Lee primero [la guía completa](knowledge/Ticks_Per_Second.md) y sus diez reglas obligatorias (sección 8). Consulta los diagramas para comprender el flujo; la información crítica ya está transcrita en texto. Las imágenes creadas en este repositorio son ilustraciones técnicas, no pruebas ejecutadas localmente.

[Volver al índice general](../README.md)
