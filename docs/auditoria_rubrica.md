# Auditoría final contra las instrucciones y rúbrica

## Alcance
**Actividad 4. Selección de modelos y prototipado rápido**, continuidad de Fase I - Business Case - Unidad Habitacional TecMilenio.

Se revisaron las instrucciones compartidas: notebook funcional, comparación de al menos tres modelos, métricas de exactitud (*accuracy*), precisión (*precision*), exhaustividad (*recall*) y F1, latencia, documentación, dataset y repositorio. Se adopta la indicación posterior del profesor de depositar los entregables **directamente en GitHub**, en lugar de generar Word, PDF o Excel. OCR significa *Optical Character Recognition* (reconocimiento óptico de caracteres); GPU significa *Graphics Processing Unit* (unidad de procesamiento gráfico); CSV significa *Comma-Separated Values* (valores separados por comas).

La tabla usa la distribución de 25 puntos por criterio descrita en la revisión de la rúbrica. **No es una calificación del profesor ni una promesa de 100 puntos.**

| Criterio (25 puntos cada uno) | Evidencia publicada | Estado y brecha |
|---|---|---|
| Selección y análisis de modelos | `docs/seleccion_modelos.md`, `docs/auditoria_datasets.md`, `docs/decision_siguiente_fase.md`, `results/fichas_modelos.csv` | **Parcial alto**: tres candidatos ejecutados y sustituciones justificadas; tamaños de pesos y situación de licencias documentados en `docs/licencias_recursos.md`; falta confirmar permisos concretos y medición de memoria GPU, además de ampliar el componente Spaces del ecosistema |
| Implementación en Colab | `notebooks/Actividad4_Comparacion_Modelos_OCR.ipynb`, `requirements.txt`, `results/estado_modelos.csv` | **Implementado con reservas**: tres modelos en estado OK sobre GPU Tesla T4; no se conserva una ejecución independiente reproducida desde cero en otra sesión y deben revisarse dependencias inestables |
| Evaluación del desempeño | `results/metricas_resumen.csv`, `results/predicciones_detalle.csv`, `docs/analisis_comparativo.md` | **Dos evaluaciones disponibles**: 12 referencias automáticas y diez revisadas manualmente, cuatro métricas y latencia; falta tamaño muestral representativo, archivo de detalle de la segunda ejecución y medición de memoria GPU |
| Documentación y justificación | README principal, cinco documentos técnicos, decisión de siguiente fase, tres notebooks, CSV y archivos de soporte | **Mayormente cubierto**: estructura y narrativa publicadas; persisten limitaciones de dataset, licencias, entorno y evidencias de ejecución sin salidas visuales por permisos |

## Lista de comprobación de las instrucciones

| Requisito | Evidencia / observación |
|---|---|
| Rama de inteligencia artificial y caso de uso | Visión computacional aplicada a reconocimiento de matrículas; `docs/caso_de_uso.md` |
| GPU, instalación y dependencias | Capturas revisadas y notebooks; `requirements.txt` |
| Autenticación en Hugging Face Hub | Celda con lectura opcional de token desde secretos de Colab; no se publicaron tokens |
| Carga de modelos y datasets | Notebooks de auditoría y comparación |
| Pipeline de inferencia | Tres TrOCR ejecutados y 36 predicciones registradas |
| Accuracy, precision, recall, F1 | `results/metricas_resumen.csv` y notebook |
| Latencia | Media y mediana por modelo en CSV; condiciones limitadas a Colab |
| Tablas, resúmenes y conclusiones parciales | Notebook y documentación en Markdown |
| Descripción, origen y estructura del dataset | `docs/auditoria_datasets.md`, `data/README.md`, `data/muestra_evaluada.csv` |
| Comparación de tarea, tamaño, licencia, precisión, latencia, recursos | **Parcial**: precisión y latencia sí; tamaño/licencias/memoria requieren consolidación documentada |
| Análisis de eficiencia frente a precisión | `docs/analisis_comparativo.md`, `docs/decision_siguiente_fase.md` |
| Ajustes mínimos y limitaciones | Normalización/recorte, sustitución de modelos y deuda técnica documentados; sin ajuste fino |
| Recomendación del modelo | TrOCR Base Printed para continuar fase de desarrollo, con condiciones claras |
| GitHub: README, entorno, ejecución, conclusiones, archivos de soporte | Archivos principales publicados; `src/` reservado, sin script independiente |
| Documento Word / archivo Excel / ZIP como entrega | No se generan por decisión posterior del profesor: GitHub y formatos `.md`, `.ipynb` y `.csv` |

## Riesgos para la evaluación académica

1. **Validación humana todavía insuficiente:** se revisaron doce imágenes, se aceptaron diez y se excluyeron dos; no reclamar cumplimiento de 97 % ni representatividad del escenario real.
2. **Muestra de solo doce imágenes:** los porcentajes tienen alta incertidumbre, y algunas referencias parecen textos ajenos a matrículas.
3. **Modelos de una misma familia:** se implementaron tres modelos distintos, pero dos de texto impreso y uno de manuscrito; comparación limitada de arquitecturas.
4. **Licencias y recursos incompletos:** falta consolidar tamaños exactos de los modelos, memoria máxima GPU y condiciones de uso de los pesos.
5. **Reproducción fuera de la sesión original:** las rutas `/content/` son temporales; las imágenes no fueron publicadas y los notebooks publicados retiraron algunas salidas visuales.

## Dictamen académico interno

La **implementación y documentación están sustancialmente avanzadas**. No sería riguroso afirmar que la actividad ya demuestra el 100 % de la rúbrica. Si solo se pueden atender uno o dos puntos antes de entregar, priorizar (1) ampliar la muestra revisada y guardar el detalle original de la CELDA 17 y (2) medir memoria GPU y confirmar licencias de uso de los pesos. La muestra de diez referencias ya fue revisada pero no resulta estadísticamente representativa.

La conclusión ejecutiva de continuidad se encuentra en `docs/decision_siguiente_fase.md`: **TrOCR Base Printed** es el candidato provisional para la fase siguiente, con TrOCR Small Printed como alternativa de respaldo.
