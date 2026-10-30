# Cálculo por componentes y preparación de movimiento: caso MOV-002

Fecha local: 2026-10-29, Guatemala. Logs finales: 2026-10-30 UTC.
Clasificación: **[APLICACIÓN]** medidas del proyecto AimTrainer_2; **[ANÁLISIS]**
interpretación; **[NO VERIFICADO]** costes universales internos de la VM.

## Resultado comprobado

MOV-002 tardaba hasta 45.87 s de simulación preparando una ruta Dash. Las últimas
runs revisadas tardan 2.14–3.12 s más ~0.10 s de arranque y la llamada nativa.
El ahorro combina cinco cambios. No es un benchmark aislado vector3 contra float
ni permite prometer un factor fijo para todos los proyectos/funciones.

El usuario aprobó visualmente la suavidad. Siete variantes mantienen puntos/tiempos
en 252 casos de transcripción, incluidos fallos heredados. Las tres Dash cambian
el muestreo: unos 7800–11161 frames pasan a 3100 en las rutas probadas de ~31 s,
usando ticks 0.01 s más fronteras. Es una aproximación aprobada; máximos medidos
0.0742, 0.4890 y 1.1577 cm en los casos del informe, no solo medias submilimétricas.

## 1. Evitar valores vectoriales intermedios en bucles calientes

El cálculo original por muestra hacía:

```verse
Point := S.A * Weight.A + S.B * Weight.B + S.C * Weight.C + S.D * Weight.D
set ArcSum += Mov002Norm(Point - Previous)
```

La versión escalar mantiene el orden de productos y sumas para X, Y y Z:

```verse
X := S.A.X * Weight.A + S.B.X * Weight.B + S.C.X * Weight.C + S.D.X * Weight.D
# Repetir la misma expresión para Y y Z.
DX := X - PreviousX
DY := Y - PreviousY
DZ := Z - PreviousZ
set ArcSum += Sqrt(DX * DX + DY * DY + DZ * DZ)
```

Fragmentos explicativos; sus variables pertenecen al bucle completo del fuente.
Se evitan los vector3 intermedios, no todas las estructuras vector3: la API y la
salida siguen usándolas. Se mantienen las 100 muestras y su suma. MeasureScalar
coincidió con Measure en 2000 curvas de la transcripción; helpers en 5000 casos.
No reordenar álgebra: (C.X - B.X*2.0) + A.X no garantiza el mismo redondeo que
A.X + C.X - 2.0*B.X. No reemplazar funciones nativas por aproximaciones en Verse.

**Límite de evidencia:** no hay un microbenchmark nativo aislado archivado que
pruebe «vector3 cuesta 10×». La mejora combinada sí está respaldada por logs.
El impacto del coste de temporales debe medirse por bloque/entorno antes de aplicar
esta técnica a todo un proyecto.

## 2. Construcción plana de arrays

SampleCurvesFlat y RetimeFlat usan una comprensión/cursor para emitir el resultado,
en vez de crear miles de arrays pequeños y unirlos con Concatenate. Esto conserva
el orden y permite repartir trabajo. No prohíbe toda concatenación pequeña ni
implica que cualquier `.Length` haga una copia. Leer el tema de arrays y medir.

## 3. Ceder por trabajo contado

FastYield acumula unidades aproximadas, con 1500 como presupuesto de MOV-002.
Incluye evaluación, construcción, copias y cierre de listas. Sleep(0.0) cede hasta
otra actualización; no tiene duración fija. Quitar cesiones puede bloquear; añadir
demasiadas aumenta latencia. Medir tiempo de carga, picos y respuesta simultáneamente.
La preparación final cede cada 256 frames en este caso. No copiar esos números sin
comprobarlos en la familia destino. El reloj de simulación no mide CPU intra-tick.

## 4. Densidad y transmisión de keyframes

Con carga inicial en este proyecto hubo fallos de conexión al ejecutar Play con
7791 frames, mientras 7400 funcionaron; cargas incrementales dieron resultados
distintos. **No es un límite oficial de Epic ni una garantía bajo 7000.**
PrepareOnly y LoadOnly permitieron separar cálculo/carga de reproducción.
El muestreo temporal de 0.01 s fue aprobado para Dash después de comparar rutas.
No imponerlo como mínimo a cualquier familia ni usarlo para compensar fallos de pausa.
El objetivo sigue siendo fidelidad visual; cuantificar máximos, medias, velocidades,
fases y seguridad de cada segmento antes de reducir muestras.

## 5. Arranque

Tras preparar, MOV-002 espera tres ticks consecutivos <=45 ms, con una ventana de
0.6 s comprobada al reanudarse. Un tick bloqueado puede excederla. No se espera
entre vueltas; la animación es Linear/PingPong nativa y continua. La espera inicial
debe contabilizarse aparte del total de preparación; no arregla una carga pesada.

## Reproducir y leer los resultados

Fuentes y checks: [MOV-002](https://github.com/leo-ema200/MovementSystem-2.0/tree/main/families/MOV-002).
`check_fast_preparation.py` compara rutas/funciones; `profile_preparation_work.py`
cuenta operaciones y cesiones, no TPS. `analyze_tracking_logs.py` lee logs nativos;
su prefijo actual es MOV-002 y debe adaptarse para otra familia.

[Informe numérico](../evidence/review_fast_preparation_report.json),
[runs sanitizadas](../evidence/review_native_runs.json),
[hashes del código](../evidence/review_source_manifest.json).
Los logs se analizaron de nuevo en esta revisión; no se ejecutó otra sesión de juego.
Sin aviso TPS no equivale a 30 TPS garantizados: el monitor solo registra valores
bajos y puede faltar telemetría. «Sin avisos» significa que el parser no encontró
los patrones buscados en la ventana analizada, no ausencia probada de todo problema.

## Reglas para agentes

Mantener baseline, mismas seeds/opciones, orden RNG y estados por target. Separar
equivalencia exacta de resampling aprobado. No afirmar rendimiento a partir de Python.
Conservar bounds/exclusión de segmentos completos y los fallos heredados documentados.
No usar benchmarks de otro proyecto como garantía. Si la técnica cambia la trayectoria,
necesita error medido y aceptación visual; mejorar arranque no justifica perder suavidad.

Comparación ampliada reproducida durante la revisión: tres seeds exitosas por preset
en el HTML. En Dash, máximos entre las polilíneas de 0.0744 cm (Rumbo), 0.6767 cm
(Desvíos) y 1.4536 cm (Cambios rápidos) para esas seeds; no son cotas universales.
Informe adicional: `review_visual_comparison.json`. El visualizador omite rutas cuyo
baseline falla; los checks de equivalencia y la lista de limitaciones conservan esos casos.
