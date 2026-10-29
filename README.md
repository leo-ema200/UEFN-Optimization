# UEFN Optimization

Biblioteca técnica modular de **optimización y buenas prácticas en UEFN / Verse**, organizada por temas para desarrolladores y agentes de IA.

> **Principio editorial:** documentar evidencias, código y recomendaciones por separado; una demostración de terceros no se presenta como límite oficial de Epic Games ni como prueba ejecutada en nuestro proyecto.

## Temas disponibles

| Tema | Contenido | Documentación |
|---|---|---|
| **Ticks per seconds** | Concurrencia en Verse, presupuesto de simulación, `Sleep(0.0)`, reparto de trabajo, pruebas y aplicación al Aim Trainer | [Abrir tema](./Ticks%20per%20seconds/README.md) |

## Convención de cada tema

Cada tema tiene su **propio directorio padre**, un archivo `README.md` que sirve de índice y subcarpetas que separan conocimiento para agentes, recursos visuales y fuentes. Los materiales no se mezclan entre temas.

```text
UEFN-Optimization/
├── README.md                      # Índice general
└── Ticks per seconds/
    ├── README.md                  # Navegación del tema
    ├── knowledge/
    │   └── Ticks_Per_Second.md   # Base principal para agentes
    ├── assets/
    │   ├── README.md             # Inventario y explicación de recursos
    │   └── diagrams/             # Diagramas visuales autocontenidos
    └── sources/
        └── README.md             # Procedencia y límites
```

## Para agentes de IA

1. Localiza el tema desde este índice.
2. Lee la guía completa y sus convenciones de trazabilidad.
3. Usa las imágenes como evidencia complementaria, **no como sustituto** de explicaciones y fragmentos de código seleccionables.
4. Distingue claramente `[VIDEO]`, `[EPIC]`, `[APLICACIÓN]` y `[NO VERIFICADO]`.
5. No afirmes que se han ejecutado optimizaciones o benchmarks salvo que exista evidencia reproducible.

> Los siguientes temas se incorporarán como carpetas hermanas de `Ticks per seconds/`, sin alterar la estructura de los existentes.
