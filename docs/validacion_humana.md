# Revisión humana y comparación actualizada

## Propósito
Revisar las 12 imágenes originales de la **Actividad 4. Selección de modelos y prototipado rápido**, corregir etiquetas automáticas y recalcular las métricas reutilizando las predicciones de tres modelos de reconocimiento óptico de caracteres (OCR, *Optical Character Recognition*).

## Procedimiento
Las 12 imágenes se mostraron en Colab, se examinaron visualmente y el usuario confirmó las transcripciones de las matrículas de dos líneas. Se conservaron **10 referencias revisadas** y se excluyeron **2 regiones ilegibles**, registrando identificador y motivo. Se reutilizaron las 36 predicciones existentes, pero las métricas se recalcularon únicamente sobre las **30 predicciones correspondientes a los diez registros aceptados**.

La CELDA 17 generó archivos locales para referencias y exclusiones, pero **no se pudieron publicar sus valores individuales en el repositorio público**. La tabla agregada `results/metricas_verificadas.csv` sí está publicada con los resultados mostrados por la CELDA 17. Para reproducir cada cifra exacta sobre las predicciones debe ejecutarse la CELDA 17 con `results/predicciones_detalle.csv`.

## Resultado sobre diez referencias revisadas

| Modelo | Exactitud matrícula | Precisión de caracteres | Recall | F1 | CER | Latencia media |
|---|---:|---:|---:|---:|---:|---:|
| TrOCR Base Printed | **70.00 %** | **90.67 %** | **82.22 %** | **85.33 %** | **20.00 %** | 120.9 ms |
| TrOCR Small Printed | 60.00 % | 83.00 % | 73.33 % | 75.87 % | 26.67 % | 60.0 ms |
| TrOCR Small Handwritten | 0.00 % | 2.02 % | 2.50 % | 2.23 % | 106.25 % | 45.6 ms |

CER (*Character Error Rate*) es la tasa de error por carácter, donde un valor más bajo es preferible. Las métricas de caracteres se calcularon mediante alineación de cadenas y promedio por imagen, no como clasificación binaria convencional.

## Dictamen
**TrOCR Base Printed permanece como modelo de continuidad para la siguiente fase.** Fue el de mejor coincidencia exacta con referencias revisadas (7 de 10) y mejor puntuación F1, con una latencia aproximada del doble de TrOCR Small Printed.

## Límites
La verificación es manual y acotada a diez matrículas; no representa un muestreo estadístico amplio, no prueba el 97 % objetivo del caso de negocio y no equivale a garantía de reconocimiento en producción. Los valores previos sobre doce etiquetas automáticas se preservan como evidencia histórica; **no se sustituyen ni borran**.

**Nota de trazabilidad:** esta tabla reproduce el resultado compartido de la CELDA 17. El archivo de detalle recalculado directamente en Colab (`predicciones_verificadas.csv`) se incorporará cuando esté disponible; no se debe afirmar que ya está publicado.
