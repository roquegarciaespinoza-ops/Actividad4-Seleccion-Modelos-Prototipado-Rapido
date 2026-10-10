# Selección y sustitución de modelos

## Criterios de elección
Se establecieron como criterios: correspondencia con la tarea OCR (*Optical Character Recognition*, reconocimiento óptico de caracteres), disponibilidad en Hugging Face, compatibilidad con Google Colab y GPU (*Graphics Processing Unit*, unidad de procesamiento gráfico), dependencia de código externo, tiempo de inferencia, desempeño sobre una muestra común, tamaño de los pesos y condiciones de licencia.

## Modelos ejecutados
| Modelo | Identificador | Papel |
|---|---|---|
| TrOCR Small Printed | `microsoft/trocr-small-printed` | Modelo ligero de texto impreso |
| TrOCR Base Printed | `microsoft/trocr-base-printed` | Comparación con un modelo de mayor tamaño |
| TrOCR Small Handwritten | `microsoft/trocr-small-handwritten` | Prueba de transferencia fuera de dominio: texto manuscrito aplicado a matrículas impresas |

Los tres modelos pertenecen a la familia TrOCR. La comparación cubre **tres modelos diferentes, pero no tres familias arquitectónicas distintas**.

## Cambios durante el prototipado
El candidato `DunnBC22/trocr-base-printed_license_plates_ocr`, específico de placas, devolvió **HTTP 401 (acceso no autorizado)** tanto al consultar metadatos como al recuperar directamente su configuración desde Colab. Aunque el origen público puede existir, no fue accesible en esa sesión; se sustituyó por TrOCR Base Printed.

GOT-OCR 2.0 se consultó como alternativa de otra arquitectura, pero su ejecución requería habilitar código remoto personalizado mediante `trust_remote_code=True`. Por decisión de seguridad y tiempo **no se habilitó ni se contabilizó como implementado**. Se sustituyó por TrOCR Small Handwritten, compatible con el mismo flujo de inferencia.

## Metadatos
En la consulta del Hub, GOT-OCR mostraba licencia Apache 2.0. Las fichas de los modelos TrOCR no devolvieron licencia declarada a través del campo consultado. Esto **no demuestra ausencia de licencia**; exige revisión de las fichas oficiales y de los modelos base antes de redistribuir recursos.

## Decisión provisional
TrOCR Base Printed ofrece la mejor calidad **exploratoria** en la muestra de 12 imágenes no verificadas. TrOCR Small Printed ofrece menor latencia. TrOCR Small Handwritten muestra problemas evidentes al aplicarse fuera de su dominio de entrenamiento.

La selección final queda condicionada a repetir la evaluación sobre transcripciones humanas verificadas y una muestra representativa.
