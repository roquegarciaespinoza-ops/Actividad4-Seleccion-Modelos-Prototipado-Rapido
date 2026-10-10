# Decisión técnica para la siguiente fase del proyecto

## Proyecto y objetivo de la decisión

Esta decisión forma parte de la **Actividad 4. Selección de modelos y prototipado rápido**, que da continuidad a la **Fase I - Business Case - Unidad Habitacional TecMilenio**. El objetivo del prototipo es reconocer las matrículas vehiculares para que, en una etapa posterior, el sistema pueda consultar un padrón de autorización. El reconocimiento de la matrícula no equivale por sí mismo a autorizar el acceso.

OCR significa *Optical Character Recognition* (reconocimiento óptico de caracteres). GPU significa *Graphics Processing Unit* (unidad de procesamiento gráfico).

## Modelo seleccionado para continuar el desarrollo

**Se selecciona TrOCR Base Printed (`microsoft/trocr-base-printed`) como modelo base para la siguiente fase de desarrollo y validación.** La elección es una **decisión provisional de ingeniería para continuar el proyecto**, no una certificación de rendimiento ni una aprobación para operar barreras vehiculares.

La decisión se apoya en que fue el modelo con mejor coincidencia con las etiquetas disponibles en el experimento realizado. Los resultados corresponden a 12 imágenes por modelo, 36 predicciones en total, en una misma sesión de Google Colab con GPU Tesla T4 y semilla 42. Las referencias son automáticas y **no fueron verificadas por completo por personas**.

| Indicador exploratorio | TrOCR Base Printed | TrOCR Small Printed | TrOCR Small Handwritten |
|---|---:|---:|---:|
| Matrículas que coincidieron exactamente con la referencia automática | 8/12 | 6/12 | 0/12 |
| Exactitud por matrícula | 66.67 % | 50.00 % | 0.00 % |
| Precisión por caracteres | 84.96 % | 73.33 % | 1.68 % |
| Exhaustividad por caracteres (*recall*) | 87.92 % | 68.06 % | 2.08 % |
| Puntuación F1 por caracteres | 85.26 % | 69.55 % | 1.86 % |
| CER (*Character Error Rate*, tasa de error por carácter; menor es mejor) | 22.50 % | 34.03 % | 105.21 % |
| Latencia media de inferencia | 113.7 ms | 56.2 ms | 44.1 ms |

La precisión, exhaustividad y F1 se calcularon mediante alineación de caracteres y promediando las métricas por matrícula; no son medidas estándar de clasificación binaria.

## Ratificación posterior con referencias revisadas

Tras revisar visualmente 12 imágenes, se aceptaron diez y se excluyeron dos por ilegibilidad. Sin volver a ejecutar los modelos, se recalcularon sus métricas sobre treinta predicciones existentes. TrOCR Base Printed obtuvo **70 % de exactitud de matrícula (7/10)**, **85.33 % de F1 por caracteres**, **20 % de CER** y **120.9 ms** de latencia media, frente a 60 % de exactitud, 75.87 % de F1 y 60.0 ms de latencia media para TrOCR Small Printed. **La selección de TrOCR Base Printed queda ratificada exclusivamente como candidato de desarrollo**. Diez matrículas no bastan para certificar el objetivo del 97 %. Ver [resultados revisados](validacion_humana.md).

## Justificación para una decisión de negocio

En control de acceso residencial, **la lectura correcta importa más que minimizar unas decenas de milisegundos de inferencia**, pues un número de placa equivocado puede generar rechazos indebidos o requerir revisión. Dentro de las restricciones de esta muestra, TrOCR Base Printed tuvo mejores indicadores de reconocimiento que las otras dos alternativas.

TrOCR Base Printed tardó aproximadamente el doble que TrOCR Small Printed (113.7 ms frente a 56.2 ms por imagen). Esa diferencia de unos **57.5 milisegundos** es un compromiso razonable **para continuar experimentando**, no una garantía de operación en tiempo real. Estos tiempos tampoco contemplan captura, detección de la matrícula, comunicaciones, consulta al padrón ni apertura física.

TrOCR Small Printed se conserva como **alternativa de respaldo** si en las siguientes pruebas la memoria disponible, el costo o la latencia total hacen inviable TrOCR Base. TrOCR Small Handwritten no se propone para continuidad debido a su especialización en texto manuscrito y su pobre coincidencia exploratoria con placas impresas.

## Qué demuestra y qué no demuestra esta actividad

**Demostrado:** los tres modelos se cargaron y ejecutaron inferencias; se registraron 36 predicciones sobre una misma muestra, métricas comparativas y latencias. Se identificaron problemas de calidad de datos, de acceso a un modelo especializado (HTTP 401, respuesta de acceso no autorizado) y requisitos de código remoto en otro candidato. Las sustituciones quedaron documentadas.

**No demostrado:** que TrOCR Base alcance el objetivo de **97 % de lectura correcta** fijado en la Fase I, que funcione de manera robusta con matrículas mexicanas, que su desempeño sea estadísticamente estable, que los datos no se solapen con los usados durante entrenamiento o que el sistema de control de acceso pueda operar de manera segura sin supervisión.

## Condiciones para avanzar a la siguiente fase

1. **Datos de referencia:** preparar un conjunto de matrículas verificadas manualmente, representativas de los formatos y condiciones del proyecto, con una separación clara entre desarrollo y evaluación.
2. **Validación comparativa:** repetir exactitud de matrícula, precisión, exhaustividad, F1, CER y latencia con referencias confiables; conservar TrOCR Small Printed como línea base.
3. **Adaptación mínima:** analizar normalización, recorte, orientación e iluminación antes de proponer ajuste fino (*fine-tuning*) del modelo; justificar cualquier entrenamiento adicional.
4. **Viabilidad:** documentar licencia de los pesos y del dataset, versión exacta de dependencias, consumo de memoria GPU, costos y condiciones para mantener el sistema.
5. **Integración segura:** añadir detección de placa en la escena, padrón de autorizaciones y manejo de excepciones. Un resultado de OCR no deberá activar por sí solo una barrera: la apertura dependerá de reglas de autorización y controles de seguridad.
6. **Punto de decisión:** si el modelo no se aproxima a los objetivos de negocio en una evaluación válida, reconsiderar el conjunto de datos, el preprocesamiento o modelos especializados en matrículas, antes de pasar a producción.

## Dictamen ejecutivo

> Con base en la auditoría de datos, la ejecución de tres modelos preentrenados y la comparación experimental realizada, se recomienda **continuar el desarrollo con TrOCR Base Printed**. Presentó la mejor coincidencia con las referencias disponibles, aunque requirió mayor tiempo de inferencia. Se acepta este compromiso para la siguiente fase, porque la exactitud de la lectura es prioritaria en el control de acceso vehicular. La elección es **provisional y condicionada**: deberá ratificarse con matrículas verificadas manualmente, datos representativos y pruebas de integración antes de cualquier decisión de despliegue.

**Decisión:** avanzar al siguiente prototipo con TrOCR Base Printed como candidato principal; conservar TrOCR Small Printed como referencia comparativa y alternativa de contingencia; mantener **pendiente** cualquier autorización para producción.
