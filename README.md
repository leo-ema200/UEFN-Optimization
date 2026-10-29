# UEFN Optimization

Biblioteca técnica modular de **optimización y buenas prácticas en UEFN / Verse**, organizada por temas para desarrolladores y agentes de IA.

> **Principio editorial:** documentar evidencias, código y recomendaciones por separado; una demostración de terceros no se presenta como límite oficial de Epic Games ni como prueba ejecutada en nuestro proyecto.

## Temas disponibles

| Tema | Contenido | Documentación |
|---|---|---|
| **Ticks per seconds** | Concurrencia en Verse, presupuesto de simulación, `Sleep(0.0)`, reparto de trabajo, pruebas y aplicación al Aim Trainer | [Abrir tema](./Ticks%20per%20seconds/README.md) |
| **How to make your arrays 100x Faster** | Construcción eficiente con `for`, costos de copias y `Slice`, pools reutilizables con `FreeIndex`, pruebas y aplicación al Aim Trainer | [Abrir tema](./How%20to%20make%20your%20arrays%20100x%20Faster/README.md) |

## Convención de cada tema

Cada tema tiene su **propio directorio padre**, un archivo `README.md` que sirve de índice y subcarpetas que separan conocimiento para agentes, recursos visuales y fuentes. Los materiales no se mezclan entre temas.

```text
UEFN-Optimization/
├── README.md                              # Índice general
├── Ticks per seconds/
│   ├── README.md                          # Índice del tema
│   ├── knowledge/
│   │   └── Ticks_Per_Second.md            # Guía para agentes
│   ├── assets/
│   │   ├── README.md
│   │   ├── capture-notes.md
│   │   └── diagrams/                      # 5 diagramas SVG
│   └── sources/
│       └── README.md
└── How to make your arrays 100x Faster/
    ├── README.md                          # Índice del tema
    ├── knowledge/
    │   └── Arrays_100x_Faster.md          # Guía para agentes
    ├── assets/
    │   ├── README.md
    │   └── diagrams/                      # 4 diagramas SVG
    └── sources/
        └── README.md
```

## Para agentes de IA

1. Localiza el tema desde este índice.
2. Lee la guía completa y sus convenciones de trazabilidad.
3. Usa las imágenes como evidencia complementaria, **no como sustituto** de explicaciones y fragmentos de código seleccionables.
4. Distingue claramente `[VIDEO]`, `[EPIC]`, `[APLICACIÓN]` y `[NO VERIFICADO]`.
5. No afirmes que se han ejecutado optimizaciones o benchmarks salvo que exista evidencia reproducible.

> Los próximos temas se añadirán como carpetas independientes al mismo nivel, y **cada tema nuevo deberá registrarse tanto en la tabla «Temas disponibles» como en este árbol de navegación**, sin alterar la documentación existente.
