# Capturas del material original — inventario técnico

La fuente primaria es `Ticks Per Seconds.docx`, entregada por el usuario con diez imágenes relevantes extraídas de dos videos de *Verse Boost*. Este registro **no reemplaza los píxeles originales**; su objetivo es que el agente pueda comprender sin visión el contenido que demuestran las capturas. Las capturas originales están incluidas en los archivos DOCX entregados en la conversación, todavía no incorporados como binarios al repositorio.

| Captura | Ubicación aproximada en el Word fuente | Contenido técnico visible | Interpretación |
|---|---|---|---|
| 01 | Parte 1, p. 1 | Función de prueba que inicia tareas y un bucle de trabajo inmediato | El bucle grande puede retener el game thread |
| 02 | Parte 1, p. 2 | Función `ImmediateWorkTask`: múltiples cálculos `Distance` y `Print` | Trabajo sin cesión voluntaria |
| 03 | Parte 1, p. 11 | Log: inicios de unas diez tareas | Inicio antes del bucle intensivo |
| 04 | Parte 1, p. 11 | Log: valores de distancia repetidos | Evidencia del bloque inmediato |
| 05 | Parte 1, p. 11 | Log: tareas informan ~9,9 s reales y ~1,2 s simulados | Diferencia de tiempo observado, específica de esa sesión |
| 06 | Parte 2, p. 14 | Código de un trabajo inmediato | Finalización dentro del update actual |
| 07 | Parte 2, p. 14 | Ejemplos `MoveTo`, `Await` y `Sleep` | Expresiones potencialmente suspendibles |
| 08 | Parte 2, p. 18 | Captura de la documentación de `Sleep` | `Sleep(0.0)` cede al siguiente update |
| 09 | Parte 2, p. 20 | Diapositiva: ~500 cálculos `Distance` y TPS bajo 30 | Caso empírico, **no cuota ni límite fijo** |
| 10 | Parte 2, p. 23 | Código de gestor de spawners con `VEHICLES_MANAGED_PER_TICK` y `Sleep(0.0)` | Ejemplo de batching, no equivalente a optimizar todo spawn |

## Pseudocódigo textual de las imágenes

**Carga inmediata:**

```text
iniciar tareas con spawn
cada tarea espera Sleep(1.0)
repetir muchas operaciones Distance sin suspender
observar que las tareas pendientes avanzan cuando termina el bloque
```

**Gestor por lotes (Parte 2):**

```text
para cada spawner pendiente:
    administrar spawner
    incrementar contador
    si contador modulo VEHICLES_MANAGED_PER_TICK == 0:
        Sleep(0.0)
```

**Importante:** los ejemplos anteriores son reconstrucciones conceptuales, **no código original del autor ni fragmentos garantizados compilables**.

[Índice visual](README.md) · [Guía principal](../knowledge/Ticks_Per_Second.md)
