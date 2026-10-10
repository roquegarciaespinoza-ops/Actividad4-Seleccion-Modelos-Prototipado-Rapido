# Documentación técnica — Actividad 4

**Actividad 4. Selección de modelos y prototipado rápido**  
**Continuidad:** Fase I - Business Case - Unidad Habitacional TecMilenio.

Esta carpeta contiene **los documentos técnicos ya publicados**. Se ejecutaron tres modelos de reconocimiento óptico de caracteres (OCR, *Optical Character Recognition*) sobre 12 imágenes con referencias automáticas. Posteriormente se revisaron las 12 imágenes, se aceptaron diez referencias y se excluyeron dos regiones ilegibles. La segunda evaluación sigue siendo una muestra limitada.

## Documentos disponibles

| Documento | Propósito |
|---|---|
| [Caso de uso](caso_de_uso.md) | Problema, objetivos y límites del prototipo |
| [Auditoría de datasets](auditoria_datasets.md) | Selección y revisión previa de datos, incidencias y correcciones |
| [Selección de modelos](seleccion_modelos.md) | Candidatos, criterios técnicos y sustituciones |
| [Análisis comparativo](analisis_comparativo.md) | Exactitud, precisión, exhaustividad, F1, tasa de error por carácter y latencia |
| [Conclusiones](conclusiones.md) | Hallazgos, límites y deuda técnica |
| [Licencias, tamaños y recursos](licencias_recursos.md) | Características de pesos y restricciones del entorno | 
| [Revisión humana posterior](validacion_humana.md) | Revisión de 12 imágenes, exclusión de dos y métricas sobre diez | 
| [Decisión para la siguiente fase](decision_siguiente_fase.md) | Justificación para continuar con TrOCR Base Printed |
| [Auditoría de la rúbrica](auditoria_rubrica.md) | Evidencias publicadas y requisitos que necesitan validación adicional |

## Estado de la documentación

**Todos los documentos enumerados se encuentran incorporados en GitHub.** No hay documentos Markdown pendientes de carga de esta relación.

Los archivos ejecutables y las evidencias están organizados en [notebooks](../notebooks/), [datos](../data/) y [resultados](../results/).

## Limitaciones todavía abiertas

La existencia de todos los archivos no equivale a demostrar cada requisito al máximo nivel: la evaluación inicial usó etiquetas automáticas y la segunda evaluación incluyó diez referencias revisadas manualmente. Sigue pendiente una validación representativa de mayor tamaño, confirmar condiciones de licencia y medir memoria GPU. Estos puntos se mantienen como **limitaciones técnicas**, no como documentos faltantes.

**Candidato para la siguiente fase:** [TrOCR Base Printed](decision_siguiente_fase.md), seleccionado provisionalmente para continuar desarrollo y pruebas; no aprobado para producción.
