# Verificación de tamaños, licencias y recursos

## Propósito

Complemento de la **Actividad 4. Selección de modelos y prototipado rápido**, centrado en comparar el tamaño de los modelos preentrenados de reconocimiento óptico de caracteres (OCR, *Optical Character Recognition*), condiciones de uso y recursos experimentales. GPU significa *Graphics Processing Unit* (unidad de procesamiento gráfico).

## Características de los modelos

| Modelo | Tamaño de pesos publicado/observado | Parámetros según Hugging Face | Especialización | Licencia |
|---|---:|---:|---|---|
| TrOCR Small Printed | ~246 MB (archivo descargado en Colab) | 61.4 millones | Texto impreso | No declarada en metadatos consultados; confirmar términos antes de redistribuir pesos |
| TrOCR Base Printed | ~1.33 GB (archivo descargado en Colab) | ~0.3 mil millones | Texto impreso | No declarada en metadatos consultados; confirmar términos antes de redistribuir pesos |
| TrOCR Small Handwritten | ~246 MB (archivo descargado en Colab) | No constatados aquí con ficha consultada | Texto manuscrito | No declarada en metadatos; existe discusión pública solicitando aclaración |

**Importante:** son tamaños aproximados de *archivos de pesos* y cantidades reportadas en fichas, no medidas de memoria de video consumida durante inferencia. La memoria efectiva depende también de precisión numérica, carga del procesador, tensores de imagen, librerías y caché. Tampoco son costos de operación.

### Evidencia de fuentes

- [TrOCR Small Printed: ficha de Hugging Face](https://huggingface.co/microsoft/trocr-small-printed)
- [TrOCR Base Printed: ficha de Hugging Face](https://huggingface.co/microsoft/trocr-base-printed)
- [TrOCR Base Printed: archivos del repositorio](https://huggingface.co/microsoft/trocr-base-printed/tree/main)
- [TrOCR Small Handwritten: discusión sobre licencia](https://huggingface.co/microsoft/trocr-small-handwritten/discussions/9)

**No se atribuye la licencia MIT del repositorio general de código TrOCR a estos pesos** sin confirmación explícita. Los modelos se descargaron para prototipado, pero el repositorio GitHub no redistribuye sus pesos.

## Recursos experimentales observados

- Plataforma: Google Colab.
- GPU disponible y utilizada para los modelos: **Tesla T4**.
- PyTorch reportado: **2.11.0+cu130**; Transformers: **4.57.6**; Datasets: **3.6.0**.
- Tres modelos ejecutados secuencialmente, procesando **una imagen por inferencia**.
- Muestra experimental: 12 recortes por modelo, semillas de selección y configuración en los notebooks.
- Tiempos de carga registrados: Small Printed **12.52 s**, Base Printed **13.54 s**, Small Handwritten **5.90 s**.
- Latencia media por imagen: **0.0562 s**, **0.1137 s**, **0.0441 s**, respectivamente.
- **No se registró el pico de memoria GPU ni el consumo económico**; por eso no se fabrican dichos valores.

## Decisión para la siguiente fase

TrOCR Base Printed mostró mejores métricas exploratorias sobre referencias automáticas, pese a una mayor latencia y pesos más grandes. La decisión de continuar con él es **provisional**. Antes de desplegarlo deben medirse memoria GPU, latencia de extremo a extremo y consumo bajo demanda real, además de verificar las condiciones de licencia.

## Trabajo mínimo pendiente

1. En una sesión de Colab con los modelos, medir la memoria GPU antes/después y el pico usando `torch.cuda.reset_peak_memory_stats()` y `torch.cuda.max_memory_allocated()` durante la inferencia; publicar resultados originales, no aproximaciones.
2. Solicitar o confirmar condiciones de uso de los pesos si se plantea redistribución o uso productivo.
3. Construir una pequeña evaluación con etiquetas humanas verificadas antes de declarar precisión operativa.

La ausencia de estas mediciones se reporta explícitamente como **deuda técnica**, no como un requisito ya completado.
