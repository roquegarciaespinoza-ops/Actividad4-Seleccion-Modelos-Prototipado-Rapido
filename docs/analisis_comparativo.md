# Análisis comparativo de modelos OCR

## Condiciones del experimento
Se utilizaron **12 recortes por modelo**, seleccionados con semilla 42 en Google Colab y procesados en una GPU Tesla T4. Se produjeron 36 predicciones. Los mismos identificadores de imagen fueron evaluados por los tres modelos.

La modalidad fue **EXPLORATORIA_ETIQUETAS_AUTOMATICAS**: las referencias no estaban verificadas manualmente. Por tanto, las métricas miden coincidencia con las etiquetas disponibles, **no el rendimiento real ante una verdad de referencia humana**.

## Resultados

| Métrica | TrOCR Base Printed | TrOCR Small Printed | TrOCR Small Handwritten |
|---|---:|---:|---:|
| Muestras | 12 | 12 | 12 |
| Exactitud de matrícula (*accuracy*) | 0.6667 | 0.5000 | 0.0000 |
| Precisión por caracteres (*precision*) | 0.8496 | 0.7333 | 0.0168 |
| Exhaustividad por caracteres (*recall*) | 0.8792 | 0.6806 | 0.0208 |
| Puntuación F1 (*F1-score*) | 0.8526 | 0.6955 | 0.0186 |
| Tasa de error por carácter (CER, *Character Error Rate*) | 0.2250 | 0.3403 | 1.0521 |
| Latencia media por imagen | 0.1137 s | 0.0562 s | 0.0441 s |
| Latencia mediana por imagen | 0.1224 s | 0.0557 s | 0.0420 s |
| Carga del modelo | 13.54 s | 12.52 s | 5.90 s |

Los tiempos se observaron en una sesión de Colab y **no representan el tiempo de apertura de la barrera**, la disponibilidad del servicio ni una garantía de latencia productiva.

## Interpretación de métricas
La exactitud por matrícula exige coincidencia completa después de normalizar caracteres alfanuméricos. Las medidas de precisión, exhaustividad y F1 se calcularon por matrícula a partir de una alineación por edición de caracteres y se promediaron entre ejemplos; no son una clasificación binaria convencional. CER corresponde a operaciones de sustitución, inserción y eliminación divididas por el número de caracteres de referencia; puede superar 1 cuando se generan muchas inserciones.

## Trade-offs: calidad y eficiencia
TrOCR Base presentó la mejor coincidencia con las referencias disponibles (8 de 12 matrículas), pero tardó cerca del doble por imagen que TrOCR Small Printed. TrOCR Small Printed coincidió exactamente en 6 de 12. TrOCR Small Handwritten obtuvo coincidencia exacta de 0 de 12; su menor latencia no compensa la inadecuación de su dominio.

En la evidencia de errores aparecen textos ajenos a matrículas como `TOTAL` o `-KEEP` y salidas no relacionadas con placas. Ello refuerza la necesidad de depurar las regiones y etiquetas antes de usar los resultados para decisiones de despliegue.

## Recomendación condicionada
**TrOCR Base Printed** es el candidato preliminar para continuar pruebas, no un ganador validado. Antes de recomendar implementación operativa es obligatorio contar con etiquetas verificadas, una muestra mayor y representativa, revisión de memoria GPU, licencias y pruebas de extremo a extremo.

## Restricciones de interpretación
El objetivo del caso de negocio de alcanzar el **97 %** de lecturas correctas no ha sido demostrado. Con doce ejemplos y anotaciones automáticas es imposible sustentar conclusiones sólidas sobre los falsos rechazos, la apertura de accesos o la calidad en matrículas mexicanas.
